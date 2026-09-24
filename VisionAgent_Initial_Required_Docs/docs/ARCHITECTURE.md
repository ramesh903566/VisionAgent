# VisionAgent — System Architecture

## 1. High-Level Architecture

```text
                         USER
                          │
                 ┌────────┴────────┐
                 │                 │
                CHAT             VOICE
                 │                 │
                 └────────┬────────┘
                          ↓
                  CONVERSATION LAYER
                          ↓
                    TASK MANAGER
                          ↓
                   TARGET TAB MANAGER
                          ↓
             ┌──────────────────────────┐
             │ SEE                      │
             │ PROTECT                  │
             │ REASON                   │
             │ ACT                      │
             │ VERIFY                   │
             └──────────────────────────┘
                          ↓
                   USER RESPONSE
```

## 2. Trust Zones

### Local trusted zone
- Browser screenshot
- Local DOM structural metadata
- Vision model
- OCR
- PII detector
- Privacy Policy Engine
- Redactor
- Credential/Profile Store
- Leak Scanner
- Action Validator
- Browser Executor
- Verifier

### Privacy boundary
```text
LOCAL DEVICE  ═══════════ PRIVACY BOUNDARY ═══════════  SERVER
```

Only sanitized context may cross this boundary.

### Server zone
- LLM/VLM reasoning
- Structured action generation

## 3. Perception Architecture
Screenshot-based vision is the primary runtime perception mechanism. Local DOM metadata is auxiliary and may improve semantic/sensitivity detection. Raw DOM and sensitive values do not leave the device.

## 4. Privacy Architecture

```text
Screenshot / local signals
          ↓
      PII Detection
          ↓
   Privacy Policy Engine
          ↓
        Redactor
          ↓
   Sanitized Context
          ↓
   Independent Leak Scan
       ↙          ↘
    BLOCK          PASS
                    ↓
                  Server
```

## 5. Action Architecture

```text
Server LLM/VLM
      ↓
Action JSON
      ↓
Pydantic/schema validation
      ↓
Tab ownership validation
      ↓
Element/value_ref validation
      ↓
Local Executor
      ↓
Verify
```

## 6. Extension Navigation

```text
Pinned Icon
    ↓
Home Popup
    ├── New Chat
    ├── Recent
    ├── Chat
    ├── History
    └── Settings
             ↓
        Full Side Panel
```

## 7. Multi-tab Architecture
Each task maintains an isolated task context and target tab ID. A tab ownership manager prevents conflicting control and provides lock/unlock lifecycle.
