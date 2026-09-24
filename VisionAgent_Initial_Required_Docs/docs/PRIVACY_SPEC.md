# VisionAgent — Privacy Specification

## 1. Privacy Boundary
The privacy boundary is:

```text
Local desktop/browser → Server reasoning service
```

## 2. Never Allowed to Leave the Device
- raw screenshots
- passwords
- raw email/phone
- Aadhaar/PAN
- card numbers/CVV
- unredacted faces
- credential/profile values
- API keys
- sensitive DOM values
- raw DOM

## 3. Allowed After Sanitization
- element IDs
- element types
- non-sensitive labels
- placeholders
- sanitized page title
- sanitized URL
- reviewed task text
- redacted screenshot only when explicitly enabled

## 4. Privacy Pipeline

```text
Detect
  ↓
Policy
  ↓
Redact
  ↓
Build sanitized context
  ↓
Independent leak scanner
  ↓
PASS → Network
FAIL → BLOCK + LOG
```

## 5. Policy Engine
Example policies:
- email → placeholder
- password → redact
- PAN → redact
- card → redact
- face → blur when permitted

Unknown sensitive types default to a restrictive handling decision.

## 6. Local Credential/Profile Store
Real values remain local. The reasoner receives a value_ref such as `profile.email`; the executor resolves the actual value locally.

Prototype storage may use protected local storage. Production should use a browser/OS credential store.

## 7. History Privacy
History should store safe conversation text and metadata. Raw PII, credentials and raw screenshots should not be persisted by default.

## 8. Independent Leak Scanner
The leak scanner must be separate from the PII detector implementation and must inspect:
- known real values
- independent regex/validator matches
- outgoing images through OCR
- outgoing JSON
- logs/files where applicable

## 9. Multi-tab Privacy
Tasks have isolated contexts. Sensitive information must not be copied between tabs unless a future explicit policy and confirmation mechanism is implemented.
