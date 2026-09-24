# VisionAgent — Model and Data Specification

## 1. Vision Model
Candidate baseline:
- YOLOv8n → ONNX

The final detector is selected after evaluating accuracy, latency, model size and browser portability.

## 2. OCR
Benchmark:
- EasyOCR
- PaddleOCR
- RapidOCR
- Tesseract

Evaluate character error rate, speed and browser portability.

## 3. PII Detection
MVP uses:
- email regex
- Indian phone detection
- Aadhaar + Verhoeff validation
- PAN format
- card + Luhn validation
- IFSC
- PIN code
- DOB
- password/context detection
- label/context signals
- local DOM sensitivity hints

Optional later:
- NER for free-text names/addresses
- face detector
- multilingual OCR

## 4. Reasoning Model
Use a pluggable Reasoner interface:
- hosted LLM/VLM for normal reasoning
- RuleReasoner as offline fallback

The model must output structured actions rather than arbitrary browser commands.

## 5. Dataset
Initial target:
- 500–1,000 diverse screenshots

Testbed:
- job application
- login
- checkout
- noisy content page

Variation:
- viewport
- zoom
- layout
- theme
- fonts
- labels
- element size
- PII types

Split by site template to test generalization to unseen layouts.

## 6. Data Contracts
Core contracts:
- Element
- PIIFinding
- SanitizedContext
- Action
- StepResult
- TabState
- Conversation
- AgentTask
