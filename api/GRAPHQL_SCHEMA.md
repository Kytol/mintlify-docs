---
title: GraphQL Schema
description: 'GraphQL API schema definitions and types'
icon: 'diagram-project'
---

# GraphQL API Schema

## Overview

This document defines the GraphQL schema for the Carepath Manager application.

## Schema Definition

### Scalar Types

```graphql
scalar DateTime
scalar JSON
```

---

## Type Definitions

### User Types

```graphql
type User {
  id: ID!
  email: String!
  name: String!
  role: UserRole!
  avatar: String
  organizationId: ID!
  organization: Organization!
  createdAt: DateTime!
  updatedAt: DateTime!
  lastLogin: DateTime
  active: Boolean!
}

enum UserRole {
  ADMIN
  NURSE
  DOCTOR
  PATIENT
}

input CreateUserInput {
  email: String!
  name: String!
  password: String!
  role: UserRole!
  organizationId: ID!
  avatar: String
}

input UpdateUserInput {
  name: String
  avatar: String
  active: Boolean
}
```

---

### Organization Types

```graphql
type Organization {
  id: ID!
  name: String!
  type: OrganizationType!
  address: String
  phone: String
  settings: OrganizationSettings!
  createdAt: DateTime!
  updatedAt: DateTime!
  active: Boolean!
  users: [User!]!
  patients: [Patient!]!
}

enum OrganizationType {
  HOSPITAL
  DEPARTMENT
  CARE_UNIT
}

type OrganizationSettings {
  timezone: String!
  locale: String!
  branding: BrandingSettings!
}

type BrandingSettings {
  logo: String
  primaryColor: String!
}

input CreateOrganizationInput {
  name: String!
  type: OrganizationType!
  address: String
  phone: String
}

input UpdateOrganizationInput {
  name: String
  type: OrganizationType
  address: String
  phone: String
  active: Boolean
}
```

---

### Patient Types

```graphql
type Patient {
  id: ID!
  personalId: String!
  name: String!
  age: Int
  gender: Gender
  phone: String
  email: String
  address: String
  emergencyContact: EmergencyContact
  medicalHistory: [String!]
  allergies: [String!]
  medications: [String!]
  conditions: [String!]
  admissionDate: DateTime
  organizationId: ID!
  organization: Organization!
  primaryCarepathId: ID
  primaryCarepath: PatientCarepath
  carepaths: [PatientCarepath!]!
  labels: [PatientLabel!]!
  notes: [PatientNote!]!
  status: PatientStatus!
  progress: Int!
  createdAt: DateTime!
  updatedAt: DateTime!
  createdBy: User!
  lastUpdateBy: User!
}

enum Gender {
  MALE
  FEMALE
  OTHER
}

enum PatientStatus {
  IN_PROGRESS
  AWAITING_APPROVAL
  COMPLETED
  ON_HOLD
}

type EmergencyContact {
  name: String!
  relationship: String!
  phone: String!
}

input EmergencyContactInput {
  name: String!
  relationship: String!
  phone: String!
}

input CreatePatientInput {
  personalId: String!
  name: String!
  age: Int
  gender: Gender
  phone: String
  email: String
  address: String
  emergencyContact: EmergencyContactInput
  medicalHistory: [String!]
  allergies: [String!]
  medications: [String!]
  conditions: [String!]
  admissionDate: DateTime
  organizationId: ID!
}

input UpdatePatientInput {
  name: String
  age: Int
  gender: Gender
  phone: String
  email: String
  address: String
  emergencyContact: EmergencyContactInput
  medicalHistory: [String!]
  allergies: [String!]
  medications: [String!]
  conditions: [String!]
  status: PatientStatus
  progress: Int
}

input PatientFilterInput {
  status: PatientStatus
  organizationId: ID
  carepathId: ID
  searchTerm: String
}
```

---

### Carepath Types

