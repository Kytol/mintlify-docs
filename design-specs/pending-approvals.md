---
title: Pending Approvals
description: 'Workflow management for form and questionnaire approvals'
icon: 'clipboard-check'
---

# Pending Approvals

Workflow management page for reviewing and approving patient-submitted forms and questionnaires.

## Overview

The Pending Approvals page provides healthcare providers with a centralized location to review, approve, or request revisions for patient-submitted forms. It streamlines the approval workflow for questionnaires that are part of care pathways, ensuring timely review and patient progression through their care journey.

## Features

### Approvals Table
- List of all pending form submissions
- Form title and type
- Patient name with link to profile
- Submission date
- Status indicator
- Action buttons

### Quick Actions
- **Approve**: Approve form and advance patient in pathway
- **Request Revision**: Send form back to patient with feedback
- **View Details**: Open full form review interface

### Navigation
- Back button to return to dashboard
- Patient name links to patient detail
- Pending count badge

### Empty State
- Friendly message when no approvals pending
- Visual indicator of completion

## Use Cases

### UC-PA-001: Approve Form Submission
**Actor**: Healthcare Provider  
**Description**: Provider reviews and approves a patient's form submission.

**Flow**:
1. Provider navigates to Pending Approvals
2. Reviews list of pending forms
3. Clicks "View Details" on form
4. Reviews patient responses
5. Clicks "Approve"
6. Form status updates
7. Patient advances in care pathway
8. Patient receives notification

### UC-PA-002: Request Form Revision
**Actor**: Healthcare Provider  
**Description**: Provider requests patient to revise incomplete form.

**Flow**:
1. Provider reviews form submission
2. Identifies incomplete or incorrect responses
3. Clicks "Request Revision"
4. Enters revision feedback
5. Form sent back to patient
6. Patient notified of revision request
7. Form reappears in pending when resubmitted

### UC-PA-003: Batch Review Forms
**Actor**: Healthcare Provider  
**Description**: Provider reviews multiple pending forms efficiently.

**Flow**:
1. Provider opens Pending Approvals
2. Sees count of pending forms
3. Reviews forms in order
4. Approves or requests revision for each
5. Pending count decreases
6. Continues until queue cleared

### UC-PA-004: Navigate to Patient Context
**Actor**: Healthcare Provider  
**Description**: Provider needs more context about patient before approval.

**Flow**:
1. Provider sees pending form
2. Clicks patient name link
3. Navigates to patient detail
4. Reviews patient history
5. Returns to pending approvals
6. Makes informed approval decision

## User Stories

### US-PA-001
**As a** healthcare provider  
**I want to** see all pending form approvals  
**So that** I can review them efficiently

**Acceptance Criteria**:
- [ ] All pending forms listed
- [ ] Form title clearly visible
- [ ] Patient name shown
- [ ] Submission date displayed
- [ ] Pending count in header

### US-PA-002
**As a** healthcare provider  
**I want to** approve forms quickly  
**So that** patients can progress in their care

**Acceptance Criteria**:
- [ ] Approve button is prominent
- [ ] Approval is one-click
- [ ] Success confirmation shown
- [ ] Form removed from pending list

### US-PA-003
**As a** healthcare provider  
**I want to** request form revisions  
**So that** I can get complete information

**Acceptance Criteria**:
- [ ] Request Revision button available
- [ ] Feedback can be provided
- [ ] Patient is notified
- [ ] Form status updates

### US-PA-004
**As a** healthcare provider  
**I want to** view form details  
**So that** I can review responses thoroughly

**Acceptance Criteria**:
- [ ] View Details opens full form
- [ ] All responses visible
- [ ] Questionnaire context shown
- [ ] Approval actions available

### US-PA-005
**As a** healthcare provider  
**I want to** navigate to patient profile  
**So that** I can review context before approval

**Acceptance Criteria**:
- [ ] Patient name is clickable
- [ ] Links to patient detail
- [ ] Easy return to approvals
- [ ] Context preserved

## Component Dependencies

```
PendingApprovalsComponent
├── ApprovalsTableComponent
└── QuestionnaireReviewComponent (via navigation)
```

## Data Flow

```
┌─────────────────┐     ┌──────────────────┐
│  FormService    │────▶│                  │
└─────────────────┘     │                  │
         │              │ PendingApprovals │
         │              │   Component      │
         ▼              │                  │
┌─────────────────┐     │                  │
│ PatientService  │────▶│                  │
└─────────────────┘     └────────┬─────────┘
                                 │
                                 ▼
                        ┌──────────────────┐
                        │QuestionnaireReview│
                        │   (navigation)   │
                        └──────────────────┘
```

## Workflow States

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│  Submitted  │────▶│   Pending   │────▶│  Approved   │
└─────────────┘     └──────┬──────┘     └─────────────┘
                           │
                           ▼
                   ┌─────────────┐
                   │  Revision   │
                   │  Requested  │
                   └──────┬──────┘
                          │
                          ▼
                   ┌─────────────┐
                   │ Resubmitted │
                   └─────────────┘
```

## Technical Notes

- Pending forms fetched from FormService
- Patient names cached for performance
- Approval triggers care pathway advancement
- Revision requests include feedback mechanism
- Toast notifications for action confirmation
- Navigation preserves source context
- Responsive table for mobile access
