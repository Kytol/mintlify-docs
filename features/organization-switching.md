---
title: Organization Switching
description: Multi-facility support for healthcare systems
---

# Organization Switching

The Organization Switching feature enables users to work across multiple healthcare facilities, departments, and care units within a single platform instance.

## Overview

Healthcare systems often span multiple locations and organizational units. This feature allows providers to switch context between different facilities while maintaining a unified experience.

<Info>
The selected organization is displayed in the sidebar and persists across sessions.
</Info>

## Key Features

<CardGroup cols={2}>
  <Card title="Multi-Facility Support" icon="hospital">
    Work across hospitals, departments, and care units
  </Card>
  <Card title="Real-time Updates" icon="rotate">
    Changes reflect immediately throughout the application
  </Card>
  <Card title="Persistent Selection" icon="floppy-disk">
    Organization choice saved to localStorage
  </Card>
  <Card title="Context Awareness" icon="building">
    Current organization always visible in sidebar
  </Card>
</CardGroup>

## Available Organization Types

| Type | Description | Example |
|------|-------------|---------|
| Hospital | Main healthcare facility | St. Mary's Hospital |
| Department | Specialized medical department | Cardiology Department |
| Care Unit | Specific care area | ICU Care Unit |

## How to Switch Organizations

<Steps>
  <Step title="Open Settings">
    Navigate to the Settings page from the sidebar
  </Step>
  <Step title="Find Organization Section">
    Locate the "Organization" section in the settings panel
  </Step>
  <Step title="Select Organization">
    Choose your desired organization from the dropdown menu
  </Step>
  <Step title="Review Details">
    Verify the organization details (type, address, phone)
  </Step>
  <Step title="Save Changes">
    Click "Save Organization" to apply your selection
  </Step>
</Steps>

## User Interface

### Settings Panel

The organization selector displays:
- Dropdown with all available organizations
- Organization type badge
- Address and contact information
- Save button with confirmation feedback

### Sidebar Display

After selection, the sidebar shows:
- Organization name below the app title
- Organization type label (Hospital/Department/Care Unit)
- Updates in real-time when changed

## Default Organizations

The platform includes these pre-configured organizations:

<AccordionGroup>
  <Accordion title="St. Mary's Hospital" icon="hospital">
    **Type:** Hospital  
    Primary healthcare facility serving as the main organizational unit.
  </Accordion>
  <Accordion title="Cardiology Department" icon="heart-pulse">
    **Type:** Department  
    Specialized department for cardiac care and monitoring.
  </Accordion>
  <Accordion title="ICU Care Unit" icon="bed-pulse">
    **Type:** Care Unit  
    Intensive care unit for critical patient monitoring.
  </Accordion>
  <Accordion title="Emergency Department" icon="truck-medical">
    **Type:** Department  
    Emergency services and urgent care.
  </Accordion>
  <Accordion title="Pediatric Care Unit" icon="baby">
    **Type:** Care Unit  
    Specialized care for pediatric patients.
  </Accordion>
</AccordionGroup>

## Use Cases

### Multi-Location Providers

Providers working at multiple facilities can quickly switch context:
- Morning shift at St. Mary's Hospital
- Afternoon consultations at Cardiology Department
- On-call coverage for ICU Care Unit

### Department Transfers

When patients transfer between departments:
1. Switch to receiving department
2. Access department-specific workflows
3. View relevant patient cohorts

### Administrative Oversight

Administrators can review operations across facilities:
- Monitor metrics per organization
- Compare performance across units
- Manage organization-specific settings

## Data Behavior

<Warning>
Organization switching affects the data context. Patient lists and metrics may vary based on the selected organization.
</Warning>

### What Changes
- Patient list filtering
- Dashboard metrics
- Available care pathways
- Team member visibility

### What Persists
- User profile settings
- Personal preferences
- Notification settings
- Theme selection

## Best Practices

1. **Verify Selection**: Always confirm the correct organization before patient interactions
2. **Check Sidebar**: The sidebar displays current organization for quick reference
3. **Consistent Context**: Complete tasks within one organization before switching
4. **Session Awareness**: Remember that selection persists across browser sessions
