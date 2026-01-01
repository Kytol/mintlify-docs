---
title: Messages
description: 'Secure messaging system with chat topics and threaded conversations'
icon: 'comments'
---

# Messages

Secure messaging system enabling communication between healthcare providers and patients through organized chat topics and threaded conversations.

## Overview

The Messages page provides a comprehensive messaging interface for healthcare communication. It features chat topics for organizing conversations, threaded message views, and support for attachments. The system ensures HIPAA-compliant secure messaging between providers and patients.

## Features

### Chat Topics Panel
- List of active conversation topics
- Unread message indicators
- Topic search and filtering
- Create new topic functionality
- Topic categorization (Patient, Team, General)

### Chat Thread View
- Chronological message display
- Message timestamps
- Read receipts
- Sender identification with avatars
- Message status indicators

### Message Composer
- Rich text input
- File attachment support
- Emoji support
- Send button with keyboard shortcut
- Draft auto-save

### Topic Management
- Create new topics
- Add/remove participants
- Archive topics
- Topic settings

### Search & Filter
- Search messages by content
- Filter by topic type
- Filter by date range
- Filter by participant

## Use Cases

### UC-MSG-001: Send Patient Message
**Actor**: Healthcare Provider  
**Description**: Provider sends a message to a patient regarding their care.

**Flow**:
1. Provider navigates to Messages
2. Selects patient's topic or creates new
3. Types message in composer
4. Optionally attaches files
5. Clicks send
6. Message appears in thread
7. Patient receives notification

### UC-MSG-002: Review Unread Messages
**Actor**: Healthcare Provider  
**Description**: Provider reviews and responds to unread messages.

**Flow**:
1. Provider sees unread count on Messages nav
2. Navigates to Messages page
3. Topics with unread messages are highlighted
4. Provider selects topic
5. Reads new messages
6. Responds as needed
7. Messages marked as read

### UC-MSG-003: Create Team Discussion
**Actor**: Healthcare Provider  
**Description**: Provider starts a team discussion about a patient case.

**Flow**:
1. Provider clicks "New Topic"
2. Selects "Team" topic type
3. Adds team members as participants
4. Enters topic title and initial message
5. Creates topic
6. Team members are notified

### UC-MSG-004: Search Message History
**Actor**: Healthcare Provider  
**Description**: Provider searches for specific information in past messages.

**Flow**:
1. Provider enters search term
2. Results show matching messages
3. Provider clicks on result
4. Navigates to message in context
5. Reviews surrounding conversation

## User Stories

### US-MSG-001
**As a** healthcare provider  
**I want to** send secure messages to patients  
**So that** I can communicate care instructions

**Acceptance Criteria**:
- [ ] Messages are encrypted in transit and at rest
- [ ] Patient receives notification of new message
- [ ] Message delivery status is shown
- [ ] Attachments are supported

### US-MSG-002
**As a** healthcare provider  
**I want to** see unread message counts  
**So that** I can prioritize responses

**Acceptance Criteria**:
- [ ] Unread count shows in navigation
- [ ] Topics with unread messages are highlighted
- [ ] Count updates in real-time
- [ ] Marking as read updates count

### US-MSG-003
**As a** healthcare provider  
**I want to** organize messages by topic  
**So that** I can manage multiple conversations

**Acceptance Criteria**:
- [ ] Topics are listed in sidebar
- [ ] Topics can be categorized
- [ ] Topics can be searched
- [ ] Topics can be archived

### US-MSG-004
**As a** healthcare provider  
**I want to** attach files to messages  
**So that** I can share documents with patients

**Acceptance Criteria**:
- [ ] Multiple file types supported
- [ ] File size limits are enforced
- [ ] Upload progress is shown
- [ ] Files can be previewed

### US-MSG-005
**As a** healthcare provider  
**I want to** search message history  
**So that** I can find past communications

**Acceptance Criteria**:
- [ ] Search covers all topics
- [ ] Results show message context
- [ ] Search is fast and responsive
- [ ] Results link to full thread

## Component Dependencies

```
MessagesComponent
├── ChatTopicsComponent
│   └── TopicListItemComponent
├── ChatThreadComponent
│   ├── MessageBubbleComponent
│   └── MessageComposerComponent
└── NewTopicModalComponent
```

## Data Flow

```
┌─────────────────┐     ┌──────────────────┐
│   ChatService   │────▶│                  │
└─────────────────┘     │                  │
         │              │    Messages      │
         │              │    Component     │
         ▼              │                  │
┌─────────────────┐     │                  │
│  WebSocket      │────▶│                  │
│  Connection     │     └────────┬─────────┘
└─────────────────┘              │
                        ┌────────┴────────┐
                        │                 │
                        ▼                 ▼
                 ┌──────────┐      ┌──────────┐
                 │ChatTopics│      │ChatThread│
                 └──────────┘      └──────────┘
```

## Technical Notes

- Real-time updates via WebSocket connection
- Messages are stored encrypted
- Supports offline message queuing
- File attachments stored in secure blob storage
- Message search uses full-text indexing
- Responsive layout for mobile messaging
- Keyboard shortcuts for power users (Ctrl+Enter to send)
