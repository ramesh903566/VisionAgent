# VisionAgent — Product Requirements Document

## 1. Product Overview
VisionAgent is a conversational, privacy-preserving, multi-tab desktop browser AI agent. It is delivered as a Chromium browser extension with local visual perception and privacy protection, a server-side reasoning service, and local browser action execution.

Core loop:

SEE → PROTECT → REASON → ACT → VERIFY

## 2. Target Platform
- Desktop Chromium-based browsers.
- Primary final client: Chrome/Chromium Manifest V3 extension.
- Mobile browser support is out of the initial scope.

## 3. User Experience

### 3.1 Extension Home Popup
When the user clicks the pinned VisionAgent extension icon, the extension opens a compact Home popup containing:
- + New Chat
- Recent conversations
- Chat
- History
- Settings

### 3.2 Side Panel
The full agent workspace is opened in the browser Side Panel and contains:
- Conversation
- Voice input/output controls
- Current target tab
- Agent pipeline status
- Pause / Resume / Stop
- Task progress

Chat and voice are two interfaces to the same conversation and agent state; they are not separate agents.

## 4. Core Functional Requirements

### FR-01 — Conversational interface
The user shall be able to give tasks through text chat and voice.

### FR-02 — Visual perception
The system shall primarily use screenshot-based visual perception and OCR locally.

### FR-03 — Privacy protection
PII and sensitive information shall be detected and handled locally before any server transmission.

### FR-04 — Sanitized reasoning
The server reasoning service shall receive sanitized context rather than raw sensitive page data.

### FR-05 — Structured actions
The reasoning service shall return validated structured actions such as click, type, scroll, select, wait, done, fail, or ask_user.

### FR-06 — Local execution
Browser actions shall be validated and executed locally.

### FR-07 — Verification
After an action, VisionAgent shall re-capture/re-evaluate the page and determine whether the action succeeded.

### FR-08 — Multi-tab operation
The user shall be able to assign a task to a specific browser tab.

### FR-09 — Target-tab locking
While VisionAgent controls a target tab, that tab shall be locked against user interaction. Other tabs remain user-controlled.

### FR-10 — Agent controls
The user shall be able to Pause, Resume, and Stop an active task.

### FR-11 — History
The system shall provide conversation history with search, continuation, rename, deletion, and clear-history capabilities.

### FR-12 — Settings
The system shall provide settings for general behavior, agent behavior, privacy/security, voice, browser behavior, and advanced configuration.

## 5. Privacy Requirements
The following shall never cross the local-to-server privacy boundary:
- raw screenshots
- passwords
- raw email, phone, Aadhaar, PAN, card numbers, CVV and similar sensitive values
- unredacted faces
- credential/profile values
- API keys
- raw DOM or sensitive DOM values

An independent leak scanner shall run before network transmission.

## 6. Initial Scope
Included:
- Desktop browser extension
- Chat + voice
- Visual perception + OCR
- Local PII detection and redaction
- Server reasoning over sanitized context
- Local browser actions
- Verification
- Multi-tab assignment and locking
- History
- Settings

Excluded initially:
- Mobile browser
- CAPTCHA solving
- unrestricted concurrent agents on the same tab
- arbitrary cross-tab sensitive-data transfer

## 7. Product Outcome
A working desktop browser agent that can understand a webpage visually, protect sensitive information locally, reason over sanitized context, perform browser tasks in a user-selected tab, and verify its actions.
