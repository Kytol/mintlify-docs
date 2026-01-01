---
title: API Integration Guide
description: 'Complete guide for integrating with backend APIs'
icon: 'code'
---

# API Integration Guide

## Overview

This guide explains how to integrate with the Carepath Manager backend APIs, including Firebase setup, GraphQL configuration, and service implementation patterns.

## Table of Contents

1. [Setup & Configuration](#setup--configuration)
2. [Authentication](#authentication)
3. [GraphQL Queries](#graphql-queries)
4. [GraphQL Mutations](#graphql-mutations)
5. [Subscriptions](#subscriptions)
6. [Error Handling](#error-handling)
7. [Best Practices](#best-practices)

---

## Setup & Configuration

### Firebase Configuration

1. **Install Firebase dependencies:**

```bash
npm install firebase @angular/fire
```

2. **Create Firebase config file:**

```typescript
// src/environments/firebase.config.ts
export const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_PROJECT.firebaseapp.com",
  projectId: "YOUR_PROJECT_ID",
  storageBucket: "YOUR_PROJECT.appspot.com",
  messagingSenderId: "YOUR_SENDER_ID",
  appId: "YOUR_APP_ID"
};
```

3. **Initialize Firebase in app:**

```typescript
// src/app/app.config.ts
import { provideFirebaseApp, initializeApp } from '@angular/fire/app';
import { provideFirestore, getFirestore } from '@angular/fire/firestore';
import { provideAuth, getAuth } from '@angular/fire/auth';
import { provideStorage, getStorage } from '@angular/fire/storage';
import { firebaseConfig } from '../environments/firebase.config';

export const appConfig: ApplicationConfig = {
  providers: [
    provideFirebaseApp(() => initializeApp(firebaseConfig)),
    provideFirestore(() => getFirestore()),
    provideAuth(() => getAuth()),
    provideStorage(() => getStorage()),
    // ... other providers
  ]
};
```

### Apollo GraphQL Configuration

1. **Install Apollo dependencies:**

```bash
npm install @apollo/client graphql apollo-angular
```

2. **Create Apollo config:**

```typescript
// src/app/graphql.config.ts
import { Apollo, APOLLO_OPTIONS } from 'apollo-angular';
import { HttpLink } from 'apollo-angular/http';
import { InMemoryCache, ApolloClientOptions } from '@apollo/client/core';
import { setContext } from '@apollo/client/link/context';

export function createApollo(httpLink: HttpLink): ApolloClientOptions<any> {
  const auth = setContext((operation, context) => {
    const token = localStorage.getItem('auth_token');
    
    if (token === null) {
      return {};
    }
    
    return {
      headers: {
        Authorization: `Bearer ${token}`
      }
    };
  });

  return {
    link: auth.concat(httpLink.create({ uri: '/graphql/v1' })),
    cache: new InMemoryCache({
      typePolicies: {
        Query: {
          fields: {
            patients: {
              merge(existing = [], incoming) {
                return incoming;
              }
            }
          }
        }
      }
    }),
    defaultOptions: {
      watchQuery: {
        errorPolicy: 'all',
        fetchPolicy: 'cache-and-network'
      },
      query: {
        errorPolicy: 'all',
        fetchPolicy: 'network-only'
      },
      mutate: {
        errorPolicy: 'all'
      }
    }
  };
}

export const apolloProvider = {
  provide: APOLLO_OPTIONS,
  useFactory: createApollo,
  deps: [HttpLink]
};
```

3. **Add to app config:**

```typescript
// src/app/app.config.ts
import { apolloProvider } from './graphql.config';

export const appConfig: ApplicationConfig = {
  providers: [
    // ... Firebase providers
    provideHttpClient(),
    apolloProvider,
    // ... other providers
  ]
};
```

---

## Authentication

### Login with Firebase

```typescript
// src/app/services/auth.service.ts
import { Injectable } from '@angular/core';
import { Auth, signInWithEmailAndPassword, signOut } from '@angular/fire/auth';
import { Apollo, gql } from 'apollo-angular';
import { BehaviorSubject, Observable } from 'rxjs';
import { map } from 'rxjs/operators';

const AUTHENTICATE_USER = gql`
  mutation AuthenticateUser($firebaseToken: String!) {
    authenticateUser(firebaseToken: $firebaseToken) {
      token
      user {
        id
        name
        email
        role
        organizationId
      }
    }
  }
`;

@Injectable({
  providedIn: 'root'
})
export class AuthService {
  private currentUserSubject = new BehaviorSubject<any>(null);
  public currentUser$ = this.currentUserSubject.asObservable();

  constructor(
    private auth: Auth,
    private apollo: Apollo
  ) {
    this.loadStoredUser();
  }

  async login(email: string, password: string): Promise<void> {
    try {
      // Authenticate with Firebase
      const credential = await signInWithEmailAndPassword(this.auth, email, password);
      const firebaseToken = await credential.user.getIdToken();
      
      // Exchange for custom JWT with GraphQL
      const result = await this.apollo.mutate({
        mutation: AUTHENTICATE_USER,
        variables: { firebaseToken }
      }).toPromise();
      
      const { token, user } = result.data.authenticateUser;
      
      // Store token and user
      localStorage.setItem('auth_token', token);
      localStorage.setItem('current_user', JSON.stringify(user));
      this.currentUserSubject.next(user);
      
    } catch (error) {
      console.error('Login failed:', error);
      throw error;
    }
  }

  async logout(): Promise<void> {
    await signOut(this.auth);
    localStorage.removeItem('auth_token');
    localStorage.removeItem('current_user');
    this.currentUserSubject.next(null);
    this.apollo.client.clearStore();
  }

  private loadStoredUser(): void {
    const stored = localStorage.getItem('current_user');
    if (stored) {
      this.currentUserSubject.next(JSON.parse(stored));
    }
  }

  isAuthenticated(): boolean {
    return !!localStorage.getItem('auth_token');
  }
}
```

---

## GraphQL Queries

### Fetching Patients

```typescript
// src/app/services/patient.service.ts
import { Injectable } from '@angular/core';
import { Apollo, gql } from 'apollo-angular';
import { Observable } from 'rxjs';
import { map } from 'rxjs/operators';
import { Patient } from '../models/patient.model';

const GET_PATIENTS = gql`
  query GetPatients($filter: PatientFilterInput, $limit: Int, $offset: Int) {
    patients(filter: $filter, limit: $limit, offset: $offset) {
      id
      name
      personalId
      age
      gender
      status
      progress
      organizationId
      carepaths {
        id
        name
        status
        progress
        assignedAt
      }
      labels {
        id
        text
        color
        triggeredBy {
          questionLabel
          carepathName
          triggeredAt
        }
      }
      updatedAt
    }
  }
`;

const GET_PATIENT = gql`
  query GetPatient($id: ID!) {
    patient(id: $id) {
      id
      name
      personalId
      age
      gender
      phone
      email
      address
      emergencyContact {
        name
        relationship
        phone
      }
      medicalHistory
      allergies
      medications
      status
      progress
      carepaths {
        id
        carepathId
        name
        status
        progress
        assignedAt
        responsibleNurses {
          id
          name
        }
      }
      labels {
        id
        text
        color
        navigationUrl
        triggeredBy {
          questionId
          questionLabel
          responseValue
          carepathName
          triggeredAt
        }
      }
      notes {
        id
        content
        type
        author {
          id
          name
        }
        createdAt
      }
      createdAt
      updatedAt
    }
  }
`;

@Injectable({
  providedIn: 'root'
})
export class PatientService {
  constructor(private apollo: Apollo) {}

  getPatients(filter?: any, limit = 50, offset = 0): Observable<Patient[]> {
    return this.apollo.query({
      query: GET_PATIENTS,
      variables: { filter, limit, offset }
    }).pipe(
      map(result => result.data.patients)
    );
  }

  getPatientById(id: string): Observable<Patient> {
    return this.apollo.query({
      query: GET_PATIENT,
      variables: { id }
    }).pipe(
      map(result => result.data.patient)
    );
  }

  searchPatients(searchTerm: string): Observable<Patient[]> {
    return this.apollo.query({
      query: gql`
        query SearchPatients($searchTerm: String!, $limit: Int) {
          searchPatients(searchTerm: $searchTerm, limit: $limit) {
            id
            name
            personalId
            status
          }
        }
      `,
      variables: { searchTerm, limit: 20 }
    }).pipe(
      map(result => result.data.searchPatients)
    );
  }
}
```

### Fetching Forms

```typescript
const GET_FORM = gql`
  query GetForm($id: ID!) {
    form(id: $id) {
      id
      title
      description
      sections {
        id
        title
        order
        questions {
          id
          type
          label
          required
          options
          validation {
            min
            max
            pattern
          }
          conditionalDisplay {
            questionId
            operator
            value
          }
        }
      }
    }
  }
`;

getForm(id: string): Observable<Form> {
  return this.apollo.query({
    query: GET_FORM,
    variables: { id }
  }).pipe(
    map(result => result.data.form)
  );
}
```

---

## GraphQL Mutations

### Creating a Patient

```typescript
const CREATE_PATIENT = gql`
  mutation CreatePatient($input: CreatePatientInput!) {
    createPatient(input: $input) {
      id
      name
      personalId
      status
      createdAt
    }
  }
`;

createPatient(patientData: any): Observable<Patient> {
  return this.apollo.mutate({
    mutation: CREATE_PATIENT,
    variables: { input: patientData },
    update: (cache, { data: { createPatient } }) => {
      // Update cache after creating patient
      const query = GET_PATIENTS;
      const data: any = cache.readQuery({ query });
      
      cache.writeQuery({
        query,
        data: {
          patients: [...data.patients, createPatient]
        }
      });
    }
  }).pipe(
    map(result => result.data.createPatient)
  );
}
```

### Updating a Patient

```typescript
const UPDATE_PATIENT = gql`
  mutation UpdatePatient($id: ID!, $input: UpdatePatientInput!) {
    updatePatient(id: $id, input: $input) {
      id
      name
      status
      progress
      updatedAt
    }
  }
`;

updatePatient(id: string, updates: any): Observable<Patient> {
  return this.apollo.mutate({
    mutation: UPDATE_PATIENT,
    variables: { id, input: updates },
    optimisticResponse: {
      __typename: 'Mutation',
      updatePatient: {
        __typename: 'Patient',
        id,
        ...updates
      }
    }
  }).pipe(
    map(result => result.data.updatePatient)
  );
}
```

### Submitting a Form

```typescript
const SUBMIT_FORM = gql`
  mutation SubmitForm($input: SubmitFormInput!) {
    submitForm(input: $input) {
      id
      status
      submittedAt
      triggeredLabels {
        labelId
        questionId
        value
      }
    }
  }
`;

submitForm(formData: any): Observable<any> {
  return this.apollo.mutate({
    mutation: SUBMIT_FORM,
    variables: { input: formData },
    refetchQueries: [
      {
        query: GET_PATIENT,
        variables: { id: formData.patientId }
      }
    ]
  }).pipe(
    map(result => result.data.submitForm)
  );
}
```

### Assigning Carepath

```typescript
const ASSIGN_CAREPATH = gql`
  mutation AssignCarepath($input: AssignCarepathInput!) {
    assignCarepathToPatient(input: $input) {
      id
      carepathId
      name
      status
      progress
      assignedAt
      responsibleNurses {
        id
        name
      }
    }
  }
`;

assignCarepath(patientId: string, carepathId: string, nurseIds: string[]): Observable<any> {
  return this.apollo.mutate({
    mutation: ASSIGN_CAREPATH,
    variables: {
      input: {
        patientId,
        carepathId,
        responsibleNurseIds: nurseIds
      }
    }
  }).pipe(
    map(result => result.data.assignCarepathToPatient)
  );
}
```

---

## Subscriptions

### Real-time Patient Updates

```typescript
const PATIENT_UPDATED = gql`
  subscription PatientUpdated($patientId: ID!) {
    patientUpdated(patientId: $patientId) {
      id
      name
      status
      progress
      updatedAt
    }
  }
`;

subscribeToPatient(patientId: string): Observable<Patient> {
  return this.apollo.subscribe({
    query: PATIENT_UPDATED,
    variables: { patientId }
  }).pipe(
    map(result => result.data.patientUpdated)
  );
}
```

### Real-time Messages

```typescript
const MESSAGE_RECEIVED = gql`
  subscription MessageReceived($topicId: ID!) {
    messageReceived(topicId: $topicId) {
      id
      content
      sender {
        id
        name
      }
      createdAt
    }
  }
`;

subscribeToMessages(topicId: string): Observable<any> {
  return this.apollo.subscribe({
    query: MESSAGE_RECEIVED,
    variables: { topicId }
  }).pipe(
    map(result => result.data.messageReceived)
  );
}
```

### Alert Notifications

```typescript
const ALERT_CREATED = gql`
  subscription AlertCreated($organizationId: ID) {
    alertCreated(organizationId: $organizationId) {
      id
      type
      severity
      title
      patient {
        id
        name
      }
      createdAt
    }
  }
`;

subscribeToAlerts(organizationId: string): Observable<any> {
  return this.apollo.subscribe({
    query: ALERT_CREATED,
    variables: { organizationId }
  }).pipe(
    map(result => result.data.alertCreated)
  );
}
```

---

## Error Handling

### GraphQL Error Interceptor

```typescript
// src/app/services/graphql-error.interceptor.ts
import { Injectable } from '@angular/core';
import { Apollo } from 'apollo-angular';
import { onError } from '@apollo/client/link/error';
import { ToastService } from './toast.service';

@Injectable({
  providedIn: 'root'
})
export class GraphQLErrorInterceptor {
  constructor(
    private apollo: Apollo,
    private toast: ToastService
  ) {
    this.setupErrorHandling();
  }

  private setupErrorHandling(): void {
    const errorLink = onError(({ graphQLErrors, networkError, operation }) => {
      if (graphQLErrors) {
        graphQLErrors.forEach(({ message, locations, path, extensions }) => {
          console.error(
            `[GraphQL error]: Message: ${message}, Location: ${locations}, Path: ${path}`
          );
          
          // Handle specific error codes
          if (extensions?.code === 'UNAUTHENTICATED') {
            this.toast.error('Session expired. Please log in again.');
            // Redirect to login
          } else if (extensions?.code === 'FORBIDDEN') {
            this.toast.error('You do not have permission to perform this action.');
          } else {
            this.toast.error(message);
          }
        });
      }

      if (networkError) {
        console.error(`[Network error]: ${networkError}`);
        this.toast.error('Network error. Please check your connection.');
      }
    });

    // Add error link to Apollo client
    this.apollo.client.setLink(
      errorLink.concat(this.apollo.client.link)
    );
  }
}
```

### Service-Level Error Handling

```typescript
getPatients(): Observable<Patient[]> {
  return this.apollo.query({
    query: GET_PATIENTS
  }).pipe(
    map(result => result.data.patients),
    catchError(error => {
      console.error('Error fetching patients:', error);
      this.toast.error('Failed to load patients');
      return of([]); // Return empty array as fallback
    })
  );
}
```

---

## Best Practices

### 1. Query Optimization

**Use fragments for reusable fields:**

```typescript
const PATIENT_FIELDS = gql`
  fragment PatientFields on Patient {
    id
    name
    personalId
    status
    progress
  }
`;

const GET_PATIENTS = gql`
  ${PATIENT_FIELDS}
  query GetPatients {
    patients {
      ...PatientFields
    }
  }
`;
```

### 2. Caching Strategy

**Configure cache policies:**

```typescript
// Cache-first for rarely changing data
getCarepathTemplates(): Observable<Carepath[]> {
  return this.apollo.query({
    query: GET_CAREPATH_TEMPLATES,
    fetchPolicy: 'cache-first'
  }).pipe(
    map(result => result.data.carepathTemplates)
  );
}

// Network-only for real-time data
getAlerts(): Observable<Alert[]> {
  return this.apollo.query({
    query: GET_ALERTS,
    fetchPolicy: 'network-only'
  }).pipe(
    map(result => result.data.alerts)
  );
}
```

### 3. Pagination

**Implement cursor-based pagination:**

```typescript
loadMorePatients(cursor: string): Observable<{ patients: Patient[], hasMore: boolean }> {
  return this.apollo.query({
    query: gql`
      query LoadMorePatients($cursor: String, $limit: Int) {
        patients(after: $cursor, limit: $limit) {
          edges {
            node {
              id
              name
              status
            }
            cursor
          }
          pageInfo {
            hasNextPage
            endCursor
          }
        }
      }
    `,
    variables: { cursor, limit: 20 }
  }).pipe(
    map(result => ({
      patients: result.data.patients.edges.map(e => e.node),
      hasMore: result.data.patients.pageInfo.hasNextPage
    }))
  );
}
```

### 4. Optimistic Updates

**Update UI before server response:**

```typescript
acknowledgeAlert(alertId: string): Observable<Alert> {
  return this.apollo.mutate({
    mutation: ACKNOWLEDGE_ALERT,
    variables: { id: alertId },
    optimisticResponse: {
      __typename: 'Mutation',
      acknowledgeAlert: {
        __typename: 'Alert',
        id: alertId,
        status: 'acknowledged',
        acknowledgedAt: new Date().toISOString()
      }
    }
  }).pipe(
    map(result => result.data.acknowledgeAlert)
  );
}
```

### 5. Batch Queries

**Load multiple resources at once:**

```typescript
loadDashboardData(): Observable<any> {
  return this.apollo.query({
    query: gql`
      query DashboardData {
        dashboardMetrics {
          pendingApprovals
          activeCarepaths
          unreadMessages
        }
        alerts(filter: { status: PENDING }, limit: 10) {
          id
          severity
          title
        }
        patients(filter: { status: IN_PROGRESS }, limit: 20) {
          id
          name
          progress
        }
      }
    `
  }).pipe(
    map(result => result.data)
  );
}
```

### 6. Type Safety

**Generate TypeScript types from schema:**

```bash
npm install --save-dev @graphql-codegen/cli @graphql-codegen/typescript
npx graphql-code-generator init
```

**codegen.yml:**

```yaml
schema: 'http://localhost:3000/graphql'
documents: 'src/**/*.graphql'
generates:
  src/generated/graphql.ts:
    plugins:
      - typescript
      - typescript-operations
      - typescript-apollo-angular
```

### 7. Environment Configuration

**Use different endpoints per environment:**

```typescript
// src/environments/environment.ts
export const environment = {
  production: false,
  graphqlEndpoint: 'http://localhost:3000/graphql/v1',
  firebaseConfig: { /* dev config */ }
};

// src/environments/environment.prod.ts
export const environment = {
  production: true,
  graphqlEndpoint: 'https://api.carepath.com/graphql/v1',
  firebaseConfig: { /* prod config */ }
};
```

---

## Testing

### Mock Apollo Provider

```typescript
// src/app/services/patient.service.spec.ts
import { TestBed } from '@angular/core/testing';
import { ApolloTestingModule, ApolloTestingController } from 'apollo-angular/testing';
import { PatientService } from './patient.service';

describe('PatientService', () => {
  let service: PatientService;
  let controller: ApolloTestingController;

  beforeEach(() => {
    TestBed.configureTestingModule({
      imports: [ApolloTestingModule],
      providers: [PatientService]
    });
    
    service = TestBed.inject(PatientService);
    controller = TestBed.inject(ApolloTestingController);
  });

  it('should fetch patients', () => {
    service.getPatients().subscribe(patients => {
      expect(patients.length).toBe(2);
      expect(patients[0].name).toBe('John Doe');
    });

    const op = controller.expectOne(GET_PATIENTS);
    op.flush({
      data: {
        patients: [
          { id: '1', name: 'John Doe' },
          { id: '2', name: 'Jane Smith' }
        ]
      }
    });

    controller.verify();
  });
});
```

---

## Additional Resources

- [Apollo Client Documentation](https://www.apollographql.com/docs/angular/)
- [Firebase Documentation](https://firebase.google.com/docs)
- [GraphQL Best Practices](https://graphql.org/learn/best-practices/)
- [Apollo Caching](https://www.apollographql.com/docs/react/caching/overview/)