```graphql
type Carepath {
  id: ID!
  name: String!
  description: String!
  category: String!
  phases: [CarepathPhase!]!
  organizationId: ID!
  organization: Organization!
  isTemplate: Boolean!
  templateVersion: Int!
  metadata: CarepathMetadata!
  createdAt: DateTime!
  updatedAt: DateTime!
  createdBy: User!
  active: Boolean!
}

type CarepathPhase {
  id: ID!
  name: String!
  order: Int!
  estimatedDuration: Int!
  forms: [Form!]!
  tasks: [String!]!
}

type CarepathMetadata {
  totalForms: Int!
  totalTasks: Int!
  averageCompletionTime: Int!
  usageCount: Int!
}

type PatientCarepath {
  id: ID!
  carepathId: ID!
  carepath: Carepath!
  templateId: ID!
  name: String!
  status: PatientStatus!
  progress: Int!
  assignedAt: DateTime!
  startedAt: DateTime
  completedAt: DateTime
  responsibleNurses: [User!]!
  currentPhase: ID
  completedPhases: [ID!]!
  notes: String
}

input CreateCarepathInput {
  name: String!
  description: String!
  category: String!
  phases: [CarepathPhaseInput!]!
  organizationId: ID!
  isTemplate: Boolean
}

input CarepathPhaseInput {
  name: String!
  order: Int!
  estimatedDuration: Int!
  formIds: [ID!]!
  tasks: [String!]!
}

input UpdateCarepathInput {
  name: String
  description: String
  category: String
  phases: [CarepathPhaseInput!]
  active: Boolean
}

input AssignCarepathInput {
  patientId: ID!
  carepathId: ID!
  responsibleNurseIds: [ID!]!
  notes: String
}

input UpdatePatientCarepathInput {
  status: PatientStatus
  progress: Int
  currentPhase: ID
  notes: String
}
```

---

### Form Types

```graphql
type Form {
  id: ID!
  title: String!
  description: String
  carepathId: ID
  carepath: Carepath
  sections: [FormSection!]!
  organizationId: ID!
  organization: Organization!
  metadata: FormMetadata!
  createdAt: DateTime!
  updatedAt: DateTime!
  createdBy: User!
  active: Boolean!
}

type FormSection {
  id: ID!
  title: String!
  order: Int!
  questions: [FormQuestion!]!
}

type FormQuestion {
  id: ID!
  type: QuestionType!
  label: String!
  required: Boolean!
  options: [String!]
  validation: QuestionValidation
  conditionalDisplay: ConditionalDisplay
}

enum QuestionType {
  TEXT
  NUMBER
  SELECT
  MULTISELECT
  DATE
  CHECKBOX
  RADIO
}

type QuestionValidation {
  min: Int
  max: Int
  pattern: String
}

type ConditionalDisplay {
  questionId: ID!
  operator: ConditionalOperator!
  value: JSON!
}

enum ConditionalOperator {
  EQUALS
  CONTAINS
  GREATER
  LESS
}

type FormMetadata {
  version: Int!
  submissionCount: Int!
  averageCompletionTime: Int!
}

type FormSubmission {
  id: ID!
  formId: ID!
  form: Form!
  patientId: ID!
  patient: Patient!
  carepathId: ID
  responses: [FormResponse!]!
  status: SubmissionStatus!
  submittedAt: DateTime
  submittedBy: User!
  reviewedAt: DateTime
  reviewedBy: User
  reviewNotes: String
  organizationId: ID!
  triggeredLabels: [TriggeredLabel!]
}

enum SubmissionStatus {
  DRAFT
  PENDING
  APPROVED
  REJECTED
}

type FormResponse {
  questionId: ID!
  value: JSON!
  answeredAt: DateTime!
}

type TriggeredLabel {
  labelId: ID!
  questionId: ID!
  value: JSON!
}

input CreateFormInput {
  title: String!
  description: String
  carepathId: ID
  sections: [FormSectionInput!]!
  organizationId: ID!
}

input FormSectionInput {
  title: String!
  order: Int!
  questions: [FormQuestionInput!]!
}

input FormQuestionInput {
  type: QuestionType!
  label: String!
  required: Boolean!
  options: [String!]
  validation: QuestionValidationInput
  conditionalDisplay: ConditionalDisplayInput
}

input QuestionValidationInput {
  min: Int
  max: Int
  pattern: String
}

input ConditionalDisplayInput {
  questionId: ID!
  operator: ConditionalOperator!
  value: JSON!
}

input UpdateFormInput {
  title: String
  description: String
  sections: [FormSectionInput!]
  active: Boolean
}

input SubmitFormInput {
  formId: ID!
  patientId: ID!
  carepathId: ID
  responses: [FormResponseInput!]!
}

input FormResponseInput {
  questionId: ID!
  value: JSON!
}

input ReviewFormSubmissionInput {
  submissionId: ID!
  status: SubmissionStatus!
  reviewNotes: String
}
```

