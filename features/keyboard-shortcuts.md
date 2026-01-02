---
title: Keyboard Shortcuts
description: Navigate and control the application with keyboard commands
---

# Keyboard Shortcuts

The Healthcare Platform supports keyboard shortcuts for efficient navigation and common actions, enabling power users to work faster without reaching for the mouse.

## Overview

Keyboard shortcuts provide rapid access to navigation and actions throughout the application.

<Info>
Press `?` at any time to open the keyboard shortcuts help modal.
</Info>

## Navigation Shortcuts

Use `G` followed by a letter to navigate to different pages:

<CardGroup cols={3}>
  <Card title="G then D" icon="gauge">
    Dashboard
  </Card>
  <Card title="G then P" icon="users">
    Patients
  </Card>
  <Card title="G then A" icon="chart-line">
    Analytics
  </Card>
  <Card title="G then C" icon="calendar">
    Calendar
  </Card>
  <Card title="G then M" icon="comments">
    Messages
  </Card>
  <Card title="G then S" icon="gear">
    Settings
  </Card>
</CardGroup>

<Warning>
Press `G`, then within 500ms press the second key. If you wait too long, the sequence resets.
</Warning>

## Action Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl+K` | Open global search |
| `?` | Show keyboard shortcuts help |
| `Esc` | Close modal / Cancel action |
| `N` | Create new (context-aware) |

## Search Navigation

When global search is open:

| Key | Action |
|-----|--------|
| `↑` | Move selection up |
| `↓` | Move selection down |
| `Enter` | Select highlighted item |
| `Esc` | Close search |

## Modal Behavior

<Tabs>
  <Tab title="Closing">
    - `Esc` closes any open modal
    - Click outside modal to close
    - Close button in modal header
  </Tab>
  <Tab title="Navigation">
    - `Tab` moves between form fields
    - `Shift+Tab` moves backwards
    - `Enter` submits forms (when appropriate)
  </Tab>
</Tabs>

## Input Field Behavior

<Info>
Keyboard shortcuts are automatically disabled when typing in form fields to prevent accidental navigation.
</Info>

Shortcuts disabled when:
- Typing in text inputs
- Typing in textareas
- Using select dropdowns
- Editing rich text

## Shortcut Help Modal

The help modal displays:

| Section | Contents |
|---------|----------|
| Navigation | Go-to shortcuts with destinations |
| Actions | Action shortcuts with descriptions |
| Footer | Reminder about `?` key |

## Quick Reference

### Most Used

| Shortcut | Action |
|----------|--------|
| `Ctrl+K` | Search |
| `G` `D` | Go to Dashboard |
| `G` `P` | Go to Patients |
| `Esc` | Close/Cancel |
| `?` | Help |

### Navigation Sequence

```
G → D = Dashboard
G → P = Patients
G → A = Analytics
G → C = Calendar
G → M = Messages
G → S = Settings
```

## Best Practices

<Check>
**Learn `Ctrl+K`**: The most useful shortcut for quick search access
</Check>

<Check>
**Use `G` Shortcuts**: Navigate without touching the mouse
</Check>

<Check>
**Press `?` When Unsure**: Quick reference always available
</Check>

<Check>
**Use `Esc` Liberally**: Quickly close modals and cancel actions
</Check>

<Check>
**Hybrid Workflow**: Combine keyboard and mouse for best efficiency
</Check>

## Accessibility

Keyboard shortcuts support accessibility by:
- Providing mouse-free navigation
- Reducing repetitive movements
- Enabling faster task completion
- Supporting screen reader workflows

## Customization

<Info>
Shortcuts are currently fixed but designed around common patterns used in popular applications.
</Info>

Design principles:
- `G` for "Go to" navigation (like GitHub)
- `Ctrl+K` for search (like VS Code, Slack)
- `?` for help (universal convention)
- `Esc` for cancel (universal convention)
