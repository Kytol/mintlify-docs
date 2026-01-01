---
title: Pending Approvals
description: Review and approve patient form submissions
---

# Pending Approvals

The Pending Approvals feature provides a centralized queue for reviewing patient questionnaire submissions that require clinical approval before processing.

## Overview

When patients complete questionnaires through their carepath, submissions enter the approval queue. Care team members review responses and either approve them or request revisions.

## Priority System

Submissions are automatically prioritized based on waiting time:

| Priority | Wait Time | Indicator |
|----------|-----------|-----------|
| Urgent | 48+ hours | Red badge, pulsing |
| High | 24-48 hours | Amber badge |
| Normal | < 24 hours | Gray badge |

## User Interface

### Header
- Back navigation
- Pending count badge
- Bulk action buttons (when items selected)

### Filter Bar
- **Search**: Find by form title or patient name
- **Priority Filter**: All, Urgent, High, Normal
- **Sort Options**: Submitted date, Priority, Form title, Patient name
- **Sort Direction**: Ascending/Descending toggle

### Priority Summary
Quick counts showing:
- Urgent submissions
- High priority submissions
- Normal priority submissions

## Submission Cards

Each pending item displays:
- Selection checkbox
- Patient avatar with initials
- Form title with type badge
- Patient name (clickable)
- Relative time and exact timestamp
- Priority badge
- Action buttons

### Expandable Details
Click expand to view:
- Form preview (first 3 questions/answers)
- Submission metadata (IDs, waiting time)
- "View Full Details" button

## Actions

### Individual Actions
- **Approve**: Accept submission and process
- **Request Revision**: Send back to patient with feedback
- **View Details**: See complete submission

### Bulk Actions
Select multiple submissions to:
- Approve all selected
- Clear selection

## Filtering

### Search
Real-time search across:
- Form titles
- Patient names

### Priority Filter
Toggle buttons for:
- All priorities
- Urgent only
- High only
- Normal only

### Sorting
Sort by:
- Submitted date (default)
- Priority level
- Form title
- Patient name

## Pagination

- Configurable page size (5, 10, 25, 50)
- Page navigation controls
- Results range display

## Empty States

### No Matching Filters
- Search icon
- "No forms match your filters" message
- Clear filters button

### All Caught Up
- Checkmark icon
- "No forms pending approval" message
- Confirmation that queue is empty

## Workflow

1. **Patient Submits**: Questionnaire completed in carepath
2. **Queue Entry**: Submission appears in pending list
3. **Priority Assignment**: Auto-calculated from wait time
4. **Review**: Care team member examines responses
5. **Decision**: Approve or request revision
6. **Processing**: Approved submissions update patient record

## Best Practices

1. **Monitor Urgent**: Address urgent items first
2. **Regular Review**: Check queue multiple times daily
3. **Bulk Processing**: Use bulk approve for routine submissions
4. **Patient Communication**: Explain revision requests clearly

## Integration

- **Carepaths**: Submissions originate from carepath questionnaires
- **Patient Profile**: View patient context before approving
- **Alerts**: Urgent submissions may trigger notifications