---

### Alert Types

```graphql
type Alert {
  id: ID!
  patientId: ID!
  patient: Patient!
  carepathId: ID
  type: AlertType!
  severity: AlertSeverity!
  title: String!
  description: String!
  status: AlertStatus!
  assignedTo: [User!]
  createdAt: DateTime!
  acknowledgedAt: DateTime
  acknowledgedBy: User
  resolvedAt: DateTime
  resolvedBy: User
  metadata: JSON
  organizationId: ID!
}

enum AlertType {
  VITAL_SIGNS
  MEDICATION
  APPOINTMENT
  LAB_RESULTS
  CUSTOM
}

enum AlertSeverity {
  LOW
  MEDIUM
  HIGH
  CRITICAL
}

enum AlertStatus {
  PENDING
  ACKNOWLEDGED
  RESOLVED
  DISMISSED
}

input CreateAlertInput {
  patientId: ID!
  carepathId: ID
  type: AlertType!
  severity: AlertSeverity!
  title: String!
  description: String!
  assignedToIds: [ID!]
  metadata: JSON
}

input UpdateAlertInput {
  status: AlertStatus
  assignedToIds: [ID!]
}

input AlertFilterInput {
  patientId: ID
  severity: AlertSeverity
  status: AlertStatus
  assignedToUserId: ID
  organizationId: ID
}
```

---

### Message Types

```graphql
type ChatTopic {
  id: ID!
  title: String!
  type: ChatType!
  participants: [ChatParticipant!]!
  patientId: ID
  patient: Patient
  carepathId: ID
  lastMessageAt: DateTime
  lastMessagePreview: String
  unreadCount: JSON!
  organizationId: ID!
  createdAt: DateTime!
  createdBy: User!
  archived: Boolean!
  archivedAt: DateTime
  messages: [Message!]!
}

enum ChatType {
  DIRECT
  GROUP
  PATIENT_CARE
}

type ChatParticipant {
  userId: ID!
  user: User!
  role: String!
  joinedAt: DateTime!
}

type Message {
  id: ID!
  topicId: ID!
  topic: ChatTopic!
  senderId: ID!
  sender: User!
  senderName: String!
  senderRole: String!
  content: String!
  attachments: [MessageAttachment!]
  replyTo: ID
  replyToMessage: Message
  reactions: [MessageReaction!]
  createdAt: DateTime!
  editedAt: DateTime
  deletedAt: DateTime
  read: Boolean!
  readBy: [ID!]!
}

type MessageAttachment {
  id: ID!
  name: String!
  url: String!
  type: String!
  size: Int!
}

type MessageReaction {
  userId: ID!
  emoji: String!
}

input CreateChatTopicInput {
  title: String!
  type: ChatType!
  participantUserIds: [ID!]!
  patientId: ID
  carepathId: ID
}

input SendMessageInput {
  topicId: ID!
  content: String!
  attachments: [MessageAttachmentInput!]
  replyToId: ID
}

input MessageAttachmentInput {
  name: String!
  url: String!
  type: String!
  size: Int!
}

input AddReactionInput {
  messageId: ID!
  emoji: String!
}
```

---

### Label & Note Types

