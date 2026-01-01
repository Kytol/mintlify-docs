---
title: Patients List
description: 'Patient directory with search, filtering, and risk indicators'
icon: 'users'
---

# Patients List

The patient directory view providing comprehensive patient management with advanced filtering, search, and risk-based prioritization.

## Overview

The Patients List is the primary interface for healthcare providers to view, search, and manage their patient population. It features advanced filtering capabilities, risk score indicators, and quick actions for efficient patient management.

## Features

### Patient Table
- Sortable columns (Name, Status, Risk Level, Last Activity, Progress)
- Pagination with configurable page size
- Row selection for bulk actions
- Quick view hover cards

### Search & Filtering
- **Global Search**: Search by patient name, ID, or condition
- **Status Filter**: Active, Inactive, Pending, Discharged
- **Risk Level Filter**: Critical, High, Moderate, Low
- **Care Pathway Filter**: Filter by assigned pathway
- **Date Range Filter**: Filter by last activity or registration date

### Risk Indicators
- Color-coded risk badges (Red: Critical, Orange: High, Yellow: Moderate, Green: Low)
- Risk score numerical display
- Trend indicators (improving, stable, declining)

### Quick Actions
- View patient details
- Send message
- Schedule appointment
- Assign care pathway
- Export patient list

### Bulk Operations
- Select multiple patients
- Bulk message sending
- Bulk care pathway assignment
- Export selected patients

## Use Cases

### UC-PAT-001: Find Patient by Name
**Actor**: Healthcare Provider  
**Description**: Provider searches for a specific patient by name.

**Flow**:
1. Provider navigates to Patients List
2. Types patient name in search field
3. Results filter in real-time
4. Provider clicks on patient row
5. Navigates to Patient Detail page

### UC-PAT-002: Review High-Risk Patients
**Actor**: Healthcare Provider  
**Description**: Provider reviews all high-risk patients for prioritization.

**Flow**:
1. Provider navigates to Patients List
2. Selects "High" and "Critical" from risk filter
3. Sorts by risk score descending
4. Reviews each patient's status
5. Takes action on priority patients

### UC-PAT-003: Add New Patient
**Actor**: Healthcare Provider  
**Description**: Provider registers a new patient in the system.

**Flow**:
1. Provider clicks "Add Patient" button
2. Patient form modal opens
3. Provider enters patient demographics
4. Provider assigns initial care pathway (optional)
5. Provider saves patient record
6. New patient appears in list

### UC-PAT-004: Export Patient Report
**Actor**: Healthcare Administrator  
**Description**: Administrator exports patient list for reporting.

**Flow**:
1. Administrator applies desired filters
2. Clicks "Export" button
3. Selects export format (CSV, Excel, PDF)
4. Downloads generated report

## User Stories

### US-PAT-001
**As a** healthcare provider  
**I want to** search for patients by name or ID  
**So that** I can quickly find specific patient records

**Acceptance Criteria**:
- [ ] Search field is prominently displayed
- [ ] Search results update as user types (debounced)
- [ ] Search matches partial names
- [ ] No results state shows helpful message

### US-PAT-002
**As a** healthcare provider  
**I want to** filter patients by risk level  
**So that** I can prioritize high-risk patients

**Acceptance Criteria**:
- [ ] Risk level filter dropdown is available
- [ ] Multiple risk levels can be selected
- [ ] Filter persists during session
- [ ] Clear filter option is available

### US-PAT-003
**As a** healthcare provider  
**I want to** see patient risk scores at a glance  
**So that** I can quickly identify patients needing attention

**Acceptance Criteria**:
- [ ] Risk badge is visible for each patient
- [ ] Color coding matches risk severity
- [ ] Trend indicator shows risk direction
- [ ] Clicking risk badge shows details

### US-PAT-004
**As a** healthcare provider  
**I want to** add new patients to the system  
**So that** I can begin managing their care

**Acceptance Criteria**:
- [ ] Add Patient button is visible
- [ ] Form validates required fields
- [ ] Duplicate patient warning is shown
- [ ] Success confirmation is displayed

### US-PAT-005
**As a** healthcare provider  
**I want to** sort patients by various criteria  
**So that** I can organize my patient list effectively

**Acceptance Criteria**:
- [ ] Column headers are clickable for sorting
- [ ] Sort direction indicator is visible
- [ ] Sort persists during session
- [ ] Default sort is configurable

## Component Dependencies

```
PatientsListComponent
├── FilterBarComponent
├── PatientFormComponent (modal)
├── RiskBadgeComponent
├── PaginationComponent
└── ExportMenuComponent
```

## Data Flow

```
┌─────────────────┐     ┌──────────────────┐     ┌─────────────────┐
│  PatientService │────▶│  PatientsListComponent │────▶│  Patient Detail │
└─────────────────┘     └──────────────────┘     └─────────────────┘
         │                       │
         │              ┌────────┴────────┐
         │              │                 │
         ▼              ▼                 ▼
┌─────────────────┐  ┌──────────┐  ┌──────────────┐
│ RiskScoringService │  │ FilterBar │  │ PatientForm  │
└─────────────────┘  └──────────┘  └──────────────┘
```

## Technical Notes

- Uses virtual scrolling for large patient lists (1000+ patients)
- Filters are applied client-side for small datasets, server-side for large
- Risk scores are calculated by RiskScoringService
- Patient data is cached and refreshed on interval
- Responsive design collapses columns on mobile
