---
title: Pending Approvals
description: Review and approve patient form submissions
---

# Pending Approvals

The Pending Approvals feature provides a centralized queue for reviewing patient questionnaire submissions that require clinical approval before processing.

## Overview

When patients complete questionnaires through their carepath, submissions enter the approval queue. Care team members review responses and either approve them or request revisions.

<Info>
Submissions are automatically prioritized based on waiting time to ensure timely review.
</Info>

## Priority System

<CardGroup cols={3}>
  <Card title="Urgent" icon="circle-exclamation">
    48+ hours waiting (Red, pulsing)
  </Card>
  <Card title="High" icon="triangle-exclamation">
    24-48 hours waiting (Amber)
  </Card>
  <Card title="Normal" icon="circle">
    Less than 24 hours (Gray)
  </Card>
</CardGroup>

| Priority | Wait Time | Visual Indicator |
|----------|-----------|------------------|
| Urgent | 48+ hours | Red badge, pulsing animation |
| High | 24-48 hours | Amber badge |
| Normal | < 24 hours | Gray badge |

## User Interface

### Header
- Back navigation
- Pending count badge
- Bulk action buttons (when items selected)

### Filter Bar

| Control | Function |
|---------|----------|
| Search | Find by form title or patient name |
| Priority Filter | All, Urgent, High, Normal |
| Sort Options | Date, Priority, Title, Patient |
| Sort Direction | Ascending/Descending toggle |

### Priority Summary

Quick counts showing distribution:
- Urgent submissions count
- High priority count
- Normal priority count

## Submission Cards

Each pending item displays:

| Element | Description |
|---------|-------------|
| Checkbox | For bulk selection |
| Avatar | Patient initials |
| Form Title | With type badge |
| Patient Name | Clickable to profile |
| Timestamp | Relative and exact time |
| Priority Badge | Color-coded indicator |
| Actions | Approve, Revise, Details |

### Expandable Details

Click expand to view:
- Form preview (first 3 questions/answers)
- Submission metadata (IDs, waiting time)
- "View Full Details" button

## Actions

<Tabs>
  <Tab title="Individual">
    <Steps>
      <Step title="Approve">
        Accept submission and process into patient record
      </Step>
      <Step title="Request Revision">
        Send back to patient with feedback
      </Step>
      <Step title="View Details">
        See complete submission with all responses
      </Step>
    </Steps>
  </Tab>
  <Tab title="Bulk">
    Select multiple submissions to:
    - Approve all selected
    - Clear selection
    
    <Warning>
    Bulk approve only routine submissions. Review complex cases individually.
    </Warning>
  </Tab>
</Tabs>

## Filtering

### Search
Real-time search across:
- Form titles
- Patient names

### Priority Filter

| Button | Shows |
|--------|-------|
| All | All priorities |
| Urgent | Only urgent items |
| High | Only high priority |
| Normal | Only normal priority |

### Sorting

| Sort By | Description |
|---------|-------------|
| Submitted Date | When form was submitted |
| Priority Level | Urgency ranking |
| Form Title | Alphabetical by form |
| Patient Name | Alphabetical by patient |

## Pagination

| Control | Options |
|---------|---------|
| Page Size | 5, 10, 25, 50 items |
| Navigation | Previous/Next buttons |
| Display | "Showing X-Y of Z" |

## Empty States

<Tabs>
  <Tab title="No Matches">
    When filters return no results:
    - Search icon
    - "No forms match your filters" message
    - Clear filters button
  </Tab>
  <Tab title="All Done">
    When queue is empty:
    - Checkmark icon
    - "No forms pending approval" message
    - Confirmation that you're caught up
  </Tab>
</Tabs>

## Workflow

**Approval Flow:** Patient Submits → Queue Entry → Priority Assigned → Review → Decision (Approve → Process OR Revise → Return to Patient)

<Steps>
  <Step title="Patient Submits">
    Questionnaire completed in carepath
  </Step>
  <Step title="Queue Entry">
    Submission appears in pending list
  </Step>
  <Step title="Priority Assignment">
    Auto-calculated from wait time
  </Step>
  <Step title="Review">
    Care team member examines responses
  </Step>
  <Step title="Decision">
    Approve or request revision
  </Step>
  <Step title="Processing">
    Approved submissions update patient record
  </Step>
</Steps>

## Integration Points

<AccordionGroup>
  <Accordion title="Carepaths" icon="route">
    Submissions originate from carepath questionnaires. Approval advances patient through their care journey.
  </Accordion>
  <Accordion title="Patient Profile" icon="user">
    View patient context before approving. Click patient name to open profile.
  </Accordion>
  <Accordion title="Alerts" icon="bell">
    Urgent submissions may trigger notifications to ensure timely review.
  </Accordion>
  <Accordion title="Analytics" icon="chart-line">
    Approval times and volumes tracked in analytics dashboard.
  </Accordion>
</AccordionGroup>

## Best Practices

<Tip>
**Monitor Urgent** - Address urgent items first to prevent delays
</Tip>

<Tip>
**Regular Review** - Check queue multiple times daily
</Tip>

<Tip>
**Bulk Processing** - Use bulk approve for routine submissions
</Tip>

<Tip>
**Clear Feedback** - When requesting revision, explain what's needed
</Tip>

<Tip>
**Patient Context** - Review patient profile for complex submissions
</Tip>
