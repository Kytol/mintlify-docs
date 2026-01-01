---
title: Data Flow Diagrams
description: 'Visual diagrams showing data flow through the system'
icon: 'arrows-split-up-and-left'
---

# Data Flow Diagrams

## System Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                         USER INTERFACE                          │
│  (Angular Components - Dashboard, Patients, Forms, Messages)   │
└────────────────┬────────────────────────────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────────────────────────────┐
│                     ANGULAR SERVICES                            │
│  (PatientService, FormService, AlertService, ChatService)      │
└────────────────┬────────────────────────────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────────────────────────────┐
│                     APOLLO CLIENT                               │
│         (GraphQL Query/Mutation Execution)                      │
└────────────────┬────────────────────────────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────────────────────────────┐
│                     GRAPHQL API LAYER                           │
│         (Resolvers, Type Definitions, Auth Middleware)          │
└────────────────┬────────────────────────────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────────────────────────────┐
│                   FIREBASE SERVICES                             │
│      (Firestore Operations, Authentication, Storage)            │
└────────────────┬────────────────────────────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────────────────────────────┐
│                    FIREBASE BACKEND                             │
│   (Firestore Database, Auth, Storage, Cloud Functions)         │
└─────────────────────────────────────────────────────────────────┘
```

---

## Patient Data Flow

### Creating a New Patient

```
User fills form → Component validates
                        ↓
                 PatientService.createPatient()
                        ↓
                 Apollo mutation: createPatient
                        ↓
                 GraphQL Resolver validates input
                        ↓
                 Firebase Service creates document
                        ↓
                 Firestore: /patients/{id}
                        ↓
                 Audit log created
                        ↓
                 Response flows back to UI
                        ↓
                 Component updates state
                        ↓
                 User sees confirmation
```

### Reading Patient List

```
Component loads → PatientService.getPatients()
                        ↓
                 Apollo query: patients
                        ↓
                 GraphQL Resolver processes query
                        ↓
                 Apply filters & pagination
                        ↓
                 Firebase Service queries Firestore
                        ↓
                 Firestore returns documents
                        ↓
                 Transform to Patient objects
                        ↓
                 Cache in Apollo
                        ↓
                 Component renders list
```

### Real-time Patient Updates

```
Patient updated → GraphQL Subscription: patientUpdated
                        ↓
                 Firebase onSnapshot listener
                        ↓
                 Firestore change detected
                        ↓
                 Subscription pushes update
                        ↓
                 Apollo cache updated
                        ↓
                 Component re-renders automatically
```

---

## Form Submission Flow

### Submitting a Form

```
User fills form → Component validates locally
                        ↓
                 FormService.submitForm()
                        ↓
                 Apollo mutation: submitForm
                        ↓
                 GraphQL Resolver validates
                        ↓
                 Check conditional logic
                        ↓
                 Process label triggers
                        ↓
                 Firebase Service creates submission
                        ↓
                 Firestore: /form_submissions/{id}
                        ↓
                 Create patient labels if triggered
                        ↓
                 Create alert if needed
                        ↓
                 Update patient progress
                        ↓
                 Audit log created
                        ↓
                 Response with submission ID
                        ↓
                 Component shows success
                        ↓
                 Navigate to next step
```

### Reviewing a Form Submission

```
Nurse opens form → Load submission data
                        ↓
                 Apollo query: formSubmission(id)
                        ↓
                 GraphQL Resolver fetches data
                        ↓
                 Firebase Service gets document
                        ↓
                 Includes related patient data
                        ↓
                 Display in review UI
                        ↓
                 Nurse approves/rejects
                        ↓
                 Apollo mutation: reviewFormSubmission
                        ↓
                 Update submission status
                        ↓
                 Update patient carepath progress
                        ↓
                 Send notification to patient
                        ↓
                 Audit log created
```

---

## Alert Management Flow

### Creating an Alert

```
System detects issue → AlertService.createAlert()
     OR                        ↓
User creates manually → Apollo mutation: createAlert
                        ↓
                 GraphQL Resolver validates
                        ↓
                 Check severity and type
                        ↓
                 Firebase Service creates alert
                        ↓
                 Firestore: /alerts/{id}
                        ↓
                 Assign to responsible users
                        ↓
                 Send notifications
                        ↓
                 Create notification entries
                        ↓
                 Push subscription updates
                        ↓
                 Dashboard counter updates
```

### Alert Lifecycle

```
Alert Created (status: pending)
        ↓
User acknowledges → status: acknowledged
        ↓
User investigates and takes action
        ↓
User resolves → status: resolved
        ↓
Alert closed
```

### Alert Query Flow

```
Dashboard loads → AlertService.getAlerts()
                        ↓
                 Apollo query: alerts(filter)
                        ↓
                 GraphQL Resolver applies filters
                        ↓
                 Filter by: severity, status, assigned user
                        ↓
                 Firebase Service queries with composite index
                        ↓
                 Firestore returns matching alerts
                        ↓
                 Include patient and carepath data
                        ↓
                 Sort by priority and timestamp
                        ↓
                 Component displays alert cards
```

---

## Messaging Flow

### Sending a Message

```
User types message → Component validates
                        ↓
                 ChatService.sendMessage()
                        ↓
                 Apollo mutation: sendMessage
                        ↓
                 GraphQL Resolver validates
                        ↓
                 Check user permissions
                        ↓
                 Firebase Service creates message
                        ↓
                 Firestore: /messages/{id}
                        ↓
                 Update chat topic lastMessageAt
                        ↓
                 Increment unread counts
                        ↓
                 Push notification to recipients
                        ↓
                 Real-time subscription updates
                        ↓
                 Recipients see new message
