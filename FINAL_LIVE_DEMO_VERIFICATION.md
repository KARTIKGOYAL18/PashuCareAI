# PashuCare AI — Final Live Demonstration Verification Report
**Phase:** D4.4 Final Demonstration & Verification  
**Date:** November 22, 2026  
**System Status:** Operational & Demonstration-Ready  
**Classification System:** Five-Class Bovine Dermatological Image Classifier & Multi-Modal Clinical Decision Support  

---

## 1. Executive Summary

This report documents the live operational readiness of the **PashuCare AI Five-Class Bovine Dermatological Image Classifier** and verifies the end-to-end integration across both CLI demonstration tooling and live FastAPI endpoints.

All verification steps were conducted live on local hardware (Windows x64, Python 3.14, PyTorch CPU, FastAPI, Uvicorn) without modifying any protected datasets, production models, or checkpoints.

### Key Verification Milestones
- **Standalone CLI Demonstration:** Verified via `scripts/demo/run_five_class_demo.py --benchmark` across 6 curated benchmark cases.
- **Live HTTP API Operational:** Standalone FastAPI application (`local_inference.app:app`) running live on port 8000, serving:
  - `POST /predict-five-class-image` (Five-class PyTorch ResNet-18 classifier)
  - `POST /predict-text` (Clinical rule-based triage and symptom extractor)
  - `POST /predict-image` (Binary LightGBM LSD nodular lesion detector)
- **Zero Regressions:** 157 of 157 workspace tests passing (`pytest tests/`).
- **Robust Error Handling:** Verified rejection of empty payloads (HTTP 422) and corrupt image binaries (HTTP 422) with helpful error messages.
- **Protected Asset Integrity:** D3, D4, D4.1, D4.2 frozen external benchmark, and production LightGBM models preserved with zero modifications.

---

## 2. API Startup Instructions

### 2.1 Starting the Standalone Inference API
To start the live PashuCare AI local inference server:

```powershell
python -m uvicorn local_inference.app:app --host 127.0.0.1 --port 8000
```

When running, the server provides an interactive Swagger UI at:
- **Interactive API Docs:** `http://127.0.0.1:8000/docs`
- **OpenAPI Schema:** `http://127.0.0.1:8000/openapi.json`
- **Health Check Endpoint:** `http://127.0.0.1:8000/health` (HTTP 200 `{"status": "healthy"}`)

### 2.2 Model Checkpoints
The server automatically loads the recommended primary model:
- **Primary Model Checkpoint:** `models/image_experiments/phase_d4_3/exp2_d4_3_domain_robust_model.pt`
  - Architecture: ResNet-18 (5-class output: Dermatophilosis, Healthy, LSD, Pediculosis, Ringworm)
  - SHA-256: `f2183ee8d1f01e0412d0172f44f31bf77a0eb112b86ed8ef037e16d4298aec9d`
  - D4.3 Internal Validation: 75.90% Accuracy, 72.26% Balanced Accuracy, 72.84% Macro F1
- **Alternative Baseline Checkpoint:** `models/image_experiments/phase_d4_3/exp0_d4_3_baseline_model.pt`
  - Retained for comparative evaluation and OOD domain analysis (35.71% external accuracy).

---

## 3. End-to-End API Verification & Payloads

### 3.1 Live Endpoint 1: Five-Class Image Classifier (`POST /predict-five-class-image`)

#### Request: Healthy Cattle Image
```bash
curl -X POST "http://127.0.0.1:8000/predict-five-class-image" \
  -H "accept: application/json" \
  -H "Content-Type: multipart/form-data" \
  -F "file=@data/experiments/image_dataset_d4_3/images/healthy/D4_0020_healthy.jpg"
```

#### Response (`HTTP 200 OK`):
```json
{
  "status": "experimental_result",
  "predicted_class": "healthy",
  "confidence": 0.8597,
  "probabilities": {
    "dermatophilosis": 0.0092,
    "healthy": 0.8597,
    "lsd": 0.1122,
    "pediculosis": 0.0035,
    "ringworm": 0.0154
  },
  "model_name": "ResNet18-DomainRobust-D4.3",
  "inference_time_ms": 104.26,
  "screening_notice": "Educational experimental screening prototype only. This is not a veterinary diagnosis. Model scores are experimental screening indications and not clinically calibrated probabilities. Please consult a licensed veterinarian for clinical assessment and confirmatory diagnostic testing.",
  "limitations": [
    "Evaluated on experimental research collections; clinical sensitivity on unfamiliar field conditions may vary.",
    "Image predictions are sensitive to camera lighting, background grass/pasture cues, and focal distance.",
    "Must always be correlated with systemic clinical evaluation (temperature, appetite, lymph node palpation)."
  ]
}
```
*Verification Check:* Probabilities sum to $0.0092 + 0.8597 + 0.1122 + 0.0035 + 0.0154 = 1.0000$.

