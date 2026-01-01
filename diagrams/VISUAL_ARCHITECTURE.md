---
title: Visual Architecture
description: 'System architecture diagrams and visual documentation'
icon: 'sitemap'
---

# Visual Architecture Overview

## System Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────────┐
│                         PRESENTATION LAYER                          │
│                                                                     │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌──────────┐ │
│  │  Dashboard  │  │  Patients   │  │    Forms    │  │  Alerts  │ │
│  └──────┬──────┘  └──────┬──────┘  └──────┬──────┘  └────┬─────┘ │
│         │                │                │               │        │
│  ┌──────┴────────────────┴────────────────┴───────────────┴─────┐ │
│  │               Angular Components & Routes                     │ │
│  └────────────────────────────┬──────────────────────────────────┘ │
└─────────────────────────────┬─┴────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────────┐
│                        APPLICATION LAYER                            │
│                                                                     │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐            │
│  │   Patient    │  │    Alert     │  │    Form      │            │
│  │   Service    │  │   Service    │  │   Service    │  ...       │
│  └──────┬───────┘  └──────┬───────┘  └──────┬───────┘            │
│         │                 │                  │                     │
│  ┌──────┴─────────────────┴──────────────────┴──────────────────┐ │
│  │         Currently using MOCK_DATA (configurable)              │ │
│  │         Can switch to Firebase/GraphQL services               │ │
│  └────────────────────────────┬──────────────────────────────────┘ │
└─────────────────────────────┬─┴────────────────────────────────────┘
                              │
        ┌─────────────────────┴─────────────────────┐
        │                                           │
        ▼                                           ▼
┌────────────────────┐                    ┌────────────────────┐
│   FIREBASE PATH    │                    │   GRAPHQL PATH     │
│    (DIRECT)        │                    │   (OPTIONAL)       │
│                    │                    │                    │
│  ┌──────────────┐  │                    │  ┌──────────────┐  │
│  │   Firebase   │  │                    │  │    Apollo    │  │
│  │  Services    │  │                    │  │   Client     │  │
│  │              │  │                    │  │              │  │
│  │ • Patient    │  │                    │  │ Queries &    │  │
│  │ • Alert      │  │                    │  │ Mutations    │  │
│  │ • Form       │  │                    │  │              │  │
│  │ • ...        │  │                    │  │ Subscriptions│  │
│  └──────┬───────┘  │                    │  └──────┬───────┘  │
│         │          │                    │         │          │
└─────────┼──────────┘                    └─────────┼──────────┘
          │                                         │
          │                                         ▼
          │                               ┌────────────────────┐
          │                               │  GraphQL Server    │
          │                               │  (Apollo Server)   │
          │                               │                    │
          │                               │  Resolvers         │
          │                               └────────┬───────────┘
          │                                        │
          └────────────────┬───────────────────────┘
                           │
                           ▼
        ┌──────────────────────────────────────────────┐
        │           DATA LAYER (FIREBASE)              │
        │                                              │
        │  ┌────────────────────────────────────────┐ │
        │  │        Firebase Firestore              │ │
        │  │                                        │ │
        │  │  Collections:                          │ │
        │  │  • users                               │ │
        │  │  • organizations                       │ │
        │  │  • patients                            │ │
        │  │    └─ carepaths (subcollection)        │ │
        │  │    └─ labels (subcollection)           │ │
        │  │    └─ notes (subcollection)            │ │
        │  │  • carepaths                           │ │
        │  │  • forms                               │ │
        │  │  • form_submissions                    │ │
        │  │  • alerts                              │ │
        │  │  • messages                            │ │
        │  │  • chat_topics                         │ │
        │  │  • audit_logs                          │ │
        │  └────────────────────────────────────────┘ │
        │                                              │
        │  ┌────────────────────────────────────────┐ │
        │  │     Firebase Authentication            │ │
        │  │  • Email/Password                      │ │
        │  │  • JWT Tokens                          │ │
        │  └────────────────────────────────────────┘ │
        │                                              │
        │  ┌────────────────────────────────────────┐ │
        │  │        Firebase Storage                │ │
        │  │  • Patient documents                   │ │
        │  │  • Form attachments                    │ │
        │  │  • Images                              │ │
        │  └────────────────────────────────────────┘ │
        └──────────────────────────────────────────────┘
```

## Data Flow Examples

### Example 1: Creating a Patient

```
User Interface (Form)
      │
      │ Submit
      ▼