```

### Real-time Chat

```
User opens chat → Subscribe to messages
                        ↓
                 GraphQL subscription: messageReceived(topicId)
                        ↓
                 Firebase onSnapshot listener
                        ↓
                 New message added to Firestore
                        ↓
                 Subscription pushes to client
                        ↓
                 Apollo cache adds message
                        ↓
                 Component renders new message
                        ↓
                 Mark as read mutation
                        ↓
                 Update read status in Firestore
```

---

## Carepath Assignment Flow

### Assigning Carepath to Patient

```
Nurse selects carepath → Component shows confirmation
                        ↓
                 CarepathService.assignCarepath()
                        ↓
                 Apollo mutation: assignCarepathToPatient
                        ↓
                 GraphQL Resolver validates
                        ↓
                 Check if carepath already assigned
                        ↓
                 Load carepath template
                        ↓
                 Create patient carepath instance
                        ↓
                 Firebase Service creates subcollection
                        ↓
                 /patients/{id}/carepaths/{carepathId}
                        ↓
                 Initialize phases and forms
                        ↓
                 Assign responsible nurses
                        ↓
                 Update patient primaryCarepathId
                        ↓
                 Create initial notifications
                        ↓
                 Audit log created
                        ↓
                 Response with carepath details
                        ↓
                 Navigate to patient carepath view
```

---

## Authentication Flow

### User Login

```
User enters credentials → Component validates format
                        ↓
                 AuthService.login()
                        ↓
                 Firebase Authentication
                        ↓
                 signInWithEmailAndPassword()
                        ↓
                 Firebase validates credentials
                        ↓
                 Returns Firebase ID token
                        ↓
                 Exchange for custom JWT
                        ↓
                 GraphQL mutation: authenticateUser
                        ↓
                 Validate Firebase token
                        ↓
                 Load user profile from Firestore
                        ↓
                 Generate JWT with user data
                        ↓
                 Store JWT in local storage
                        ↓
                 Set Apollo auth header
                        ↓
                 Create audit log entry
                        ↓
                 Redirect to dashboard
```

### Authenticated Request

```
User action → Service method called
                        ↓
                 Apollo Client intercepts
                        ↓
                 Add Authorization header with JWT
                        ↓
                 GraphQL request sent to server
                        ↓
                 Auth middleware validates JWT
                        ↓
                 Extract user info from token
                        ↓
                 Add to request context
                        ↓
                 Resolver accesses context.user
                        ↓
                 Apply authorization rules
                        ↓
                 Execute query/mutation
                        ↓
                 Return response
```

---

## File Upload Flow

### Uploading Patient Documents

```
User selects file → Component validates size/type
                        ↓
                 FileService.upload()
                        ↓
                 Generate unique file path
                        ↓
                 Firebase Storage upload
                        ↓
                 /patients/{id}/documents/{filename}
                        ↓
                 Get download URL
                        ↓
                 Create document metadata
                        ↓
                 Apollo mutation: createPatientDocument
                        ↓
                 Save metadata to Firestore
                        ↓
                 /patients/{id}/documents (subcollection)
                        ↓
                 Audit log created
                        ↓
                 Return document info
                        ↓
                 Component shows success
```

---

## Cache Strategy

### Apollo Cache Flow

```
Query executed → Check Apollo cache
                        ↓
         ┌──────────────┴──────────────┐
         │                             │
    Cache Hit                      Cache Miss
         │                             │
    Return cached data          Fetch from GraphQL
         │                             │
         └──────────────┬──────────────┘
                        │
                 Update Apollo cache
                        │
                 Normalize data
                        │
                 Store by ID and typename
                        │
                 Component receives data
```

### Cache Invalidation

```
Mutation executed → Automatic cache update
                        ↓
                 Apollo identifies affected queries
                        ↓
                 Refetch affected data
                        ↓
                 Update cache
                        ↓
                 Subscribed components re-render
```

---

## Error Handling Flow

```
Error occurs → GraphQL resolver catches error
                        ↓
                 Format error response
                        ↓
                 Include error code and message
                        ↓
                 Return to Apollo Client
                        ↓
                 Apollo error handling interceptor
                        ↓
         ┌──────────────┴──────────────┐
         │                             │
    Network Error              GraphQL Error
         │                             │
    Show offline message      Extract error details
         │                             │
         └──────────────┬──────────────┘
                        │
                 Service catches error
                        │
                 ToastService shows message
                        │
                 Log error for monitoring
                        │
                 Component shows error state
```

---

## Data Synchronization

### Offline-First Strategy (Future Enhancement)

```
User makes change → Store in local cache
                        ↓
                 Mark as pending sync
                        ↓
         ┌──────────────┴──────────────┐
         │                             │
      Online                        Offline
         │                             │
    Sync to server              Queue for later
         │                             │
    Update server state         Store in IndexedDB
         │                             │
    Confirm success             Show pending indicator
         │                             │
         └──────────────┬──────────────┘
                        │
                 When online, sync queue
                        │
                 Resolve conflicts
                        │
                 Update UI
```

---

## Performance Optimization

### Query Batching

```
Multiple components load → Collect queries
                        ↓
                 Batch within time window (10ms)
                        ↓
                 Send as single GraphQL request
                        ↓
                 Server processes in parallel
                        ↓
                 Return batched response
                        ↓
                 Apollo distributes to components
```

### Pagination Flow

```
User scrolls/clicks next → Load more data
                        ↓
                 Apollo query with offset/cursor
                        ↓
                 GraphQL resolver applies pagination
                        ↓
                 Firebase query with startAfter()
                        ↓
                 Return page of results
                        ↓
                 Apollo merges with existing cache
                        ↓
                 Component appends to list
                        ↓
                 Infinite scroll continues
```
