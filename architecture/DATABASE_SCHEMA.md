---
title: Database Schema
description: 'Database structure and data models'
icon: 'database'
---

# Firebase Database Schema

## Overview

This document describes the Firestore database schema for the Carepath Manager application.

## Firestore Collections

### 1. users
**Collection Path**: `/users`

Stores user profile and authentication data.

```typescript
interface User {
  id: string;                    // Firestore document ID
  email: string;                 // User email
  name: string;                  // Full name
  role: 'admin' | 'nurse' | 'doctor' | 'patient';
  avatar?: string;               // Profile picture URL
  organizationId: string;        // Reference to organization
  createdAt: Timestamp;
  updatedAt: Timestamp;
  lastLogin?: Timestamp;
  active: boolean;
}
```

**Indexes**:
- `email` (unique)
- `organizationId + role`
- `active`

---

### 2. organizations
**Collection Path**: `/organizations`

Stores healthcare organization data.

```typescript
interface Organization {
  id: string;
  name: string;
  type: 'hospital' | 'department' | 'care-unit';
  address?: string;
  phone?: string;
  settings: {
    timezone: string;
    locale: string;
    branding: {
      logo?: string;
      primaryColor: string;
    };
  };
  createdAt: Timestamp;
  updatedAt: Timestamp;
  active: boolean;
}
```

**Indexes**:
- `type + active`
- `name`

---

### 3. patients
**Collection Path**: `/patients`

Stores patient information and medical records.

```typescript
interface Patient {
  id: string;
  personalId: string;           // National ID or SSN
  name: string;
  age?: number;
  gender?: 'Male' | 'Female' | 'Other';
  phone?: string;
  email?: string;
  address?: string;
  
  emergencyContact?: {
    name: string;
    relationship: string;
    phone: string;
  };
  
  medicalHistory?: string[];
  allergies?: string[];
  medications?: string[];
  conditions?: string[];
  admissionDate?: Timestamp;
  
  organizationId: string;        // Reference to organization
  primaryCarepathId?: string;    // Main carepath
  
  status: 'In Progress' | 'Awaiting Approval' | 'Completed' | 'On Hold';
  progress: number;              // 0-100
  
  createdAt: Timestamp;
  updatedAt: Timestamp;
  createdBy: string;             // User ID
  lastUpdateBy: string;          // User ID
}
```

**Indexes**:
- `organizationId + status`
- `personalId` (unique within organization)
- `primaryCarepathId`
- `status + updatedAt`

**Subcollections**:
- `/patients/{patientId}/carepaths` - Patient's assigned carepaths
- `/patients/{patientId}/labels` - Patient labels from questionnaires
- `/patients/{patientId}/notes` - Clinical notes

---

### 4. carepaths
**Collection Path**: `/carepaths`

Stores carepath definitions and templates.

```typescript
interface Carepath {
  id: string;
  name: string;
  description: string;
  category: string;
  
  phases: {
    id: string;
    name: string;
    order: number;
    estimatedDuration: number;   // in days
    forms: string[];             // Form IDs
    tasks: string[];             // Task IDs
  }[];
  
  organizationId: string;
  
  isTemplate: boolean;
  templateVersion: number;
  
  metadata: {
    totalForms: number;
    totalTasks: number;
    averageCompletionTime: number;
    usageCount: number;
  };
  
  createdAt: Timestamp;
  updatedAt: Timestamp;
  createdBy: string;
  active: boolean;
}
```

**Indexes**:
- `organizationId + active`
- `isTemplate`
- `category + active`

---

### 5. patient_carepaths
**Subcollection Path**: `/patients/{patientId}/carepaths`

Tracks individual patient's carepath assignments and progress.

```typescript
interface PatientCarepath {
  id: string;
  carepathId: string;            // Reference to carepath template
  templateId: string;
  name: string;
  
  status: 'In Progress' | 'Awaiting Approval' | 'Completed' | 'On Hold';
  progress: number;              // 0-100
  
  assignedAt: Timestamp;
  startedAt?: Timestamp;
  completedAt?: Timestamp;
  
  responsibleNurses: string[];   // User IDs
  
  currentPhase?: string;
  completedPhases: string[];
  
  notes?: string;
}
```

**Indexes**:
- `carepathId`
- `status + assignedAt`

---

### 6. forms
**Collection Path**: `/forms`

Stores form definitions and questionnaires.

```typescript
interface Form {
  id: string;
  title: string;
  description?: string;
  carepathId?: string;
  
  sections: {
    id: string;
    title: string;
    order: number;
    questions: {
      id: string;
      type: 'text' | 'number' | 'select' | 'multiselect' | 'date' | 'checkbox' | 'radio';
      label: string;
      required: boolean;
      options?: string[];
      validation?: {
        min?: number;
        max?: number;
        pattern?: string;
      };
      conditionalDisplay?: {
        questionId: string;
        operator: 'equals' | 'contains' | 'greater' | 'less';
        value: any;
      };
    }[];
  }[];
  
  organizationId: string;
  
  metadata: {
    version: number;
    submissionCount: number;
    averageCompletionTime: number;
  };
  
  createdAt: Timestamp;
  updatedAt: Timestamp;
  createdBy: string;
  active: boolean;
}
```

