---
title: Dashboard
description: 'Main landing page with overview widgets and quick actions'
icon: 'gauge'
---

# Dashboard

The main landing page providing healthcare providers with an at-a-glance overview of their patient population, recent activity, and quick access to common actions.

## Overview

The Dashboard serves as the central hub for healthcare providers, displaying key metrics, recent patient activity, and quick navigation to important features. It's designed to help providers quickly assess their workload and prioritize patient care.

## Features

### Welcome Banner
- Personalized greeting with user's name
- Current date display
- Organization context indicator
- Quick action buttons for common tasks

### Quick Stats Widget
Displays real-time metrics including:
- **Total Patients**: Count of patients in the provider's panel
- **Active Carepaths**: Number of ongoing care pathways
- **Pending Forms**: Forms awaiting review or completion
- **Unread Messages**: Count of unread patient messages
- **Upcoming Appointments**: Scheduled appointments for the day/week
- **Critical Alerts**: High-priority alerts requiring attention

### Activity Feed
Real-time feed showing recent events:
- New patient registrations
- Form submissions
- Message notifications
- Appointment updates
- Care pathway progress changes
- Alert triggers

### Navigation Cards
Quick access cards to main application sections:
- Patient Management
- Messages
- Care Pathways
- Alerts
- Analytics
- Settings

## Use Cases

### UC-DASH-001: Morning Review
**Actor**: Healthcare Provider  
**Description**: Provider reviews dashboard at start of shift to understand daily priorities.

**Flow**:
1. Provider logs into the application
2. Dashboard loads with current metrics
3. Provider reviews pending forms count
4. Provider checks critical alerts
5. Provider reviews activity feed for overnight events
6. Provider navigates to highest priority items

### UC-DASH-002: Quick Patient Access
**Actor**: Healthcare Provider  
**Description**: Provider needs to quickly access a specific patient's information.

**Flow**:
1. Provider uses global search from dashboard header
2. Types patient name or ID
3. Selects patient from search results
4. Navigates directly to patient detail page

### UC-DASH-003: Alert Response
**Actor**: Healthcare Provider  
**Description**: Provider responds to critical alert from dashboard.

**Flow**:
1. Provider sees critical alert indicator on dashboard
2. Clicks alert card or notification
3. Reviews alert details
4. Takes appropriate action (view patient, acknowledge, escalate)

## User Stories

### US-DASH-001
**As a** healthcare provider  
**I want to** see a summary of my patient panel status  
**So that** I can quickly prioritize my daily tasks

**Acceptance Criteria**:
- [ ] Dashboard displays total patient count
- [ ] Pending forms count is visible and clickable
- [ ] Unread messages count updates in real-time
- [ ] Critical alerts are prominently displayed

### US-DASH-002
**As a** healthcare provider  
**I want to** see recent patient activity  
**So that** I can stay informed about changes in my patient population

**Acceptance Criteria**:
- [ ] Activity feed shows last 10-20 events
- [ ] Each activity item shows timestamp
- [ ] Activities are categorized by type (form, message, alert, etc.)
- [ ] Clicking an activity navigates to relevant detail

### US-DASH-003
**As a** healthcare provider  
**I want to** quickly navigate to common tasks  
**So that** I can efficiently manage my workflow

**Acceptance Criteria**:
- [ ] Quick action buttons are visible above the fold
- [ ] Navigation cards provide clear visual hierarchy
- [ ] Keyboard shortcuts are available for power users

## Component Dependencies

```
DashboardComponent
├── WelcomeBannerComponent
├── QuickStatsWidgetComponent
├── ActivityFeedComponent
├── StatCardComponent
└── GlobalSearchComponent (header)
```

## Data Flow

```
┌─────────────────┐     ┌──────────────────┐
│  PatientService │────▶│                  │
└─────────────────┘     │                  │
┌─────────────────┐     │    Dashboard     │
│  FormService    │────▶│    Component     │
└─────────────────┘     │                  │
┌─────────────────┐     │                  │
│  ChatService    │────▶│                  │
└─────────────────┘     └────────┬─────────┘
┌─────────────────┐              │
│  AlertService   │──────────────┘
└─────────────────┘
```

## Technical Notes

- Component uses `OnPush` change detection for performance
- Stats are refreshed on component initialization and via subscriptions
- Activity feed uses virtual scrolling for large datasets
- Responsive layout adapts to mobile, tablet, and desktop viewports
