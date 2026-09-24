# VisionAgent — API Specification

## 1. API Principle
The backend receives sanitized context only. The client performs all privacy detection, policy enforcement, redaction, and leak scanning before transmission.

## 2. POST /v1/reason

### Request
```json
{
  "conversation_id": "uuid",
  "task_id": "uuid",
  "target_tab_id": "tab-2",
  "task": "Submit the application",
  "context": {
    "page_title": "Job Application",
    "url_sanitized": "https://site/apply",
    "elements": [
      {
        "id": 7,
        "type": "input",
        "label": "Email",
        "value": "[EMAIL_1]"
      },
      {
        "id": 9,
        "type": "button",
        "label": "Submit Application"
      }
    ],
    "image_included": false
  }
}
```

### Response
```json
{
  "action_id": "uuid",
  "action": "click",
  "element_id": 9,
  "value_ref": null,
  "reason": "Submit application",
  "confidence": 0.94
}
```

## 3. Action Schema

| Action | Required |
|---|---|
| click | element_id |
| type | element_id + value_ref |
| scroll | direction + amount |
| select | element_id + option |
| wait | duration_ms |
| done | reason recommended |
| fail | reason recommended |
| ask_user | reason recommended |

## 4. Security Validation
Every response must be checked for:
- valid action schema
- valid target tab ownership
- element_id existing in current perception context
- value_ref existing in local profile store
- no raw literal sensitive values
- action safety policy

## 5. Future API Areas
If cloud-synchronized history/accounts are later introduced, define separate authenticated conversation/history APIs only after the privacy model is approved.
