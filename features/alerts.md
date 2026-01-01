---
title: Alerts System
description: Monitor and respond to patient threshold alerts
---

# Alerts System

The Alerts feature provides real-time monitoring of patient health data, triggering notifications when values exceed configured thresholds.

## Overview

Alerts are generated automatically when patient questionnaire responses or health metrics cross predefined thresholds. The system enables care teams to quickly identify and respond to patients requiring attention.

## Alert Properties

### Severity Levels
- **Critical**: Immediate attention required (red indicator)
- **High**: Urgent review needed (orange indicator)
- **Medium**: Monitor closely (yellow indicator)
- **Low**: Informational (blue indicator)

### Status States
- **Pending**: New alert awaiting review
- **Acknowledged**: Alert seen by care team member
- **Resolved**: Alert addressed and closed

## User Interface

### Statistics Bar
Quick-filter buttons showing counts for:
- Pending alerts (with pulse animation)
- Acknowledged alerts
- Resolved alerts

### Severity Filters
Filter alerts by severity level with count badges.

### View Modes
- **Table View**: Detailed list with sortable columns
- **Card View**: Visual cards grouped by patient

## Alert Information

Each alert displays:
- Patient name and identifier
- Alert message describing the trigger
- Questionnaire source
- Threshold comparison (actual vs. threshold value)
- Timestamp with relative time
- Current status with handler attribution

## Actions

### Individual Actions
- **Acknowledge**: Mark alert as seen (adds timestamp and user)
- **Resolve**: Close alert as addressed
- **View Patient**: Navigate to patient profile

### Bulk Actions
Select multiple alerts to:
- Acknowledge all selected
- Resolve all selected

## Threshold Display

Alerts show the triggering condition:

```
Response Value [operator] Threshold Value
Example: 8 greater than 5 (Pain score exceeded threshold)
```

Supported operators:
- Greater than `>`
- Less than `<`
- Equal to `=`
- Greater than or equal `>=`
- Less than or equal `<=`

## Sorting Options

Sort alerts by:
- Severity (critical first)
- Patient name
- Status
- Triggered time

## Pagination

Configure display with:
- 5, 10, 25, or 50 alerts per page
- Page navigation controls
- Results count display

## Workflow

1. **Alert Triggered**: System detects threshold breach
2. **Review**: Care team sees alert in pending list
3. **Acknowledge**: Team member marks alert as seen
4. **Action**: Appropriate intervention taken
5. **Resolve**: Alert closed with optional notes

## Integration

- **Questionnaires**: Alerts generated from form responses
- **Risk Scoring**: High-risk patients may generate more alerts
- **Patient Dashboard**: View patient-specific alert history
