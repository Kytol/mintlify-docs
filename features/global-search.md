---
title: Global Search
description: Quick search across patients, pages, and resources
---

# Global Search

The Global Search feature provides instant access to patients, pages, and resources from anywhere in the application using a keyboard-driven interface.

## Overview

Global search enables rapid navigation and patient lookup without leaving your current context. Results appear instantly as you type.

<Info>
Press `Ctrl+K` (or `Cmd+K` on Mac) from anywhere to open search.
</Info>

## Activation

<CardGroup cols={2}>
  <Card title="Keyboard Shortcut" icon="keyboard">
    `Ctrl+K` or `Cmd+K`
  </Card>
  <Card title="Click Icon" icon="magnifying-glass">
    Search icon in navigation bar
  </Card>
</CardGroup>

## Search Interface

### Search Input
- Large, focused input field
- Placeholder text with search hints
- ESC key indicator for closing

### Results Display

| Element | Description |
|---------|-------------|
| Grouping | Results grouped by type |
| Icon | Visual indicator of result type |
| Title | Primary result text |
| Subtitle | Additional context |
| Type Badge | Patient, page, carepath, etc. |

## Search Capabilities

<Tabs>
  <Tab title="Patient Search">
    Find patients by:
    - Name (partial match)
    - Patient ID
    
    Results show:
    - Patient name
    - ID and current status
    - Direct link to patient profile
  </Tab>
  <Tab title="Page Navigation">
    Quick access to all main pages:
    - Dashboard
    - Patients
    - Carepaths
    - Questionnaires
    - Alerts
    - Calendar
    - Messages
    - Settings
  </Tab>
  <Tab title="Resources">
    Find resources like:
    - Carepath templates
    - Questionnaire forms
    - Documentation
  </Tab>
</Tabs>

## Recent Searches

When search is empty, displays:
- Recent search queries
- Associated results (if any)
- Clear all button
- Individual remove buttons

<Info>
Recent searches are stored in session storage and cleared when the browser closes.
</Info>

## Quick Links

Grid of common destinations when no search query:

<CardGroup cols={4}>
  <Card title="Dashboard" icon="gauge" />
  <Card title="Patients" icon="users" />
  <Card title="Carepaths" icon="route" />
  <Card title="Questionnaires" icon="clipboard-question" />
  <Card title="Alerts" icon="bell" />
  <Card title="Calendar" icon="calendar" />
  <Card title="Messages" icon="comments" />
  <Card title="Settings" icon="gear" />
</CardGroup>

## Keyboard Navigation

| Key | Action |
|-----|--------|
| `↑` / `↓` | Navigate results |
| `Enter` | Select highlighted result |
| `Escape` | Close search |
| `Ctrl+K` | Toggle search open/close |

## Visual Feedback

| State | Display |
|-------|---------|
| Loading | Spinner during search |
| No Results | "No results found" message |
| Selected | Highlighted background |
| Hover | Subtle highlight |

## Footer Help

Bottom bar shows keyboard hints:
- `↑↓` Navigate
- `↵` Select
- `esc` Close

## Best Practices

<Check>
**Use Keyboard**: `Ctrl+K` is the fastest way to access search
</Check>

<Check>
**Partial Matching**: Type just a few characters of patient name
</Check>

<Check>
**Recent Searches**: Leverage recent searches for repeated lookups
</Check>

<Check>
**Navigate with Keys**: Use arrow keys and Enter for efficiency
</Check>

## Integration

Global search is available from:
- All pages in the application
- Any modal or overlay (closes first)
- Mobile and desktop views