```graphql
type PatientLabel {
  id: ID!
  text: String!
  color: LabelColor!
  triggeredBy: LabelTrigger!
  navigationUrl: String
  active: Boolean!
  dismissedAt: DateTime
  dismissedBy: User
}

enum LabelColor {
  RED
  YELLOW
  BLUE
  GREEN
  PURPLE
  ORANGE
}

type LabelTrigger {
  questionId: ID!
  questionLabel: String!
  responseValue: JSON!
  formSubmissionId: ID!
  carepathName: String!
  triggeredAt: DateTime!
}

type PatientNote {
  id: ID!
  content: String!
  type: NoteType!
  authorId: ID!
  author: User!
  authorName: String!
  authorRole: String!
  carepathId: ID
  attachments: [NoteAttachment!]
  tags: [String!]
  createdAt: DateTime!
  updatedAt: DateTime
  private: Boolean!
}

enum NoteType {
  CLINICAL
  NURSING
  ADMINISTRATIVE
}

type NoteAttachment {
  id: ID!
  name: String!
  url: String!
}

input CreatePatientNoteInput {
  patientId: ID!
  content: String!
  type: NoteType!
  carepathId: ID
  tags: [String!]
  private: Boolean
}

input UpdatePatientNoteInput {
  content: String
  tags: [String!]
  private: Boolean
}
```

---

### Analytics Types

```graphql
type DashboardMetrics {
  pendingApprovals: Int!
  activeCarepaths: Int!
  unreadMessages: Int!
  carepathTemplates: Int!
  totalPatients: Int!
  criticalAlerts: Int!
}

type CarepathStatistics {
  carepathId: ID!
  carepathName: String!
  total: Int!
  inProgress: Int!
  awaitingApproval: Int!
  completed: Int!
  onHold: Int!
  averageProgress: Float!
  averageCompletionTime: Int
}

type OrganizationStatistics {
  totalPatients: Int!
  activePatients: Int!
  totalCarepaths: Int!
  activeCarepaths: Int!
  totalForms: Int!
  pendingSubmissions: Int!
  totalAlerts: Int!
  criticalAlerts: Int!
  averagePatientProgress: Float!
}
```

---

## Query Definitions

```graphql
type Query {
  # User queries
  me: User!
  user(id: ID!): User
  users(organizationId: ID, role: UserRole): [User!]!
  
  # Organization queries
  organization(id: ID!): Organization
  organizations: [Organization!]!
  
  # Patient queries
  patient(id: ID!): Patient
  patients(filter: PatientFilterInput, limit: Int, offset: Int): [Patient!]!
  searchPatients(searchTerm: String!, limit: Int): [Patient!]!
  
  # Carepath queries
  carepath(id: ID!): Carepath
  carepaths(organizationId: ID, isTemplate: Boolean): [Carepath!]!
  carepathTemplates(category: String): [Carepath!]!
  patientCarepath(patientId: ID!, carepathId: ID!): PatientCarepath
  patientCarepaths(patientId: ID!): [PatientCarepath!]!
  
  # Form queries
  form(id: ID!): Form
  forms(organizationId: ID, carepathId: ID): [Form!]!
  formSubmission(id: ID!): FormSubmission
  formSubmissions(
    formId: ID
    patientId: ID
    status: SubmissionStatus
    limit: Int
    offset: Int
  ): [FormSubmission!]!
  
  # Alert queries
  alert(id: ID!): Alert
  alerts(filter: AlertFilterInput, limit: Int, offset: Int): [Alert!]!
  
  # Message queries
  chatTopic(id: ID!): ChatTopic
  chatTopics(userId: ID, patientId: ID, archived: Boolean): [ChatTopic!]!
  messages(topicId: ID!, limit: Int, offset: Int): [Message!]!
  
  # Label & Note queries
  patientLabels(patientId: ID!): [PatientLabel!]!
  patientNotes(patientId: ID!, carepathId: ID): [PatientNote!]!
  
  # Analytics queries
  dashboardMetrics: DashboardMetrics!
  carepathStatistics(carepathId: ID!): CarepathStatistics!
  organizationStatistics(organizationId: ID!): OrganizationStatistics!
}
```

---

## Mutation Definitions