**Indexes**:
- `organizationId + active`
- `carepathId`

---

### 7. form_submissions
**Collection Path**: `/form_submissions`

Stores completed form responses.

```typescript
interface FormSubmission {
  id: string;
  formId: string;
  patientId: string;
  carepathId?: string;
  
  responses: {
    questionId: string;
    value: any;
    answeredAt: Timestamp;
  }[];
  
  status: 'draft' | 'pending' | 'approved' | 'rejected';
  
  submittedAt?: Timestamp;
  submittedBy: string;           // User ID
  
  reviewedAt?: Timestamp;
  reviewedBy?: string;
  reviewNotes?: string;
  
  organizationId: string;
  
  triggeredLabels?: {
    labelId: string;
    questionId: string;
    value: any;
  }[];
}
```

**Indexes**:
- `formId + status`
- `patientId + submittedAt`
- `status + submittedAt`
- `organizationId + status`

---

### 8. alerts
**Collection Path**: `/alerts`

Stores patient alerts and notifications.

```typescript
interface Alert {
  id: string;
  patientId: string;
  carepathId?: string;
  
  type: 'vital-signs' | 'medication' | 'appointment' | 'lab-results' | 'custom';
  severity: 'low' | 'medium' | 'high' | 'critical';
  
  title: string;
  description: string;
  
  status: 'pending' | 'acknowledged' | 'resolved' | 'dismissed';
  
  assignedTo?: string[];         // User IDs
  
  createdAt: Timestamp;
  acknowledgedAt?: Timestamp;
  acknowledgedBy?: string;
  resolvedAt?: Timestamp;
  resolvedBy?: string;
  
  metadata?: {
    vitalSign?: string;
    value?: number;
    threshold?: number;
    formSubmissionId?: string;
  };
  
  organizationId: string;
}
```

**Indexes**:
- `patientId + status`
- `severity + status + createdAt`
- `organizationId + status`
- `assignedTo + status`

---

### 9. messages
**Collection Path**: `/messages`

Stores chat messages and communications.

```typescript
interface Message {
  id: string;
  topicId: string;               // Chat topic/thread
  
  senderId: string;              // User ID
  senderName: string;
  senderRole: string;
  
  content: string;
  
  attachments?: {
    id: string;
    name: string;
    url: string;
    type: string;
    size: number;
  }[];
  
  replyTo?: string;              // Message ID
  
  reactions?: {
    userId: string;
    emoji: string;
  }[];
  
  createdAt: Timestamp;
  editedAt?: Timestamp;
  deletedAt?: Timestamp;
  
  read: boolean;
  readBy: string[];              // User IDs
}
```

**Indexes**:
- `topicId + createdAt`
- `senderId + createdAt`

---

### 10. chat_topics
**Collection Path**: `/chat_topics`

Stores chat topics/threads.

```typescript
interface ChatTopic {
  id: string;
  title: string;
  
  type: 'direct' | 'group' | 'patient-care';
  
  participants: {
    userId: string;
    role: string;
    joinedAt: Timestamp;
  }[];
  
  patientId?: string;            // If patient-related
  carepathId?: string;
  
  lastMessageAt?: Timestamp;
  lastMessagePreview?: string;
  
  unreadCount: {
    [userId: string]: number;
  };
  
  organizationId: string;
  
  createdAt: Timestamp;
  createdBy: string;
  
  archived: boolean;
  archivedAt?: Timestamp;
}
```

**Indexes**:
- `participants.userId + lastMessageAt`
- `patientId`
- `organizationId + archived`

---

### 11. patient_labels
**Subcollection Path**: `/patients/{patientId}/labels`

Stores labels generated from questionnaire responses.

```typescript
interface PatientLabel {
  id: string;
  text: string;
  color: 'red' | 'yellow' | 'blue' | 'green' | 'purple' | 'orange';
  
  triggeredBy: {
    questionId: string;
    questionLabel: string;
    responseValue: string;
    formSubmissionId: string;
    carepathName: string;
    triggeredAt: Timestamp;
  };
  
  navigationUrl?: string;
  
  active: boolean;
  dismissedAt?: Timestamp;
  dismissedBy?: string;
}
```

---

### 12. patient_notes
**Subcollection Path**: `/patients/{patientId}/notes`

Stores clinical notes for patients.

```typescript
interface PatientNote {
  id: string;
  content: string;
  type: 'clinical' | 'nursing' | 'administrative';
  
  authorId: string;
  authorName: string;
  authorRole: string;
  
  carepathId?: string;
  
  attachments?: {
    id: string;
    name: string;
    url: string;
  }[];
  
  tags?: string[];
  
  createdAt: Timestamp;
  updatedAt?: Timestamp;
  
  private: boolean;              // Visible only to care team
}
```

