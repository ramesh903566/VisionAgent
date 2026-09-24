# VisionAgent — Evaluation Plan

## 1. Primary SIH Evaluation Metrics
The implementation plan identifies:
- Visual-context accuracy — 25%
- PII detection precision & recall — 20%
- Redaction precision — 20%
- Client resource utilization — 20%
- End-to-end latency — 15%

These weights must be checked against the official SIH26171 statement before final submission.

## 2. Internal Metrics
- Task Success Rate
- Privacy Leakage Rate
- Action Success Rate
- Average steps per task
- Stage-by-stage latency
- Peak RAM
- Average CPU
- Model load time

## 3. Evaluation Layers

### Perception
- detection mAP
- per-class precision/recall
- OCR character error rate
- label association accuracy
- element grounding accuracy

### Privacy
- PII precision/recall/F1
- redaction precision
- leakage rate
- over-redaction

### Agent
- task success
- action success
- invalid action rate
- verification success
- stuck-loop frequency

### Multi-tab
- correct task-to-tab assignment
- target-tab lock enforcement
- prevention of duplicate ownership
- other-tab usability
- pause/resume state preservation
- stop/completion/failure unlock

### Extension
Compare extension results with the Python/Playwright reference implementation.

## 4. Privacy Red-Team
Test:
- deliberate PII injection
- sensitive text hidden in page content
- misleading DOM attributes
- sensitive values in URLs
- OCR-visible PII
- log leakage
- prompt-injection text
- cross-tab isolation

## 5. Reporting
Use held-out test sites/layouts. Report failures and limitations. Internal engineering targets must be clearly labeled as internal targets, not official SIH requirements.
