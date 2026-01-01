---
title: Patient Detail
description: 'Comprehensive patient profile with tabbed navigation'
icon: 'user'
---

# Patient Detail

Comprehensive patient profile view with tabbed navigation for managing all aspects of patient care including forms, messages, appointments, medications, and tasks.

## Overview

The Patient Detail page provides a complete view of an individual patient's information, care status, and interactions. It uses a tabbed interface to organize different aspects of patient management while maintaining context about the patient throughout navigation.

## Features

### Patient Header
- Patient name and demographics
- Profile photo/avatar
- Risk score badge with trend
- Care pathway progress indicator
- Quick action buttons (Message, Schedule, Edit)

### Tab Navigation
Six main tabs for comprehensive patient management:

1. **Overview Tab**
   - Patient demographics
   - Care pathway progress
   - Recent activity timeline
   - Health summary cards
   - Assigned care team

2. **Forms Tab**
   - Pending questionnaires
   - Completed forms history
   - Form submission status
   - Revision requests

3. **Messages Tab**
   - Secure messaging thread
   - Message history
   - Attachment support
   - Read receipts

4. **Appointments Tab**
   - Upcoming appointments
   - Past visit history
   - Appointment scheduling
   - Telehealth links

5. **Medications Tab**
   - Current medications list
   - Medication history
   - Dosage information
   - Refill status

6. **Tasks Tab**
   - Assigned tasks
   - Task completion tracking
   - Due date management
   - Task notes

### Health Chart
- Visual representation of health metrics
- Trend analysis over time
- Configurable date ranges
- Multiple metric overlays

## Use Cases

### UC-PD-001: Review Patient Overview
**Actor**: Healthcare Provider  
**Description**: Provider reviews patient's overall status and recent activity.

**Flow**:
1. Provider navigates to patient from list
2. Overview tab loads by default
3. Provider reviews care pathway progress
4. Provider checks recent activity timeline
5. Provider identifies any pending items

### UC-PD-002: Complete Form Review
**Actor**: Healthcare Provider  
**Description**: Provider reviews and approves patient-submitted form.

**Flow**:
1. Provider navigates to Forms tab
2. Selects pending form submission
3. Reviews form responses
4. Approves form or requests revision
5. Patient is notified of decision

### UC-PD-003: Send Patient Message
**Actor**: Healthcare Provider  
**Description**: Provider sends secure message to patient.

**Flow**:
1. Provider navigates to Messages tab
2. Types message in composer
3. Optionally attaches files
4. Sends message
5. Message appears in thread

### UC-PD-004: Schedule Appointment
**Actor**: Healthcare Provider  
**Description**: Provider schedules appointment for patient.

**Flow**:
1. Provider navigates to Appointments tab
2. Clicks "Schedule Appointment"
3. Selects appointment type
4. Chooses date and time
5. Confirms appointment
6. Patient receives notification

### UC-PD-005: Review Medications
**Actor**: Healthcare Provider  
**Description**: Provider reviews patient's current medications.

**Flow**:
1. Provider navigates to Medications tab
2. Reviews current medication list
3. Checks for interactions or concerns
4. Updates medication if needed
5. Documents any changes

## User Stories

### US-PD-001
**As a** healthcare provider  
**I want to** see a patient's complete profile  
**So that** I have full context for care decisions

**Acceptance Criteria**:
- [ ] Patient header shows key demographics
- [ ] Risk score is prominently displayed
- [ ] Care pathway progress is visible
- [ ] Navigation between tabs is seamless

### US-PD-002
**As a** healthcare provider  
**I want to** review and approve patient forms  
**So that** I can track care pathway completion

**Acceptance Criteria**:
- [ ] Pending forms are highlighted
- [ ] Form responses are clearly displayed
- [ ] Approve/Revise actions are available
- [ ] Revision comments can be added

### US-PD-003
**As a** healthcare provider  
**I want to** communicate securely with patients  
**So that** I can provide care guidance

**Acceptance Criteria**:
- [ ] Message thread shows full history
- [ ] New messages are highlighted
- [ ] File attachments are supported
- [ ] Messages are encrypted

### US-PD-004
**As a** healthcare provider  
**I want to** view patient's health trends  
**So that** I can monitor their progress

**Acceptance Criteria**:
- [ ] Health chart displays key metrics
- [ ] Date range is configurable
- [ ] Multiple metrics can be compared
- [ ] Trend direction is indicated

### US-PD-005
**As a** healthcare provider  
**I want to** manage patient tasks  
**So that** I can track care activities

**Acceptance Criteria**:
- [ ] Tasks show due dates
- [ ] Completion status is trackable
- [ ] Tasks can be assigned to team members
- [ ] Overdue tasks are highlighted

## Component Dependencies

```
PatientDetailComponent
├── PatientNavComponent
├── PatientFormsComponent
│   └── QuestionnaireReviewComponent
├── PatientMessagesComponent
│   └── ChatThreadComponent
├── PatientAppointmentsComponent
│   └── AppointmentFormComponent
├── PatientMedicationsComponent
├── PatientTasksComponent
└── PatientHealthChartComponent
```

## Data Flow

```
┌─────────────────┐
│  Route Params   │
│  (patient ID)   │
└────────┬────────┘
         │
         ▼
┌─────────────────┐     ┌──────────────────┐
│  PatientService │────▶│                  │
└─────────────────┘     │                  │
┌─────────────────┐     │  PatientDetail   │
│  FormService    │────▶│   Component      │
└─────────────────┘     │                  │
┌─────────────────┐     │                  │
│  ChatService    │────▶│                  │
└─────────────────┘     └────────┬─────────┘
┌─────────────────┐              │
│ AppointmentSvc  │──────────────┘
└─────────────────┘
```

## Technical Notes

- Patient data is loaded once and shared across tabs
- Tab content is lazy-loaded for performance
- Messages use WebSocket for real-time updates
- Health chart uses Chart.js for visualization
- Form review supports inline editing
- Responsive layout stacks tabs on mobile