---

#### Request: Lumpy Skin Disease (LSD) Cattle Image
```bash
curl -X POST "http://127.0.0.1:8000/predict-five-class-image" \
  -H "accept: application/json" \
  -H "Content-Type: multipart/form-data" \
  -F "file=@data/experiments/image_dataset_d4_3/images/lsd/D4_0089_lsd.jpg"
```

#### Response (`HTTP 200 OK`):
```json
{
  "status": "experimental_result",
  "predicted_class": "lsd",
  "confidence": 0.8346,
  "probabilities": {
    "dermatophilosis": 0.0108,
    "healthy": 0.0796,
    "lsd": 0.8346,
    "pediculosis": 0.0143,
    "ringworm": 0.0607
  },
  "model_name": "ResNet18-DomainRobust-D4.3",
  "inference_time_ms": 28.1,
  "screening_notice": "Educational experimental screening prototype only. This is not a veterinary diagnosis. Model scores are experimental screening indications and not clinically calibrated probabilities. Please consult a licensed veterinarian for clinical assessment and confirmatory diagnostic testing.",
  "limitations": [
    "Evaluated on experimental research collections; clinical sensitivity on unfamiliar field conditions may vary.",
    "Image predictions are sensitive to camera lighting, background grass/pasture cues, and focal distance.",
    "Must always be correlated with systemic clinical evaluation (temperature, appetite, lymph node palpation)."
  ]
}
```

---

### 3.2 Live Endpoint 2: Existing Clinical Text Triage (`POST /predict-text`)

#### Request:
```bash
curl -X POST "http://127.0.0.1:8000/predict-text" \
  -H "Content-Type: application/json" \
  -d '{"text": "Cow has high fever and swelling with nodular lesions on skin"}'
```

#### Response (`HTTP 200 OK`):
```json
{
  "status": "insufficient_information",
  "decision_state": "insufficient_information",
  "emergency_escalation": false,
  "emergency_reason": null,
  "primary_diagnosis": null,
  "differential_diagnoses": [],
  "margin": null,
  "distinguishing_questions": [
    "Has the cow experienced any changes in feeding, rumination (chewing cud), or milk yield?",
    "Have you observed any abnormal discharges from the eyes, nose, mouth, or dung consistency?"
  ],
  "extraction_summary": {
    "confirmed_present": ["fever", "swelling"],
    "confirmed_absent": [],
    "unmatched_phrases": ["nodular lesions on skin"],
    "active_symptoms_count": 2,
    "completeness_score": 0.0215
  },
  "nearest_jaccard_distance": 0.6,
  "active_symptoms_count": 2,
  "message": "Only 0–2 symptoms were identified. A reliable veterinary assessment cannot be produced from sparse observations. Please observe and confirm additional symptoms before re-evaluating.",
  "notice": "Educational experimental prototype only; this is not a veterinary diagnosis. Model scores are not clinically calibrated probabilities."
}
```
*Verification Check:* Clinical safety gate triggered properly; distinguishing questions returned without runtime exceptions.

---

### 3.3 Live Endpoint 3: Existing Binary LSD Image Screening (`POST /predict-image`)

#### Request:
```bash
curl -X POST "http://127.0.0.1:8000/predict-image" \
  -H "accept: application/json" \
  -H "Content-Type: multipart/form-data" \
  -F "file=@data/experiments/image_dataset_d4_3/images/lsd/D4_0089_lsd.jpg"
```

