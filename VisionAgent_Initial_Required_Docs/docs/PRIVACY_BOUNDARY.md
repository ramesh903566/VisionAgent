# VisionAgent — Privacy Boundary Specification

## Boundary
`LOCAL_DEVICE → SERVER`

## Allowed
- sanitized element IDs/types
- non-sensitive labels
- placeholders
- sanitized page title
- sanitized URL
- reviewed task text
- redacted screenshot only when explicitly enabled

## Never allowed
- raw screenshot
- passwords
- raw email/phone
- Aadhaar/PAN
- card/CVV
- unredacted faces
- credentials/profile values
- API keys
- raw DOM
- sensitive DOM values

## Invariant
**No raw screenshot or raw sensitive value may cross the privacy boundary.**

## Enforcement
Every network request must pass through the independent leak scanner. A failed scan blocks transmission and records a safe diagnostic.

## Review
Every implementation phase must be checked against this document.
