---
title: Patient Notes
description: Comprehensive documentation system for patient care
---

# Patient Notes

The Patient Notes feature provides a structured system for healthcare providers to document observations, concerns, and care-related information for each patient.

## Overview

Patient notes enable care teams to maintain detailed records of patient interactions, observations, and clinical decisions. Notes are categorized, prioritized, and attributed to specific nurses for accountability.

<Info>
Notes are visible as icons with count badges in the patients list for quick reference.
</Info>

## Key Features

<CardGroup cols={2}>
  <Card title="Categorized Notes" icon="folder">
    6 note types for organized documentation
  </Card>
  <Card title="Priority Levels" icon="flag">
    4 priority levels with color coding
  </Card>
  <Card title="Privacy Controls" icon="lock">
    Mark sensitive notes as private
  </Card>
  <Card title="Rich Metadata" icon="tags">
    Timestamps, attribution, and tagging
  </Card>
</CardGroup>

## Note Categories

<Tabs>
  <Tab title="General">
    **Color:** Blue  
    General patient information and observations not fitting other categories.
    
    **Examples:**
    - Family visit notes
    - Patient preferences
    - Communication observations
  </Tab>
  <Tab title="Medical">
    **Color:** Red  
    Medical conditions, treatments, and clinical observations.
    
    **Examples:**
    - Symptom changes
    - Treatment responses
    - Vital sign trends
  </Tab>
  <Tab title="Behavioral">
    **Color:** Purple  
    Behavioral observations and psychological concerns.
    
    **Examples:**
    - Mood changes
    - Anxiety observations
    - Compliance concerns
  </Tab>
  <Tab title="Medication">
    **Color:** Green  
    Medication-related notes and adjustments.
    
    **Examples:**
    - Dosage changes
    - Side effects
    - Administration notes
  </Tab>
  <Tab title="Discharge">
    **Color:** Orange  
    Discharge planning and coordination notes.
    
    **Examples:**
    - Discharge criteria
    - Home care instructions
    - Follow-up scheduling
  </Tab>
  <Tab title="Follow-up">
    **Color:** Yellow  
    Follow-up requirements and scheduling notes.
    
    **Examples:**
    - Appointment reminders
    - Test result follow-ups
    - Care plan reviews
  </Tab>
</Tabs>

## Priority Levels

| Priority | Color | Description |
|----------|-------|-------------|
| Low | Gray | Non-urgent information for reference |
| Normal | Blue | Standard priority documentation |
| High | Orange | Important, needs attention soon |
| Urgent | Red | Requires immediate attention |

## User Interface

### Patients List Integration

Notes are accessible directly from the patients list:
- **Notes Icon**: Clickable icon in the actions column
- **Count Badge**: Cyan badge showing number of notes
- **Tooltip**: Shows note count or "Click to add"
- **Hover Effects**: Visual feedback on interaction

### Notes Modal

Full-featured modal interface with:
- **Two-column Layout**: Notes list on left, form on right
- **Note Cards**: Rich display with metadata and styling
- **Statistics Panel**: Summary of note activity
- **Add Note Form**: Comprehensive creation interface

## Creating Notes

<Steps>
  <Step title="Open Notes Modal">
    Click the notes icon on any patient row
  </Step>
  <Step title="Fill Note Details">
    Enter title and content (both required)
  </Step>
  <Step title="Select Category">
    Choose appropriate note type from dropdown
  </Step>
  <Step title="Set Priority">
    Select priority level based on urgency
  </Step>
  <Step title="Privacy Setting">
    Toggle private if note is sensitive
  </Step>
  <Step title="Save Note">
    Click "Add Note" to save
  </Step>
</Steps>

### Note Fields

| Field | Required | Description |
|-------|----------|-------------|
| Title | Yes | Brief descriptive title |
| Content | Yes | Detailed note content |
| Type | Yes | Category selection |
| Priority | Yes | Urgency level |
| Private | No | Restrict visibility to nurses |

## Viewing Notes

### Note Display

Each note card shows:
- Title with priority badge
- Full content text
- Category indicator with color
- Nurse attribution
- Timestamp (relative, e.g., "2 hours ago")
- Tags (if any)

### Sorting

Notes are displayed in chronological order with newest first.

## Statistics Panel

The modal includes a statistics summary:

| Metric | Description |
|--------|-------------|
| Total Count | Overall number of notes |
| Recent Activity | Notes from last 7 days |
| High Priority | Count of high/urgent notes |
| Type Distribution | Breakdown by category |

## Privacy Controls

<Warning>
Private notes are only visible to nursing staff. Use this setting for sensitive information.
</Warning>

### When to Use Private Notes
- Sensitive behavioral observations
- Family dynamics concerns
- Confidential medical information
- Staff-only communications

## Sample Notes

The system includes realistic sample data:

| Patient | Type | Priority | Title |
|---------|------|----------|-------|
| P-001 | Medical | High | Blood Sugar Management |
| P-001 | General | Normal | Family Concerns |
| P-002 | Medication | High | Medication Adjustment |
| P-002 | Behavioral | Normal | Behavioral Observation (Private) |
| P-003 | Medical | Normal | Pain Management Update |
| P-004 | Discharge | High | Discharge Planning |
| P-005 | Follow-up | Urgent | Follow-up Required |

## Integration Points

### Patient Records
Notes are linked to patient profiles and accessible from:
- Patients list (via icon)
- Patient detail view
- Care team dashboard

### Audit Trail
Complete history maintained:
- Creation timestamps
- Nurse attribution
- Modification tracking

### Alerts
High-priority notes can trigger:
- Dashboard notifications
- Care team alerts
- Shift handoff highlights

## Best Practices

1. **Be Specific**: Use clear, descriptive titles
2. **Choose Correct Category**: Helps with filtering and reporting
3. **Set Appropriate Priority**: Reserve urgent for true emergencies
4. **Use Privacy Wisely**: Only mark private when necessary
5. **Document Timely**: Add notes promptly after observations
6. **Include Context**: Provide enough detail for other team members
7. **Use Tags**: Add relevant tags for searchability
