---
title: Shared Components
description: 'Reusable UI components catalog with usage examples'
icon: 'puzzle-piece'
---

# Shared Components

Reusable UI components that provide consistent functionality and styling across the application.

## Overview

The application uses a component-based architecture with shared components that encapsulate common UI patterns and functionality. These components promote consistency, reduce code duplication, and simplify maintenance.

## Component Catalog

### Navigation & Layout

#### PatientNavComponent
Tabbed navigation for patient detail views.

**Inputs**:
- `activeTab`: Current active tab ID
- `pendingFormsCount`: Badge count for forms tab
- `pendingTasksCount`: Badge count for tasks tab
- `unreadMessagesCount`: Badge count for messages tab

**Outputs**:
- `tabChange`: Emits when tab is selected

**Usage**:
```html
<app-patient-nav
  [activeTab]="activeTab"
  [pendingFormsCount]="3"
  (tabChange)="onTabChange($event)"
/>
```

---

### Data Display

#### RiskBadgeComponent
Displays patient risk level with color-coded badge.

**Inputs**:
- `riskLevel`: 'low' | 'moderate' | 'high' | 'critical'
- `score`: Numeric risk score (0-100)
- `showScore`: Whether to display numeric score
- `size`: 'sm' | 'md' | 'lg'

**Usage**:
```html
<app-risk-badge
  [riskLevel]="patient.riskLevel"
  [score]="patient.riskScore"
  [showScore]="true"
/>
```

---

#### QuickStatsWidgetComponent
Dashboard widget displaying key statistics with icons.

**Inputs**:
- `stats`: Array of stat objects with label, value, icon, trend

**Usage**:
```html
<app-quick-stats-widget [stats]="dashboardStats" />
```

---

#### CarepathTimelineComponent
Visual timeline showing care pathway progress.

**Inputs**:
- `steps`: Array of care pathway steps
- `currentStep`: ID of current active step
- `orientation`: 'horizontal' | 'vertical'

**Outputs**:
- `stepClick`: Emits when step is clicked

**Usage**:
```html
<app-carepath-timeline
  [steps]="carepathSteps"
  [currentStep]="activeStepId"
  (stepClick)="onStepClick($event)"
/>
```

---

#### PatientHealthChartComponent
Interactive health metrics chart with multiple data series.

**Inputs**:
- `patientId`: Patient identifier
- `metrics`: Array of metric types to display
- `dateRange`: Start and end dates

**Usage**:
```html
<app-patient-health-chart
  [patientId]="patient.id"
  [metrics]="['weight', 'bloodPressure']"
  [dateRange]="selectedRange"
/>
```

---

### Forms & Input

#### FilterBarComponent
Reusable filter bar with search, dropdowns, and date pickers.

**Inputs**:
- `filters`: Configuration array for filter controls
- `values`: Current filter values

**Outputs**:
- `filterChange`: Emits when any filter changes
- `reset`: Emits when filters are cleared

**Usage**:
```html
<app-filter-bar
  [filters]="filterConfig"
  [values]="currentFilters"
  (filterChange)="onFilterChange($event)"
/>
```

---

#### QuestionnaireFormComponent
Dynamic form renderer for questionnaires.

**Inputs**:
- `questionnaire`: Questionnaire definition
- `responses`: Existing responses (for editing)
- `readOnly`: Disable editing

**Outputs**:
- `submit`: Emits form responses on submission
- `save`: Emits for draft save

**Usage**:
```html
<app-questionnaire-form
  [questionnaire]="activeQuestionnaire"
  (submit)="onSubmit($event)"
/>
```

---

#### CarepathFormComponent
Form for creating/editing care pathways.

**Inputs**:
- `carepath`: Existing carepath for editing
- `mode`: 'create' | 'edit'

**Outputs**:
- `save`: Emits carepath data on save
- `cancel`: Emits on cancel

---

#### PatientFormCompletionComponent
Patient-facing form completion interface.