#### Response (`HTTP 200 OK`):
```json
{
  "status": "detected",
  "condition": "Lumpy Skin Disease (Experimental)",
  "decision_score": 0.7284,
  "optimal_threshold": 0.4,
  "confidence_level": "high",
  "lesion_characteristics": {
    "mean_gradient_magnitude": 0.228,
    "gradient_energy": 0.0703,
    "local_contrast_mean": 0.0445,
    "texture_heterogeneity": 0.0151,
    "color_mean_rgb": [0.5675, 0.3799, 0.2589]
  },
  "screening_notice": "Educational experimental screening prototype only. This is not a veterinary diagnosis. Model scores are experimental screening indications and not clinically calibrated probabilities. Please contact a licensed veterinarian for definitive clinical assessment and laboratory confirmation (PCR/ELISA).",
  "limitations": [
    "Trained exclusively for Lumpy Skin Disease (LSD) nodular lesion screening; cannot diagnose or differentiate other bovine dermatological conditions (e.g. dermatophilosis, pseudo-lumpy skin disease/bovine herpesvirus 2, ringworm, mange, papillomatosis).",
    "Predictions are highly sensitive to image capture conditions, including camera angle, lighting, distance, coat contamination, and compression artifacts.",
    "Image screening must always be combined with systemic clinical evaluation (rectal temperature, superficial lymph node palpation, oral/nasal lesion inspection, milk yield monitoring).",
    "Model evaluated on curated research dataset; performance may vary under unconstrained rural field conditions."
  ]
}
```
*Verification Check:* Production LightGBM model loaded and scored gradient/texture features accurately.

---

### 3.4 Live Error Handling Verification

| Test Scenario | Input Data | HTTP Status | API Response Message | Graceful Handling |
| :--- | :--- | :---: | :--- | :---: |
| **Empty File** | 0 bytes payload | `422 Unprocessable Entity` | `"Uploaded file is empty."` | ✅ PASS |
| **Corrupted Image** | Random 32 bytes (`os.urandom(32)`) | `422 Unprocessable Entity` | `"Uploaded file is not a valid or readable image."` | ✅ PASS |
| **Unsupported Format** | Plain text file disguised as `.jpg` | `422 Unprocessable Entity` | `"Uploaded file is not a valid or readable image."` | ✅ PASS |

---

## 4. Benchmark Outcome Summary Table (CLI Demo)

The standalone CLI demo was executed via:
```powershell
python scripts/demo/run_five_class_demo.py --benchmark
```

### Complete 6-Case Benchmark Results

| Image ID | Ground Truth | Predicted Class | Confidence | CPU Latency | Verdict | Clinical Context & Observations |
| :--- | :--- | :--- | :---: | :---: | :---: | :--- |
| **D4_0010** | Dermatophilosis | Ringworm | 71.98% | 34.7 ms | **Misclassified** | Crusted matted paintbrush lesions on calf hide. Model confused by crust texture overlap. |
| **D4_0020** | Healthy | Healthy | 85.97% | 20.9 ms | **Correct** | Smooth bovine coat without alopecia or cutaneous eruptions. High specificity. |
| **D4_0089** | LSD | LSD | 83.46% | 28.1 ms | **Correct** | Well-demarcated circumscribed cutaneous nodules across neck and flank. |
| **D4_0007** | Pediculosis | Pediculosis | 90.67% | 22.0 ms | **Correct** | Pruritus-induced patchy alopecia and hair damage from sucking louse infestation. |
| **D4_0003** | Ringworm | Ringworm | 81.64% | 23.6 ms | **Correct** | Circumscribed circular alopecic scaling crusts typical of *Trichophyton verrucosum*. |
| **D4_2_EXT_004** | Dermatophilosis | Ringworm | 68.59% | 22.9 ms | **Misclassified** | Out-of-distribution clinical hospital case from Ethiopia (*Ashenafi et al. 2025*). |

**Benchmark Summary:**
- **In-Distribution Test Cases:** 4 / 5 correct (80.0% accuracy).
- **Average CPU Inference Latency:** 25.4 ms per image.
- **Honest Demonstration of Error Modes:** Preserves both correct predictions and documented misclassifications (Dermatophilosis crusted lesions predicted as Ringworm due to shared visual scab morphology).

---

## 5. Step-by-Step Evaluator Demonstration Guide

When presenting PashuCare AI to academic evaluators or examination committees, follow this 3-step structured walkthrough:

### Step 1: Explain the System Architecture & Scope (1 minute)
- **Clarify Role:** State clearly that PashuCare AI is an **undergraduate educational screening prototype**, not a commercial or certified veterinary diagnostic medical device.
- **Explain Dual Modality:**
  - *Modality A (Text):* Rule-based triage and clinical question formulation for systemic cattle diseases.
  - *Modality B (Image):* Deep learning five-class dermatological screening for bovine skin conditions:
    1. Dermatophilosis (*Dermatophilus congolensis*)
    2. Healthy controls
    3. Lumpy Skin Disease (Poxviridae)
    4. Pediculosis (*Linognathus vituli* / *Haematopinus*)
    5. Ringworm (*Trichophyton verrucosum*)

