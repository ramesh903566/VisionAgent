# VisionAgent — Data Contracts

## Element
```json
{
  "id": 7,
  "type": "input",
  "bbox": [100, 200, 300, 240],
  "center": [200, 220],
  "text": "",
  "label": "Email",
  "dom_hints": {"input_type": "email"},
  "sensitive": true,
  "pii_type": "email",
  "placeholder": "[EMAIL_1]"
}
```

## SanitizedContext
```json
{
  "task": "Submit the application",
  "page_title": "Job Application",
  "url_sanitized": "https://site/apply",
  "elements": [
    {"id": 7, "type": "input", "label": "Email", "value": "[EMAIL_1]"},
    {"id": 9, "type": "button", "label": "Submit Application"}
  ],
  "image_included": false
}
```

## Action
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

## TabState
```json
{
  "tab_id": "tab-2",
  "state": "AGENT_RUNNING",
  "task_id": "uuid",
  "locked": true
}
```

## Conversation
```json
{
  "conversation_id": "uuid",
  "title": "GitHub Issues",
  "created_at": "timestamp",
  "updated_at": "timestamp"
}
```

## AgentTask
```json
{
  "task_id": "uuid",
  "conversation_id": "uuid",
  "target_tab_id": "tab-2",
  "status": "RUNNING"
}
```

All contracts must be versioned when breaking changes are introduced.
