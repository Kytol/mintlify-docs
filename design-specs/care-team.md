---
title: Care Team Dashboard
description: 'Team collaboration platform for care coordination'
icon: 'people-group'
---

# Care Team Dashboard

Comprehensive team collaboration platform for coordinating care, managing workloads, communicating, and scheduling across healthcare team members.

## Overview

The Care Team Dashboard is a multi-functional collaboration hub designed for healthcare teams. It provides real-time team status, task management, patient assignments, risk monitoring, internal messaging, calendar scheduling, and team settings. The dashboard uses a tabbed interface to organize different aspects of team coordination.

## Features

### Header Section
- Live clock display
- Global search across team, tasks, and messages
- Team online status indicator
- Pending tasks counter
- Notifications dropdown
- Quick actions button

### Tab Navigation
Six main tabs with keyboard shortcuts (⌘1-6):

1. **Dashboard Tab**
   - Welcome banner with daily summary
   - Quick stats with sparkline trends
   - Team status panel with filters
   - Priority tasks panel (List/Board views)
   - Activity feed
   - Shift schedule overview

2. **Patients Tab**
   - Assigned patients by team member
   - Patient workload distribution
   - Quick patient actions
   - Assignment management

3. **Risk Tab**
   - Team's high-risk patients
   - Risk interventions tracking
   - Escalation management
   - Risk trend monitoring

4. **Messages Tab**
   - Team channels
   - Direct messages
   - Channel creation
   - Message search

5. **Calendar Tab**
   - Team schedule view
   - Shift management
   - Time-off requests
   - Event creation

6. **Settings Tab**
   - Team preferences
   - Notification settings
   - Role management
   - Integration settings

### Team Status Panel
- Real-time member status (Available, Busy, Offline)
- Workload indicators with progress bars
- Role-based avatars
- Quick message action
- Filter by status

### Task Management
- **List View**: Priority-sorted task list with checkboxes
- **Board View**: Kanban-style columns by priority
- Task details (patient, assignee, due date)
- Overdue highlighting
- Quick task creation

### Activity Feed
- Real-time team activity stream
- Activity types (tasks, messages, shifts, patients, alerts)
- Timestamp display
- User attribution

### Notifications System
- Unread notification badge
- Notification dropdown
- Mark all as read
- Notification categories

## Use Cases

### UC-CT-001: Morning Team Huddle
**Actor**: Care Team Lead  
**Description**: Team lead reviews team status for morning huddle.

**Flow**:
1. Lead opens Care Team Dashboard
2. Reviews team online status
3. Checks pending tasks count
4. Reviews high-priority tasks
5. Notes any critical patient alerts
6. Conducts team huddle with information

### UC-CT-002: Assign Task to Team Member
**Actor**: Healthcare Provider  
**Description**: Provider assigns a patient task to team member.

**Flow**:
1. Provider clicks "Quick Task" button
2. Enters task details
3. Selects patient
4. Assigns to team member
5. Sets priority and due date
6. Creates task
7. Assignee receives notification

### UC-CT-003: Review Team Workload
**Actor**: Care Team Lead  
**Description**: Lead reviews and balances team workload.

**Flow**:
1. Lead views Team Status panel
2. Reviews workload percentages
3. Identifies overloaded members
4. Navigates to Patients tab
5. Reassigns patients as needed
6. Workload rebalances

### UC-CT-004: Team Communication
**Actor**: Healthcare Provider  
**Description**: Provider sends message to team channel.

**Flow**:
1. Provider navigates to Messages tab
2. Selects team channel
3. Types message
4. Sends to channel
5. Team members receive notification

### UC-CT-005: Schedule Management
**Actor**: Care Team Lead  
**Description**: Lead manages team shift schedule.

**Flow**:
1. Lead navigates to Calendar tab
2. Views current shift schedule
3. Reviews time-off requests
4. Adjusts shifts as needed
5. Publishes updated schedule
6. Team members notified

## User Stories

### US-CT-001
**As a** care team member  
**I want to** see my team's status  
**So that** I know who's available for collaboration

**Acceptance Criteria**:
- [ ] Team members listed with status
- [ ] Status updates in real-time
- [ ] Quick message action available
- [ ] Workload visible for each member

### US-CT-002
**As a** care team member  
**I want to** manage my tasks  
**So that** I can track my work

**Acceptance Criteria**:
- [ ] Tasks show priority and due date
- [ ] Tasks can be marked complete
- [ ] Overdue tasks are highlighted
- [ ] Tasks can be filtered and sorted

### US-CT-003
**As a** care team lead  
**I want to** monitor team workload  
**So that** I can balance assignments

**Acceptance Criteria**:
- [ ] Workload percentage shown
- [ ] Visual indicators for overload
- [ ] Patient counts per member
- [ ] Reassignment is easy

### US-CT-004
**As a** care team member  
**I want to** communicate with my team  
**So that** I can coordinate care

**Acceptance Criteria**:
- [ ] Team channels available
- [ ] Direct messaging supported
- [ ] Unread indicators shown
- [ ] Search across messages

### US-CT-005
**As a** care team member  
**I want to** view team schedule  
**So that** I know shift coverage

**Acceptance Criteria**:
- [ ] Calendar shows all shifts
- [ ] My shifts are highlighted
- [ ] Time-off requests visible
- [ ] Schedule changes notified

## Component Dependencies

```
CareTeamDashboardComponent
├── TeamStatusPanelComponent
├── TasksPanelComponent
│   ├── TaskListViewComponent
│   └── TaskBoardViewComponent
├── ActivityFeedComponent
├── PatientsTabComponent
├── RiskTabComponent
├── MessagesTabComponent
│   └── ChannelListComponent
├── CalendarTabComponent
│   └── ShiftScheduleComponent
├── SettingsTabComponent
└── NotificationsDropdownComponent
```

## Data Flow

```
┌─────────────────┐     ┌──────────────────┐
│CareTeamService  │────▶│                  │
└─────────────────┘     │                  │
         │              │   CareTeam       │
         │              │   Dashboard      │
         ▼              │                  │
┌─────────────────┐     │                  │
│  WebSocket      │────▶│                  │
│  (Real-time)    │     └────────┬─────────┘
└─────────────────┘              │
                        ┌────────┼────────┐
                        │        │        │
                        ▼        ▼        ▼
                 ┌──────────┐ ┌─────┐ ┌────────┐
                 │TeamStatus│ │Tasks│ │Calendar│
                 └──────────┘ └─────┘ └────────┘
```

## Technical Notes

- Real-time updates via WebSocket for team status
- Keyboard shortcuts for tab navigation (⌘1-6)
- View mode toggle (Grid/List) persists in session
- Task board supports drag-and-drop
- Calendar integrates with external calendar systems
- Notifications use browser notification API
- Mobile-responsive for on-the-go access
- Role-based access controls for settings