PatientService.createPatient()
      │
      ├─────── Mock Mode ────────┐
      │                          │
      │                          ▼
      │                     MOCK_PATIENTS.push()
      │
      └─────── Real Backend ─────┐
                                 │
                                 ▼
                    FirebasePatientService.create()
                                 │
                                 ▼
                    Firestore: patients/{id}
                                 │
                                 ▼
                    AuditLogService.log()
                                 │
                                 ▼
                    Firestore: audit_logs/{id}
                                 │
                                 ▼
                    Real-time update subscription
                                 │
                                 ▼
                    UI updates automatically
```

### Example 2: Loading Patient List

```
Dashboard Component loads
      │
      ▼
PatientService.getPatients()
      │
      ├─────── Mock Mode ────────┐
      │                          │
      │                          ▼
      │                     Return MOCK_PATIENTS
      │
      └─────── Real Backend ─────┐
                                 │
          ┌──────────────────────┴─────────────┐
          │                                    │
          ▼                                    ▼
    Firebase Direct                      GraphQL Query
          │                                    │
          ▼                                    ▼
    FirebasePatientService                 Apollo Client
          │                                    │
          ▼                                    ▼
    Firestore Query                      GraphQL Server
    patients/?filters                          │
          │                                    ▼
          │                               Resolver fetches
          │                               from Firestore
          │                                    │
          └────────────┬────────────────────────┘
                       │
                       ▼
              Patient[] returned
                       │
                       ▼
              Component renders
```

### Example 3: Real-time Alert

```
Patient vital signs exceed threshold
                │
                ▼
    Form submission processed
                │
                ▼
    Label trigger detected
                │
                ▼
    AlertService.createAlert()
                │
                ▼
    FirebaseAlertService.create()
                │
                ▼
    Firestore: alerts/{id}
                │
                ├────────────────┐
                │                │
                ▼                ▼
    Subscription         Email notification
    pushes to UI         sent to assigned nurses
                │
                ▼
    Dashboard alert counter updates
                │
                ▼
    Toast notification displayed
```

## Security Layers

```
┌──────────────────────────────────────────────────┐
│             REQUEST PROCESSING                   │
└──────────────────────────────────────────────────┘
                     │
                     ▼
┌──────────────────────────────────────────────────┐
│  1. Authentication (Firebase Auth)               │
│     • Verify JWT token                           │
│     • Check token expiration                     │
│     • Extract user ID and role                   │
└──────────────────────────────────────────────────┘
                     │
                     ▼
┌──────────────────────────────────────────────────┐
│  2. Authorization (Firestore Rules)              │
│     • Check user's organization                  │
│     • Verify role permissions                    │
│     • Validate data access scope                 │
└──────────────────────────────────────────────────┘
                     │
                     ▼
┌──────────────────────────────────────────────────┐
│  3. Data Validation                              │
│     • Validate input types                       │
│     • Check required fields                      │
│     • Sanitize user input                        │
└──────────────────────────────────────────────────┘
                     │
                     ▼
┌──────────────────────────────────────────────────┐
│  4. Business Logic                               │
│     • Execute operation                          │
│     • Apply business rules                       │
│     • Update related data                        │
└──────────────────────────────────────────────────┘
                     │
                     ▼
┌──────────────────────────────────────────────────┐
│  5. Audit Logging                                │
│     • Log action taken                           │
│     • Record user and timestamp                  │
│     • Store before/after values                  │
└──────────────────────────────────────────────────┘
```

## Technology Stack

```
Frontend
  ├─ Angular 19.2
  ├─ TypeScript 5.7
  ├─ TailwindCSS 3.4
  ├─ Angular Material 19.2
  └─ RxJS 7.8

Backend Integration
  ├─ Firebase SDK 10.x
  ├─ AngularFire 18.0
  ├─ Apollo Client 3.x
  └─ GraphQL 16.x

Database
  ├─ Firestore (NoSQL)
  ├─ Firebase Auth
  └─ Firebase Storage

Optional GraphQL Server
  ├─ Apollo Server
  ├─ Firebase Admin SDK
  └─ Node.js/Express