```graphql
type Mutation {
  # User mutations
  createUser(input: CreateUserInput!): User!
  updateUser(id: ID!, input: UpdateUserInput!): User!
  deleteUser(id: ID!): Boolean!
  
  # Organization mutations
  createOrganization(input: CreateOrganizationInput!): Organization!
  updateOrganization(id: ID!, input: UpdateOrganizationInput!): Organization!
  
  # Patient mutations
  createPatient(input: CreatePatientInput!): Patient!
  updatePatient(id: ID!, input: UpdatePatientInput!): Patient!
  deletePatient(id: ID!): Boolean!
  
  # Carepath mutations
  createCarepath(input: CreateCarepathInput!): Carepath!
  updateCarepath(id: ID!, input: UpdateCarepathInput!): Carepath!
  deleteCarepath(id: ID!): Boolean!
  assignCarepathToPatient(input: AssignCarepathInput!): PatientCarepath!
  updatePatientCarepath(
    patientId: ID!
    carepathId: ID!
    input: UpdatePatientCarepathInput!
  ): PatientCarepath!
  removePatientCarepath(patientId: ID!, carepathId: ID!): Boolean!
  
  # Form mutations
  createForm(input: CreateFormInput!): Form!
  updateForm(id: ID!, input: UpdateFormInput!): Form!
  deleteForm(id: ID!): Boolean!
  submitForm(input: SubmitFormInput!): FormSubmission!
  reviewFormSubmission(input: ReviewFormSubmissionInput!): FormSubmission!
  
  # Alert mutations
  createAlert(input: CreateAlertInput!): Alert!
  updateAlert(id: ID!, input: UpdateAlertInput!): Alert!
  acknowledgeAlert(id: ID!): Alert!
  resolveAlert(id: ID!): Alert!
  dismissAlert(id: ID!): Alert!
  
  # Message mutations
  createChatTopic(input: CreateChatTopicInput!): ChatTopic!
  sendMessage(input: SendMessageInput!): Message!
  editMessage(id: ID!, content: String!): Message!
  deleteMessage(id: ID!): Boolean!
  addReaction(input: AddReactionInput!): Message!
  removeReaction(messageId: ID!, emoji: String!): Message!
  markMessageAsRead(messageId: ID!): Message!
  archiveChatTopic(topicId: ID!): ChatTopic!
  
  # Label & Note mutations
  dismissPatientLabel(patientId: ID!, labelId: ID!): PatientLabel!
  createPatientNote(input: CreatePatientNoteInput!): PatientNote!
  updatePatientNote(id: ID!, input: UpdatePatientNoteInput!): PatientNote!
  deletePatientNote(id: ID!): Boolean!
}
```

---

## Subscription Definitions

```graphql
type Subscription {
  # Patient subscriptions
  patientUpdated(patientId: ID!): Patient!
  patientCreated(organizationId: ID!): Patient!
  
  # Alert subscriptions
  alertCreated(organizationId: ID, patientId: ID): Alert!
  alertUpdated(alertId: ID!): Alert!
  
  # Message subscriptions
  messageReceived(topicId: ID!): Message!
  chatTopicUpdated(topicId: ID!): ChatTopic!
  
  # Form subscriptions
  formSubmissionCreated(formId: ID, patientId: ID): FormSubmission!
  formSubmissionReviewed(submissionId: ID!): FormSubmission!
}
```

---

## Error Handling

```graphql
type Error {
  message: String!
  code: String!
  field: String
}

type MutationResponse {
  success: Boolean!
  message: String
  errors: [Error!]
}
```

---

## Authentication

### JWT Token Structure

```typescript
interface JWTPayload {
  userId: string;
  email: string;
  role: UserRole;
  organizationId: string;
  iat: number;
  exp: number;
}
```

### Authentication Header

```
Authorization: Bearer <JWT_TOKEN>
```

---

## Rate Limiting

- **Anonymous users**: 100 requests per hour
- **Authenticated users**: 1000 requests per hour
- **Admin users**: 5000 requests per hour

## API Versioning

Current version: `v1`

Endpoint: `/graphql/v1`