**Inputs**:
- `formId`: Form identifier
- `patientId`: Patient identifier

**Outputs**:
- `complete`: Emits on form completion
- `back`: Emits on back navigation

---

### Communication

#### ChatTopicsComponent
List of chat topics/conversations.

**Inputs**:
- `topics`: Array of chat topics
- `selectedTopicId`: Currently selected topic

**Outputs**:
- `topicSelect`: Emits when topic is selected
- `newTopic`: Emits when new topic requested

**Usage**:
```html
<app-chat-topics
  [topics]="chatTopics"
  [selectedTopicId]="activeTopicId"
  (topicSelect)="onTopicSelect($event)"
/>
```

---

#### ChatThreadComponent
Message thread display with composer.

**Inputs**:
- `messages`: Array of messages
- `currentUserId`: Current user for message alignment

**Outputs**:
- `sendMessage`: Emits new message content
- `attachFile`: Emits file attachment

---

#### PatientMessagesComponent
Complete messaging interface for patient context.

**Inputs**:
- `patientId`: Patient identifier

---

### Modals & Overlays

#### ToastComponent
Toast notification display.

**Inputs**:
- `message`: Notification message
- `type`: 'success' | 'error' | 'warning' | 'info'
- `duration`: Auto-dismiss duration in ms

**Usage**: Typically used via ToastService:
```typescript
this.toastService.success('Patient saved successfully');
```

---

#### RiskConfigModalComponent
Modal for configuring risk scoring thresholds.

**Inputs**:
- `config`: Current risk configuration
- `isOpen`: Modal visibility state

**Outputs**:
- `save`: Emits updated configuration
- `close`: Emits on modal close

---

#### ReportBugModalComponent
Bug reporting modal for user feedback.

**Inputs**:
- `isOpen`: Modal visibility state

**Outputs**:
- `submit`: Emits bug report data
- `close`: Emits on modal close

---

### Patient Management

#### PatientFormsComponent
Patient forms list and management.

**Inputs**:
- `patientId`: Patient identifier

**Outputs**:
- `formSelected`: Emits when form is selected

---

#### PatientTasksComponent
Patient tasks list and completion tracking.

**Inputs**:
- `patientId`: Patient identifier

**Outputs**:
- `taskSelected`: Emits when task is selected

---

#### PatientAppointmentsComponent
Patient appointments list and scheduling.

**Inputs**:
- `patientId`: Patient identifier

---

#### PatientMedicationsComponent
Patient medications list and management.

**Inputs**:
- `patientId`: Patient identifier

---

### Review & Display

#### QuestionnaireResponseDisplayComponent
Read-only display of questionnaire responses.

**Inputs**:
- `responses`: Array of question responses
- `questionnaire`: Questionnaire definition

---

#### ResponseCardComponent
Card display for individual response item.

**Inputs**:
- `response`: Response data
- `question`: Question definition

---

#### FormReviewCardComponent
Card for form review with approval actions.

**Inputs**:
- `form`: Form submission data
- `showActions`: Whether to show approve/reject

**Outputs**:
- `approve`: Emits on approval
- `reject`: Emits on rejection
- `viewDetails`: Emits on view details click

---

#### NurseQuestionnaireReviewComponent
Specialized review interface for clinical staff.

**Inputs**:
- `responseId`: Questionnaire response ID
- `patientId`: Patient identifier

**Outputs**:
- `approve`: Emits on approval
- `requestRevision`: Emits revision request

---

## Component Guidelines

### Styling
- All components use CSS custom properties for theming
- Tailwind CSS utility classes for layout
- BEM-style class naming for custom styles

### Accessibility
- ARIA labels on interactive elements
- Keyboard navigation support
- Focus management in modals
- Screen reader announcements

### Performance
- OnPush change detection where applicable
- Lazy loading for heavy components
- Virtual scrolling for long lists

### Testing
- Unit tests for component logic
- Integration tests for component interactions
- Accessibility audits
