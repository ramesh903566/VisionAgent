# VisionAgent

VisionAgent is a conversational, privacy-preserving, multi-tab desktop browser AI agent.

## Core loop
SEE → PROTECT → REASON → ACT → VERIFY

## Product
VisionAgent is delivered as a Chromium browser extension.

Clicking the pinned extension icon opens the Home popup:
- + New Chat
- Recent conversations
- Chat
- History
- Settings

The full agent interface runs in the Side Panel and supports:
- Chat
- Voice
- Target-tab selection
- Agent status
- Pause / Resume / Stop
- Multi-tab task management

## Architecture
Local visual perception and privacy protection happen on-device. Only sanitized context crosses the privacy boundary to the server reasoning service. Browser actions are validated and executed locally, then verified.

## Reference implementation
Python + Playwright is used for development and evaluation. The browser extension is the intended final client deployment.

## Documentation
- PRD.md
- TDD.md
- ARCHITECTURE.md
- API_SPEC.md
- PRIVACY_SPEC.md
- PRIVACY_BOUNDARY.md
- MODEL_SPEC.md
- EVALUATION_PLAN.md
- CONTRACTS.md

## Implementation
See the separate VisionAgent Implementation Plan for the phase-by-phase build sequence.