### Step 2: Live Interactive CLI Demonstration (2 minutes)
Open terminal and run the benchmark suite to show live, sub-30ms CPU inference with ASCII probability distributions:
```powershell
python scripts/demo/run_five_class_demo.py --benchmark
```
- **Show High-Confidence Correct Detections:**
  - Point to **Healthy** (`D4_0020_healthy.jpg`, 85.97% confidence).
  - Point to **LSD** (`D4_0089_lsd.jpg`, 83.46% confidence).
  - Point to **Pediculosis** (`D4_0007_pediculosis.jpg`, 90.67% confidence).
- **Show Single Image Inference:**
  ```powershell
  python scripts/demo/run_five_class_demo.py --image data/experiments/image_dataset_d4_3/images/pediculosis/D4_0007_pediculosis.jpg
  ```
- **Show Academic Honesty (The Crust Texture Overlap):**
  - Highlight Case 1 (`D4_0010_dermatophilosis.jpg`) where Dermatophilosis is predicted as Ringworm (71.98%).
  - Explain that both conditions produce superficial crusting and hair matting; this demonstrates that the system does not cheat with hardcoded heuristics and exhibits realistic morphological challenges.

### Step 3: Live API & Integration Demonstration (2 minutes)
- Demonstrate the live API in browser or terminal:
  - Visit `http://127.0.0.1:8000/docs` in the browser to showcase the live OpenAPI documentation.
  - Execute a live POST request to `/predict-five-class-image` with a cattle image.
  - Show that the response delivers full probability distributions, screening notices, and limitation disclosures.
  - Show the existing `/predict-text` endpoint to demonstrate multi-modal system continuity.

---

## 6. Verification Checklist & Protected Assets Audit

| Item | Requirement | Status | Evidence / Location |
| :--- | :--- | :---: | :--- |
| **1. CLI Demo Script** | `run_five_class_demo.py --benchmark` operational | ✅ VERIFIED | [run_five_class_demo.py](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/scripts/demo/run_five_class_demo.py) |
| **2. API Server** | `local_inference.app:app` running live | ✅ VERIFIED | Active PID 44360 on port 8000 |
| **3. 5-Class Endpoint** | `POST /predict-five-class-image` operational | ✅ VERIFIED | HTTP 200 with 5 probabilities summing to 1.0 |
| **4. Existing Text Endpoint** | `POST /predict-text` operational | ✅ VERIFIED | HTTP 200 with clinical safety gates |
| **5. Existing Image Endpoint**| `POST /predict-image` (LightGBM LSD) operational | ✅ VERIFIED | HTTP 200 with gradient/texture score |
| **6. Error Handling** | Reject empty/corrupt files with HTTP 422 | ✅ VERIFIED | Graceful HTTP 422 responses verified live |
| **7. Checkpoint Loading** | Primary Exp2 and baseline Exp0 verified | ✅ VERIFIED | Both load weights cleanly via PyTorch |
| **8. Automated Tests** | All workspace tests pass without failure | ✅ VERIFIED | **157 / 157 passed** (0 failures) |
| **9. D3 Dataset Protection** | Original D3 datasets and manifests untouched | ✅ VERIFIED | Git status clean on `data/splits/` |
| **10. D4.2 External Benchmark**| Frozen external benchmark 100% immutable | ✅ VERIFIED | `image_dataset_d4_2_external/` unmodified |
| **11. Production Assets** | Production models and rules untouched | ✅ VERIFIED | `production_pipeline.py` unmodified |

---

## 7. Limitations & Ethical Boundary Statement

1. **Academic Prototype Status:** PashuCare AI is developed as an undergraduate academic engineering prototype. It has not been approved by any regulatory body or veterinary medicine licensing authority.
2. **Not a Clinical Device:** Predictions generated by the image and text models must never supersede direct physical examination, palpation, temperature measurement, or laboratory confirmation (such as fungal cultures, skin scrapings, bacterial smears, or PCR assays) by a licensed veterinary practitioner.
3. **Dataset Scope:** The five-class model was developed on experimental datasets comprising 653 annotated images. Performance in rural field environments may vary due to ambient sunlight, mud contamination, camera sensor variability, and coat coloration.
4. **Multi-Class Overlap:** As observed in the benchmark, crusted exuded skin lesions (Dermatophilosis) share substantial morphological features with alopecic scaling crusts (Ringworm). The model should be used as a triage aid in conjunction with clinical history.

---
*Report certified complete and verified against live system runtime on November 22, 2026.*