**Indexes**:
- `carepathId + createdAt`
- `type + createdAt`

---

### 13. audit_logs
**Collection Path**: `/audit_logs`

Stores audit trail for compliance.

```typescript
interface AuditLog {
  id: string;
  
  action: 'create' | 'read' | 'update' | 'delete' | 'login' | 'logout';
  entityType: 'patient' | 'user' | 'form' | 'alert' | 'message' | 'note';
  entityId: string;
  
  userId: string;
  userName: string;
  userRole: string;
  
  organizationId: string;
  
  changes?: {
    field: string;
    oldValue: any;
    newValue: any;
  }[];
  
  metadata?: {
    ipAddress?: string;
    userAgent?: string;
    sessionId?: string;
  };
  
  timestamp: Timestamp;
}
```

**Indexes**:
- `entityType + entityId + timestamp`
- `userId + timestamp`
- `action + timestamp`
- `organizationId + timestamp`

---

## Firestore Security Rules

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    
    // Helper functions
    function isAuthenticated() {
      return request.auth != null;
    }
    
    function isAdmin() {
      return isAuthenticated() && 
             get(/databases/$(database)/documents/users/$(request.auth.uid)).data.role == 'admin';
    }
    
    function belongsToOrganization(organizationId) {
      return isAuthenticated() && 
             get(/databases/$(database)/documents/users/$(request.auth.uid)).data.organizationId == organizationId;
    }
    
    // Users collection
    match /users/{userId} {
      allow read: if isAuthenticated() && 
                     (request.auth.uid == userId || isAdmin());
      allow write: if isAuthenticated() && 
                      (request.auth.uid == userId || isAdmin());
    }
    
    // Organizations collection
    match /organizations/{orgId} {
      allow read: if belongsToOrganization(orgId);
      allow write: if isAdmin();
    }
    
    // Patients collection
    match /patients/{patientId} {
      allow read: if isAuthenticated() && 
                     belongsToOrganization(resource.data.organizationId);
      allow create: if isAuthenticated() && 
                       belongsToOrganization(request.resource.data.organizationId);
      allow update: if isAuthenticated() && 
                       belongsToOrganization(resource.data.organizationId);
      allow delete: if isAdmin();
      
      // Patient subcollections
      match /carepaths/{carepathId} {
        allow read, write: if isAuthenticated() && 
                              belongsToOrganization(get(/databases/$(database)/documents/patients/$(patientId)).data.organizationId);
      }
      
      match /labels/{labelId} {
        allow read, write: if isAuthenticated() && 
                              belongsToOrganization(get(/databases/$(database)/documents/patients/$(patientId)).data.organizationId);
      }
      
      match /notes/{noteId} {
        allow read, write: if isAuthenticated() && 
                              belongsToOrganization(get(/databases/$(database)/documents/patients/$(patientId)).data.organizationId);
      }
    }
    
    // Forms and submissions
    match /forms/{formId} {
      allow read: if isAuthenticated() && 
                     belongsToOrganization(resource.data.organizationId);
      allow write: if isAdmin();
    }
    
    match /form_submissions/{submissionId} {
      allow read: if isAuthenticated() && 
                     belongsToOrganization(resource.data.organizationId);
      allow create: if isAuthenticated() && 
                       belongsToOrganization(request.resource.data.organizationId);
      allow update: if isAuthenticated() && 
                       belongsToOrganization(resource.data.organizationId);
      allow delete: if isAdmin();
    }
    
    // Alerts
    match /alerts/{alertId} {
      allow read, write: if isAuthenticated() && 
                            belongsToOrganization(resource.data.organizationId);
    }
    
    // Messages and chat topics
    match /messages/{messageId} {
      allow read, write: if isAuthenticated();
    }
    
    match /chat_topics/{topicId} {
      allow read: if isAuthenticated() && 
                     request.auth.uid in resource.data.participants[].userId;
      allow write: if isAuthenticated() && 
                      request.auth.uid in resource.data.participants[].userId;
    }
    
    // Audit logs (read-only for most users)
    match /audit_logs/{logId} {
      allow read: if isAdmin();
      allow write: if false; // Only server-side writes
    }
  }
}
```

## Data Migration Strategy

### Phase 1: Parallel Run
- Keep mock data active
- Implement Firebase services alongside
- Dual-write to both systems
- Read from Firebase with mock fallback

### Phase 2: Validation
- Compare data consistency
- Verify query performance
- Test all user workflows
- Monitor error rates

### Phase 3: Cutover
- Switch primary data source to Firebase
- Disable mock data
- Keep mock as backup for 30 days
- Monitor production metrics

### Phase 4: Optimization
- Add missing indexes
- Optimize query patterns
- Implement caching
- Fine-tune security rules
