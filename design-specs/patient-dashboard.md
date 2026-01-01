---
title: Patient Dashboard
description: 'Patient-facing self-service portal for care journey management'
icon: 'mobile'
---

# Patient Dashboard

Patient-facing self-service portal providing patients with access to their care journey, forms, messages, appointments, medications, and health observations.

## Overview

The Patient Dashboard is a dedicated view designed for patients to interact with their healthcare journey. It provides a simplified, patient-friendly interface for completing forms, communicating with care teams, viewing appointments, and tracking health progress. This view is accessed through a "View as Patient" feature or patient portal login.

## Features

### Patient View Banner
- Visual indicator showing patient view mode
- Patient name display
- Exit button to return to provider view

### Dashboard Tab
- **Care Journey Progress**: Visual timeline of care pathway steps
- **Quick Actions**: 
  - Complete pending forms
  - Continue tasks
  - Message care team
  - View appointments
  - Access health resources
  - Report bugs/issues
- **Progress Bar**: Overall care pathway completion percentage

### Forms Tab
- List of pending questionnaires
- Completed forms history
- Form completion interface
- Submission status tracking

### Tasks Tab
- Assigned patient tasks
- Task completion tracking
- Due date visibility
- Task instructions

### Messages Tab
- Secure messaging with care team
- Message history
- Attachment support
- Notification indicators

### Appointments Tab
- Upcoming appointments list
- Past visit history
- Appointment details (type, provider, location)
- Telehealth access links

### Medications Tab
- Current medications list
- Dosage instructions
- Refill information
- Medication schedule

### Health Tab
- **Data View**: Tabular display of health observations
  - Weight tracking
  - Blood pressure readings
  - Pain level assessments
  - Lab values (PSA, etc.)
- **Graph View**: Visual charts showing trends
  - Interactive data points
  - Trend indicators
  - Normal range highlighting

## Use Cases

### UC-PDash-001: Complete Questionnaire
**Actor**: Patient  
**Description**: Patient completes a required questionnaire as part of their care pathway.

**Flow**:
1. Patient logs into patient portal
2. Sees pending forms notification on dashboard
3. Clicks "Complete Forms" quick action
4. Navigates to Forms tab
5. Selects pending questionnaire
6. Completes all questions
7. Submits questionnaire
8. Receives confirmation

### UC-PDash-002: Message Care Team
**Actor**: Patient  
**Description**: Patient sends a question to their care team.

**Flow**:
1. Patient navigates to Messages tab
2. Types message in composer
3. Optionally attaches relevant files
4. Sends message
5. Receives confirmation
6. Awaits care team response

### UC-PDash-003: View Upcoming Appointments
**Actor**: Patient  
**Description**: Patient checks their scheduled appointments.

**Flow**:
1. Patient navigates to Appointments tab
2. Views list of upcoming appointments
3. Clicks on appointment for details
4. Notes date, time, location, and provider
5. Accesses telehealth link if applicable

### UC-PDash-004: Track Health Progress
**Actor**: Patient  
**Description**: Patient reviews their health metrics over time.

**Flow**:
1. Patient navigates to Health tab
2. Toggles between Data and Graph views
3. Reviews weight, blood pressure, pain levels
4. Observes trends and improvements
5. Notes any concerns to discuss with provider

### UC-PDash-005: Report Issue
**Actor**: Patient  
**Description**: Patient reports a bug or issue with the application.

**Flow**:
1. Patient clicks "Report a Bug" on dashboard
2. Bug report modal opens
3. Patient describes the issue
4. Optionally attaches screenshots
5. Submits report
6. Receives confirmation

## User Stories

### US-PDash-001
**As a** patient  
**I want to** see my care journey progress  
**So that** I understand where I am in my treatment

**Acceptance Criteria**:
- [ ] Care pathway steps are displayed as timeline
- [ ] Completed steps show checkmarks
- [ ] Current step is highlighted
- [ ] Locked steps show lock icon
- [ ] Overall progress percentage is visible

### US-PDash-002
**As a** patient  
**I want to** complete required forms online  
**So that** I can participate in my care from home

**Acceptance Criteria**:
- [ ] Pending forms count is visible
- [ ] Forms are easy to navigate
- [ ] Progress is saved automatically
- [ ] Submission confirmation is shown

### US-PDash-003
**As a** patient  
**I want to** message my care team securely  
**So that** I can ask questions between appointments

**Acceptance Criteria**:
- [ ] Message interface is intuitive
- [ ] Previous messages are visible
- [ ] Unread message count is shown
- [ ] Attachments can be added

### US-PDash-004
**As a** patient  
**I want to** view my health trends  
**So that** I can see my progress over time

**Acceptance Criteria**:
- [ ] Health data is displayed clearly
- [ ] Graphs show trends visually
- [ ] Normal ranges are indicated
- [ ] Data can be toggled between views

### US-PDash-005
**As a** patient  
**I want to** see my upcoming appointments  
**So that** I can prepare and attend on time

**Acceptance Criteria**:
- [ ] Appointments show date, time, provider
- [ ] Telehealth links are accessible
- [ ] Past appointments are viewable
- [ ] Appointment type is indicated

## Component Dependencies

```
PatientDashboardComponent
├── PatientNavComponent
├── PatientFormsComponent
│   └── PatientFormCompletionComponent
├── PatientTasksComponent
├── PatientMessagesComponent
├── PatientAppointmentsComponent
├── PatientMedicationsComponent
└── ReportBugModalComponent
```

## Data Flow

```
┌─────────────────┐     ┌──────────────────┐
│ ViewModeService │────▶│                  │
└─────────────────┘     │                  │
┌─────────────────┐     │  PatientDashboard │
│  PatientService │────▶│    Component     │
└─────────────────┘     │                  │
┌─────────────────┐     │                  │
│ CarepathService │────▶│                  │
└─────────────────┘     └────────┬─────────┘
┌─────────────────┐              │
│  FormService    │──────────────┘
└─────────────────┘
```

## Technical Notes

- ViewModeService manages patient view state
- Patient context is maintained across tab navigation
- Health observations include mock data for demonstration
- Graph view uses SVG for responsive charts
- Forms support auto-save functionality
- Mobile-optimized for patient access on phones
