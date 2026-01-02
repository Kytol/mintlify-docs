---
title: Dashboard
description: Central hub for healthcare platform overview and quick actions
---

# Dashboard

The Dashboard provides a comprehensive overview of the healthcare platform, displaying key metrics, upcoming tasks, and quick access to common actions.

## Overview

The dashboard serves as the home screen for healthcare providers, offering at-a-glance insights into patient care activities and easy navigation to frequently used features.

<Info>
The dashboard updates in real-time to reflect the latest patient data and system activity.
</Info>

## Components

### Welcome Banner

Personalized greeting with:
- User name
- Current date and time
- Contextual information about the session

### Quick Stats Widget

<CardGroup cols={4}>
  <Card title="Total Patients" icon="users">
    All patients in the system
  </Card>
  <Card title="Pending Alerts" icon="bell">
    Alerts requiring attention
  </Card>
  <Card title="Completion Rate" icon="chart-pie">
    Care pathway progress
  </Card>
  <Card title="Response Time" icon="clock">
    Average response metrics
  </Card>
</CardGroup>

### Metric Widgets

Six clickable cards showing real-time counts:

| Widget | Description | Navigation |
|--------|-------------|------------|
| Pending Approvals | Forms awaiting review | `/pending-approvals` |
| Active Carepaths | Patients on care pathways | `/carepaths` |
| Unread Messages | New patient messages | `/messages` |
| Templates | Available carepath templates | `/carepaths` |
| Questionnaires | Form templates | `/questionnaires` |
| Alerts | Active alerts | `/alerts` |

## Quick Actions

<Tabs>
  <Tab title="Patient Actions">
    | Action | Description |
    |--------|-------------|
    | Add Patient | Register a new patient |
    | Appointment | Schedule an appointment |
    | Messages | View inbox |
  </Tab>
  <Tab title="Clinical Actions">
    | Action | Description |
    |--------|-------------|
    | New Carepath | Create a carepath template |
    | Questionnaire | Create a new form |
    | Review Pending | Go to approval queue |
  </Tab>
  <Tab title="Admin Actions">
    | Action | Description |
    |--------|-------------|
    | Analytics | View insights |
    | Report Bug | Submit feedback |
  </Tab>
</Tabs>

## Upcoming Tasks

Scrollable list of scheduled tasks with:

| Element | Description |
|---------|-------------|
| Task Title | Name of the task |
| Patient Name | Associated patient |
| Due Time | Relative or absolute time |
| Priority | High/Medium/Low indicator |
| Type Badge | Appointment, followup, medication, assessment |

### Task Actions

Click any task to open action modal:

<Steps>
  <Step title="View Patient">
    Navigate to patient profile
  </Step>
  <Step title="Mark Complete">
    Close task as done
  </Step>
  <Step title="Reschedule">
    Change task timing
  </Step>
  <Step title="Cancel Task">
    Remove from queue
  </Step>
</Steps>

## Activity Feed

Real-time feed showing recent platform activity:

- Patient updates
- Form submissions
- Alert triggers
- System events

<Info>
Activity feed updates automatically without page refresh.
</Info>

## Modal Forms

Quick actions open modal forms for:

| Modal | Purpose |
|-------|---------|
| Carepath Template | Create new care pathway |
| Questionnaire | Build patient forms |
| New Patient | Register patient |
| Appointment | Schedule visit |
| Bug Report | Submit feedback |

## Navigation

Dashboard widgets provide quick navigation:

- **Metric Cards**: Click to go to that section
- **Quick Actions**: Open relevant pages or modals
- **Task Items**: Link to patient profiles
- **Activity Items**: Navigate to related records

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `G` then `D` | Go to Dashboard |
| `G` then `P` | Go to Patients |
| `G` then `M` | Go to Messages |
| `?` | Show all shortcuts |

## Best Practices

<Check>
**Morning Review**: Check dashboard at shift start for overview
</Check>

<Check>
**Priority First**: Address high-priority tasks before routine items
</Check>

<Check>
**Monitor Approvals**: Keep pending approvals count low
</Check>

<Check>
**Activity Awareness**: Review activity feed for recent changes
</Check>

## Customization

The dashboard adapts to user role:

| Role | Visible Widgets |
|------|-----------------|
| Nurse | All clinical widgets |
| Provider | Clinical + analytics |
| Admin | All widgets + settings |

## Performance

Dashboard optimizations:
- Lazy loading of widgets
- Cached metric calculations
- Incremental activity feed updates
- Responsive design for all devices
