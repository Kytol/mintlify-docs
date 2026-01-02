---
title: Features Overview
description: Documentation for implemented features in the Healthcare Platform
icon: 'sparkles'
---

# Features

This section documents the key features implemented in the Healthcare Platform application.

<Info>
Each feature page includes detailed usage instructions, UI components, and best practices.
</Info>

## Core Features

<CardGroup cols={2}>
  <Card title="Dashboard" icon="gauge" href="/features/dashboard">
    Central hub displaying key metrics, upcoming tasks, quick actions, and activity feed for healthcare providers.
  </Card>
  <Card title="Analytics Dashboard" icon="chart-line" href="/features/analytics">
    Comprehensive insights with KPI cards, activity trends, patient status distribution, and performance metrics.
  </Card>
  <Card title="Global Search" icon="magnifying-glass" href="/features/global-search">
    Quick search across patients, pages, and resources with keyboard navigation and recent search history.
  </Card>
  <Card title="Keyboard Shortcuts" icon="keyboard" href="/features/keyboard-shortcuts">
    Navigate and control the application efficiently with keyboard commands for power users.
  </Card>
</CardGroup>

## Clinical Features

<CardGroup cols={2}>
  <Card title="Carepath Templates" icon="route" href="/features/carepaths">
    Create and manage structured patient care journey templates with steps, questionnaires, and version control.
  </Card>
  <Card title="Questionnaires" icon="clipboard-question" href="/features/questionnaires">
    Build patient data collection forms with 9 question types, threshold alerts, and recurrence settings.
  </Card>
  <Card title="Risk Scoring" icon="chart-mixed" href="/features/risk-scoring">
    Monitor patient risk levels with predictive analytics, trend tracking, and proactive alerts.
  </Card>
  <Card title="Alerts System" icon="bell" href="/features/alerts">
    Real-time monitoring of patient health data with threshold-based notifications and severity levels.
  </Card>
  <Card title="Pending Approvals" icon="clipboard-check" href="/features/pending-approvals">
    Review and approve patient questionnaire submissions with priority-based queue management.
  </Card>
</CardGroup>

## Communication

<CardGroup cols={2}>
  <Card title="Messaging System" icon="comments" href="/features/messaging">
    Secure patient-provider communication through topic-based conversations with read/unread tracking.
  </Card>
  <Card title="Patient Notes" icon="note-sticky" href="/features/patient-notes">
    Comprehensive notes system with categories, priorities, and privacy controls for patient documentation.
  </Card>
</CardGroup>

## Administration

<CardGroup cols={2}>
  <Card title="Settings" icon="gear" href="/features/settings">
    Manage user profile, website preferences, organization selection, and system configuration.
  </Card>
  <Card title="Organization Switching" icon="building" href="/features/organization-switching">
    Multi-facility support allowing users to switch between different care units, hospitals, and departments.
  </Card>
</CardGroup>

## Feature Matrix

| Feature | Patient Facing | Provider Facing | Admin |
|---------|---------------|-----------------|-------|
| Dashboard | ✓ | ✓ | ✓ |
| Messaging | ✓ | ✓ | - |
| Questionnaires | ✓ | ✓ | ✓ |
| Carepaths | ✓ | ✓ | ✓ |
| Alerts | - | ✓ | ✓ |
| Risk Scoring | - | ✓ | ✓ |
| Patient Notes | - | ✓ | - |
| Analytics | - | ✓ | ✓ |
| Settings | ✓ | ✓ | ✓ |
| Organization Switching | - | ✓ | ✓ |

## Technical Documentation

<Card title="State Management Analysis" icon="code" href="/rfc/state-management-analysis">
  Technical analysis comparing NgRx vs service-based state management approaches for this Angular healthcare application.
</Card>

## Getting Started

<Steps>
  <Step title="Explore the Dashboard">
    Start with the [Dashboard](/features/dashboard) to understand the main interface
  </Step>
  <Step title="Learn Clinical Tools">
    Review [Questionnaires](/features/questionnaires) and [Carepaths](/features/carepaths) for clinical workflows
  </Step>
  <Step title="Understand Communication">
    Check [Messaging](/features/messaging) and [Patient Notes](/features/patient-notes) for documentation
  </Step>
  <Step title="Configure Settings">
    Set up your preferences in [Settings](/features/settings)
  </Step>
</Steps>
