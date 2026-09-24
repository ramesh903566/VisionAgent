# VisionAgent — Technical Design Document

## 1. Technical Objective
Implement the VisionAgent product as a desktop Chromium browser extension backed by a local perception/privacy pipeline and a server reasoning service.

## 2. Technology Stack

### Reference/evaluation
- Python 3.11
- Playwright
- Chromium
- ONNX Runtime
- Pydantic
- pytest

### Final client
- Chrome/Chromium Manifest V3
- TypeScript
- React
- Vite
- Tailwind CSS
- ONNX Runtime Web
- Web Worker
- WASM/WebGPU where supported

### AI
- Lightweight UI detector, candidate YOLOv8n → ONNX
- OCR benchmark
- Deterministic PII detectors
- Hosted LLM/VLM through a Reasoner interface
- RuleReasoner offline fallback

## 3. Runtime Pipeline

CAPTURE
→ PERCEIVE
→ PROTECT
→ REASON
→ ACT
→ VERIFY
→ LOOP / DONE / FAIL

## 4. Extension Components

```text
extension/
├── popup/
├── sidepanel/
├── history/
├── settings/
├── content/
├── background/
├── privacy/
├── perception/
└── shared/
```

### Popup
Provides quick access to New Chat, Recent conversations, Chat, History and Settings.

### Side Panel
Provides the full conversation and active-agent interface.

### Background/service worker
Coordinates extension-level state, tab ownership, messaging and lifecycle.

### Content script
Captures/coordinates page interaction and provides local structural DOM signals without exporting sensitive values.

### Web Worker
Runs browser inference without blocking the UI thread.

## 5. Multi-tab State

```text
AVAILABLE
   ↓
ASSIGNED
   ↓
LOCKED
   ↓
AGENT_RUNNING
   ↓
PAUSED / COMPLETED / FAILED
```

Rules:
- Each active task owns one target tab.
- Two tasks cannot control the same tab simultaneously.
- The target tab remains locked while paused unless the product explicitly defines another policy.
- Stop, completion, or failure releases ownership.
- Other browser tabs remain available to the user.
- The agent should not steal browser focus unless explicitly required by the user action.

## 6. Conversation State
Chat and voice use the same:
- conversation_id
- task_id
- target_tab_id
- agent state
- history
- controls

## 7. History Storage
Store sanitized conversation data and metadata. Raw screenshots, credentials and raw PII shall not be stored in ordinary conversation history.

## 8. Security
The LLM response must pass:
1. schema validation
2. target-tab ownership validation
3. element validation
4. value_ref validation
5. safety policy checks

Only then may the executor run the action.
