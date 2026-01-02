---
title: Carepath Templates
description: Create and manage patient care journey templates
---

# Carepath Templates

The Carepath Templates feature enables healthcare teams to create, manage, and track structured patient care journeys. Templates define the steps patients follow through their treatment process.

## Overview

Carepaths provide a standardized approach to patient care by defining sequential steps that guide patients through their treatment journey. Each template can include questionnaires, tasks, and milestones.

<Info>
Carepaths ensure consistent care delivery across your organization while allowing flexibility for individual patient needs.
</Info>

## Key Features

<CardGroup cols={2}>
  <Card title="Template Management" icon="folder-open">
    Create, edit, duplicate, and organize templates
  </Card>
  <Card title="Version Control" icon="code-branch">
    Track changes with full version history
  </Card>
  <Card title="Step Types" icon="list-check">
    Questionnaires, tasks, and milestones
  </Card>
  <Card title="Patient Assignment" icon="user-plus">
    Assign and track patient progress
  </Card>
</CardGroup>

## Step Types

<Tabs>
  <Tab title="Questionnaire Steps">
    Embed forms for patient data collection at specific points in the care journey.
    
    **Use cases:**
    - Pre-operative assessments
    - Daily symptom tracking
    - Post-procedure follow-ups
  </Tab>
  <Tab title="Task Steps">
    Define actions for care team members to complete.
    
    **Use cases:**
    - Schedule appointments
    - Review lab results
    - Contact patient
  </Tab>
  <Tab title="Milestone Steps">
    Mark significant progress points in the care journey.
    
    **Use cases:**
    - Surgery completed
    - Discharge ready
    - Recovery milestone
  </Tab>
</Tabs>

## User Interface

### View Modes

| Mode | Description |
|------|-------------|
| Table View | Detailed list with sortable columns |
| Card View | Visual grid with template summaries |

### Statistics Dashboard

<CardGroup cols={4}>
  <Card title="Total Templates" icon="files">
    Count of all templates
  </Card>
  <Card title="Active Patients" icon="users">
    Patients on carepaths
  </Card>
  <Card title="Total Steps" icon="list">
    Steps across all templates
  </Card>
  <Card title="Avg Steps" icon="calculator">
    Average steps per template
  </Card>
</CardGroup>

## Template Actions

<Steps>
  <Step title="Create">
    Start a new template from scratch with the template builder
  </Step>
  <Step title="Edit">
    Modify template steps, settings, and metadata
  </Step>
  <Step title="Duplicate">
    Create a copy of an existing template for variations
  </Step>
  <Step title="Preview">
    View template as a patient would see it
  </Step>
  <Step title="Export/Import">
    Share templates as JSON files between systems
  </Step>
</Steps>

## Creating a Template

<Steps>
  <Step title="Basic Information">
    Enter template name and description
  </Step>
  <Step title="Add Steps">
    Add questionnaire, task, or milestone steps
  </Step>
  <Step title="Configure Steps">
    Set step details, requirements, and timing
  </Step>
  <Step title="Review">
    Preview the complete template
  </Step>
  <Step title="Save">
    Save and optionally assign to patients
  </Step>
</Steps>

### Step Configuration

| Field | Description |
|-------|-------------|
| Title | Step name displayed to patient |
| Description | Detailed instructions |
| Type | Questionnaire, Task, or Milestone |
| Required | Whether step must be completed |
| Duration | Expected time to complete |
| Dependencies | Previous steps that must be done first |

## Filtering & Search

### Search
Find templates by name or description using the search bar.

### Filters

| Filter | Options |
|--------|---------|
| Step Count | 1-3, 4-6, 7-10, 10+ |
| Patient Usage | With patients, Without patients |
| Status | Active, Draft, Archived |

## Version History

Every change to a template is tracked:

| Change Type | Description |
|-------------|-------------|
| `created` | Initial template creation |
| `updated` | General updates |
| `step_added` | New step added |
| `step_removed` | Step deleted |
| `step_modified` | Step settings changed |
| `reordered` | Step order changed |

### Version Information

Each version records:
- Version number (auto-incremented)
- Change description
- User who made the change
- Timestamp
- Previous/new values (for rollback)

## Bulk Operations

Select multiple templates to:
- Export selected templates together
- Delete multiple templates at once
- Archive templates

## Patient Assignment

### Assigning a Template

<Steps>
  <Step title="Select Template">
    Choose the appropriate carepath template
  </Step>
  <Step title="Select Patient">
    Choose patient(s) to assign
  </Step>
  <Step title="Set Start Date">
    Configure when the carepath begins
  </Step>
  <Step title="Confirm">
    Review and confirm assignment
  </Step>
</Steps>

### Tracking Progress

Monitor patient progress through:
- Step completion status
- Time spent on each step
- Questionnaire responses
- Task completion

## Integration Points

<AccordionGroup>
  <Accordion title="Patient Dashboard" icon="user">
    View patient's active carepath progress from their profile.
  </Accordion>
  <Accordion title="Pending Approvals" icon="clipboard-check">
    Review questionnaire submissions from carepath steps.
  </Accordion>
  <Accordion title="Alerts" icon="bell">
    Trigger alerts based on carepath questionnaire responses.
  </Accordion>
  <Accordion title="Analytics" icon="chart-line">
    Track carepath completion rates and outcomes.
  </Accordion>
</AccordionGroup>

## Best Practices

<Check>
**Start Simple**: Begin with essential steps, add complexity as needed
</Check>

<Check>
**Use Questionnaires**: Collect structured data at key points
</Check>

<Check>
**Version Control**: Document changes when updating templates
</Check>

<Check>
**Monitor Usage**: Review patient statistics to optimize templates
</Check>

<Warning>
Avoid creating overly complex carepaths. Patients are more likely to complete shorter, focused journeys.
</Warning>

## Example Templates

| Template | Steps | Use Case |
|----------|-------|----------|
| Pre-Surgery Prep | 5 | Surgical preparation checklist |
| Post-Op Recovery | 8 | Post-operative monitoring |
| Chronic Care | 12 | Ongoing condition management |
| New Patient Onboarding | 4 | Initial patient setup |
