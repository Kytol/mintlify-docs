---
title: Care Pathways
description: 'Care pathway management for structured treatment protocols'
icon: 'route'
---

# Care Pathways

Care pathway management system for creating, assigning, and tracking structured treatment protocols for patients.

## Overview

The Care Pathways page enables healthcare providers to manage standardized care protocols. Care pathways define a sequence of steps, questionnaires, and milestones that guide patient treatment. Providers can create custom pathways, assign them to patients, and monitor progress through the care journey.

## Features

### Pathway List
- Grid/List view toggle
- Pathway cards with summary info
- Patient count per pathway
- Completion rate statistics
- Quick actions (Edit, Duplicate, Archive)

### Pathway Details
- Step-by-step pathway visualization
- Step configuration (questionnaires, tasks, milestones)
- Estimated duration per step
- Dependencies between steps
- Branching logic support

### Pathway Builder
- Drag-and-drop step ordering
- Step type selection (Form, Task, Milestone, Wait)
- Questionnaire assignment to steps
- Conditional logic configuration
- Preview mode

### Patient Assignment
- Assign pathway to patient
- Bulk assignment capability
- Start date configuration
- Pathway customization per patient

### Progress Tracking
- Visual timeline of patient progress
- Step completion status
- Time spent per step
- Bottleneck identification

## Use Cases

### UC-CP-001: Create New Pathway
**Actor**: Healthcare Administrator  
**Description**: Administrator creates a new care pathway for a condition.

**Flow**:
1. Administrator clicks "Create Pathway"
2. Enters pathway name and description
3. Adds steps using pathway builder
4. Configures questionnaires for each step
5. Sets step dependencies
6. Saves and publishes pathway
7. Pathway available for assignment

### UC-CP-002: Assign Pathway to Patient
**Actor**: Healthcare Provider  
**Description**: Provider assigns a care pathway to a new patient.

**Flow**:
1. Provider navigates to patient detail
2. Clicks "Assign Pathway"
3. Selects appropriate pathway
4. Configures start date
5. Confirms assignment
6. Patient receives first step

### UC-CP-003: Monitor Pathway Progress
**Actor**: Healthcare Provider  
**Description**: Provider monitors patient progress through pathway.

**Flow**:
1. Provider views pathway dashboard
2. Sees patients at each step
3. Identifies patients stuck at steps
4. Reviews individual patient progress
5. Takes action on delayed patients

### UC-CP-004: Modify Existing Pathway
**Actor**: Healthcare Administrator  
**Description**: Administrator updates an existing pathway.

**Flow**:
1. Administrator selects pathway
2. Clicks "Edit"
3. Modifies steps or configuration
4. Saves changes
5. Chooses to apply to existing patients or new only

## User Stories

### US-CP-001
**As a** healthcare administrator  
**I want to** create care pathways  
**So that** I can standardize treatment protocols

**Acceptance Criteria**:
- [ ] Pathway builder is intuitive
- [ ] Multiple step types supported
- [ ] Questionnaires can be assigned
- [ ] Dependencies can be configured

### US-CP-002
**As a** healthcare provider  
**I want to** assign pathways to patients  
**So that** I can guide their treatment

**Acceptance Criteria**:
- [ ] Assignment is quick and easy
- [ ] Start date can be configured
- [ ] Patient is notified
- [ ] First step is activated

### US-CP-003
**As a** healthcare provider  
**I want to** track pathway progress  
**So that** I can ensure patients complete treatment

**Acceptance Criteria**:
- [ ] Progress is visually displayed
- [ ] Completion percentage shown
- [ ] Stuck patients are highlighted
- [ ] Time at each step is tracked

### US-CP-004
**As a** healthcare administrator  
**I want to** view pathway analytics  
**So that** I can optimize care protocols

**Acceptance Criteria**:
- [ ] Completion rates are shown
- [ ] Average time per step displayed
- [ ] Bottlenecks are identified
- [ ] Comparison between pathways available

### US-CP-005
**As a** healthcare provider  
**I want to** see pathway timeline  
**So that** I can visualize patient journey

**Acceptance Criteria**:
- [ ] Timeline shows all steps
- [ ] Completed steps are marked
- [ ] Current step is highlighted
- [ ] Future steps show estimates

## Component Dependencies

```
CarepathsListComponent
├── CarepathCardComponent
├── CarepathFormComponent (modal)
├── CarepathTimelineComponent
└── CarepathBuilderComponent
    ├── StepConfigComponent
    └── QuestionnaireSelectComponent
```

## Data Flow

```
┌─────────────────┐     ┌──────────────────┐
│CarepathService  │────▶│                  │
└─────────────────┘     │                  │
         │              │   Carepaths      │
         │              │    Component     │
         ▼              │                  │
┌─────────────────┐     │                  │
│QuestionnaireService│──▶│                  │
└─────────────────┘     └────────┬─────────┘
                                 │
                        ┌────────┴────────┐
                        │                 │
                        ▼                 ▼
                 ┌──────────┐      ┌──────────┐
                 │PathwayList│     │PathwayForm│
                 └──────────┘      └──────────┘
```

## Technical Notes

- Pathways support branching logic for complex protocols
- Step completion triggers next step activation
- Questionnaire responses stored with step context
- Pathway templates can be shared across organizations
- Version control for pathway modifications
- Analytics track pathway effectiveness