```

## Deployment Architecture

```
┌─────────────────────────────────────────────────┐
│              CDN / Hosting                      │
│         (Firebase Hosting / Vercel)             │
│                                                 │
│  Static Assets: HTML, CSS, JS, Images          │
└─────────────────┬───────────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────────┐
│           Angular Application                   │
│        (Runs in user's browser)                 │
└─────────────────┬───────────────────────────────┘
                  │
        ┌─────────┴─────────┐
        │                   │
        ▼                   ▼
┌─────────────┐    ┌─────────────────┐
│  Firebase   │    │  GraphQL Server │
│  Services   │    │   (Optional)    │
│             │    │                 │
│ • Auth      │    │ Cloud Functions │
│ • Firestore │    │ or Cloud Run    │
│ • Storage   │    │                 │
└─────────────┘    └─────────────────┘
```

## Scalability Features

```
Performance Optimizations
  ├─ Client-side caching (Apollo/Firestore)
  ├─ Lazy loading of modules
  ├─ Pagination for large datasets
  ├─ Composite indexes for queries
  └─ CDN for static assets

Scaling Strategy
  ├─ Firestore auto-scales reads/writes
  ├─ Firebase Auth handles millions of users
  ├─ Storage auto-scales for files
  ├─ GraphQL server can scale horizontally
  └─ Multi-region deployment support

Monitoring
  ├─ Firebase Performance Monitoring
  ├─ Error tracking and reporting
  ├─ Usage analytics
  ├─ Audit log analysis
  └─ Cost monitoring
```

## Migration Path

```
Phase 1: Development (Current)
  └─ Mock data mode
     All features work with sample data

Phase 2: Firebase Setup
  ├─ Create Firebase project
  ├─ Configure credentials
  └─ Deploy security rules

Phase 3: Service Migration
  ├─ Update service imports
  ├─ Replace mock data with Firebase
  └─ Test each service

Phase 4: Gradual Rollout
  ├─ Enable for test users
  ├─ Monitor performance
  ├─ Fix any issues
  └─ Full deployment

Phase 5: Optimization
  ├─ Add missing indexes
  ├─ Optimize queries
  ├─ Enable caching
  └─ Fine-tune security rules
```

## File Organization

```
src/
├── app/
│   ├── firebase/                    ← Firebase Services
│   │   ├── firestore.models.ts     ← Type definitions
│   │   ├── firebase-base.service.ts ← Base CRUD service
│   │   ├── firebase-patient.service.ts
│   │   └── firebase-alert.service.ts
│   │
│   ├── services/                    ← Application Services
│   │   ├── patient.service.ts      ← Uses mock or Firebase
│   │   ├── alert.service.ts
│   │   └── ...
│   │
│   ├── models/                      ← App Models
│   │   ├── patient.model.ts
│   │   └── ...
│   │
│   └── pages/
│       └── settings/
│           └── settings.component.ts ← Data Models UI
│
├── environments/
│   ├── firebase.config.ts           ← Firebase credentials
│   └── graphql.config.ts            ← GraphQL endpoint
│
└── docs/
    ├── architecture/                ← Architecture docs
    ├── api/                         ← API documentation
    ├── diagrams/                    ← Visual diagrams
    └── IMPLEMENTATION_SUMMARY.md    ← Overview
```

## Quick Reference

### Key Files

| File | Purpose |
|------|---------|
| `firestore.models.ts` | All Firestore type definitions |
| `firebase-base.service.ts` | Generic CRUD operations |
| `firebase-patient.service.ts` | Patient-specific operations |
| `firebase.config.ts` | Firebase project credentials |
| `settings.component.ts` | Data Models UI |
| `DATABASE_SCHEMA.md` | Complete schema reference |
| `GRAPHQL_SCHEMA.md` | GraphQL API reference |

### Key Concepts

- **Collections**: Top-level Firestore data containers
- **Subcollections**: Nested collections under a document
- **Timestamp**: Firestore's date/time type
- **Observable**: RxJS pattern for async data
- **Query Constraints**: Filters, ordering, pagination
- **Security Rules**: Firestore access control

### Common Operations

```typescript
// Get all patients
patientService.getAll()

// Get patient by ID
patientService.getById('P-001')

// Create patient
patientService.create(patientData)

// Update patient
patientService.update('P-001', updates)

// Delete patient
patientService.delete('P-001')

// Query with filters
patientService.getAll({
  where: [{ field: 'status', operator: '==', value: 'In Progress' }],
  orderBy: [{ field: 'updatedAt', direction: 'desc' }],
  limit: 50
})
```

---

**For complete details, see:**
- `docs/architecture/BACKEND_ARCHITECTURE.md`
- `docs/architecture/DATABASE_SCHEMA.md`
- `docs/api/GRAPHQL_SCHEMA.md`
- `docs/IMPLEMENTATION_SUMMARY.md`
