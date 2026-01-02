---
title: Settings
description: Manage profile, preferences, and organization settings
---

# Settings

The Settings page allows users to customize their profile, adjust application preferences, and manage organization-level configurations.

## Overview

Settings are organized into sections for easy navigation. Changes are saved automatically or with explicit save buttons depending on the setting type.

<Info>
Some settings may require administrator privileges to modify.
</Info>

## Profile Management

### User Profile Fields

| Field | Required | Description |
|-------|----------|-------------|
| Avatar | No | Profile image URL |
| Full Name | Yes | Display name |
| Email | Yes | Contact email (validated) |
| Role | Read-only | Admin-managed role |

### Avatar Options

<Steps>
  <Step title="Enter URL">
    Paste an image URL in the avatar field
  </Step>
  <Step title="Preview">
    Image displays in circular preview
  </Step>
  <Step title="Remove">
    Hover and click remove to clear
  </Step>
</Steps>

<Info>
When no avatar is set, initials are displayed as a fallback.
</Info>

## Website Settings

### Theme Options

<Tabs>
  <Tab title="Dark">
    Default theme with dark backgrounds and light text. Reduces eye strain in low-light environments.
  </Tab>
  <Tab title="Light">
    Bright theme with light backgrounds. Better for well-lit environments.
  </Tab>
  <Tab title="Blue">
    Alternative theme with blue accent colors.
  </Tab>
</Tabs>

Theme changes apply immediately across the application.

### Font Size

| Size | Description |
|------|-------------|
| Small | Compact text for more content |
| Medium | Default balanced size |
| Large | Larger text for accessibility |

### Notifications

| Setting | Description |
|---------|-------------|
| In-app | Enable/disable in-app notifications |
| Email | Enable/disable email notifications |

### Language

Supported languages:
- English
- Finnish
- French
- Spanish
- Swedish
- German

## Organization Settings

<Card title="Organization Switching" icon="building" href="/features/organization-switching">
  Switch between hospitals, departments, and care units. See the dedicated documentation for details.
</Card>

### Organization Selection

1. Select new organization from dropdown
2. Review organization details
3. Click "Switch Organization"
4. Settings persist across sessions

### Organization Details

View selected organization info:
- Organization type
- Address
- Phone number

## Help & Support

### Documentation Links

<CardGroup cols={3}>
  <Card title="User Guide" icon="book">
    Comprehensive usage documentation
  </Card>
  <Card title="Video Tutorials" icon="video">
    Step-by-step video guides
  </Card>
  <Card title="FAQ" icon="circle-question">
    Frequently asked questions
  </Card>
</CardGroup>

### Quick Actions

| Action | Description |
|--------|-------------|
| Change Password | Update account password |
| Report a Bug | Submit issue report |
| Request Feature | Suggest improvements |
| System Status | Check platform health |

## About Section

### Application Info

| Field | Description |
|-------|-------------|
| Version | Current application version |
| Build | Build number and date |
| License | License information |

### MDR Compliance

<Accordion title="Medical Device Regulation" icon="certificate">
Toggle to view compliance information:
- CE marking status
- Regulation reference (EU 2017/745)
- Compliance documentation
</Accordion>

## Security Configuration

<Warning>
Security settings require administrator privileges.
</Warning>

### Authentication Settings

| Setting | Description |
|---------|-------------|
| Two-Factor Auth | Require 2FA for all users |
| Password Length | Minimum password length |
| Password Complexity | Require special characters |
| Password Expiry | Days until password expires |

### Access Controls

| Setting | Description |
|---------|-------------|
| Login Attempts | Max failed attempts before lockout |
| Lockout Duration | Minutes until account unlocks |
| IP Whitelist | Allowed IP addresses |
| Session Timeout | Minutes until auto-logout |

## Admin Configuration

<Warning>
Admin settings affect all users in the organization.
</Warning>

### Hospital Settings

| Setting | Description |
|---------|-------------|
| Hospital Logo | Organization branding |
| Hospital Name | Display name |
| Primary Color | Theme accent color |
| Support Contact | Help desk information |
| Default Timezone | Organization timezone |

### Feature Flags

| Feature | Description |
|---------|-------------|
| Messaging | Enable/disable messaging |
| AI Features | Enable/disable AI assistance |
| Risk Scoring | Enable/disable risk analytics |
| Care Team | Enable/disable team features |
| A/B Testing | Enable/disable experiments |

### Maintenance Mode

Enable maintenance mode to:
- Display maintenance message to users
- Prevent new logins
- Allow admin access only

## Data Persistence

Settings are saved to different storage locations:

| Setting Type | Storage |
|--------------|---------|
| Preferences | Local storage |
| Profile Data | Server |
| Session State | Session storage |
| Organization | Server + Local |

## Best Practices

<Check>
**Keep Profile Current**: Update contact information regularly
</Check>

<Check>
**Choose Appropriate Theme**: Select theme based on your environment
</Check>

<Check>
**Enable Notifications**: Stay informed about important alerts
</Check>

<Check>
**Review Organization**: Verify correct organization selection
</Check>

<Check>
**Strong Passwords**: Use complex passwords and enable 2FA
</Check>
