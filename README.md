# PashuCare AI — AI-Assisted Cattle Health Screening and Triage System

**Academic Capstone Project & Technical Implementation**  
**Target:** Final College Project Evaluation & Viva  
**Status:** Fully Integrated, Tested (162/162 Passed), and Demonstration-Ready

---

## 1. Project Overview

**PashuCare AI** is an intelligent, multimodal clinical decision-support and triage system engineered specifically for Indian dairy cattle (*Bos indicus*, crossbreds) and riverine buffaloes (*Bubalus bubalis*). Designed to bridge the critical gap between early symptom onset and certified veterinary intervention in rural communities, PashuCare AI combines:

1. **Natural Language Symptom Triage**: Parses free-text symptoms, maps them to a canonical 93-symptom vocabulary, applies distance-based Out-Of-Distribution (OOD) gating, and enforces 5-state clinical safety decision logic.
2. **Binary LSD Image Screening**: A calibrated 197-feature computer-vision pipeline with an optimized LightGBM classifier distinguishing Lumpy Skin Disease nodular lesions from non-nodular skin conditions.
3. **Five-Class Dermatological Classifier**: An experimental deep convolutional neural network (PyTorch ResNet-18) predicting probabilities across five distinct bovine skin classes: Healthy Control, Lumpy Skin Disease (LSD), Ringworm, Dermatophilosis, and Pediculosis.
4. **Standardized Clinical Guidance**: Evidence-based first-aid stabilization protocols, explicit fatal contraindication warnings, and 1-tap SOS connection to the National Animal Ambulance helpline (**1962**).

---

## 2. Main Features

- **Multimodal Health Check (Triage)**: Supports natural language text descriptions, fast clinical symptom pickers, and modular image screening.
- **5-State Safety Decision Gating**:
  - `CANDIDATE`: Clear statistical separation between differential diagnoses.
  - `AMBIGUOUS`: Close differential scores (<20% margin), triggering automatic follow-up distinguishing questions.
  - `INSUFFICIENT_INFORMATION`: Abstains from guessing when active canonical symptom count is too low (<2).
  - `EMERGENCY`: Automatic escalation for life-threatening acute presentations (systemic hemorrhage, severe asphyxiation).
  - `UNFAMILIAR_INPUT`: Rejects out-of-distribution inputs using Jaccard distance ($d > 0.70$) against canonical cases.
- **Dual-Tier Image Classification**:
  - Binary LightGBM screening for rapid nodule identification with a calibrated 0.4000 threshold.
  - Multiclass ResNet-18 with full 5-class horizontal probability distribution bars.
- **Farmer Dashboard**: Real-time herd health status, active alerts, upcoming vaccination schedules, and quick actions.
- **Animal Passports**: Complete individual bovine bio-data management (RFID tags, breed, age, lactation cycle, health records).
- **Vaccination Tracker**: Tracking national immunisation schedules (FMD, HS, BQ, Brucellosis, LSD) with automated overdue alerts.
- **Emergency Hub**: One-touch dialing to **1962** animal ambulance and nearest district veterinary hospitals.
- **Evaluation Demo Suite (Viva Mode)**: Pre-configured test scenarios across all three AI models for repeatable viva demonstration without manual input.

---

## 3. Technology Stack

- **Frontend**: React 18.3.1, Vite 8.3.8, Tailwind CSS 3.4.1, Lucide React Icons
- **Backend**: FastAPI 0.115+, Uvicorn 0.32+, Python 3.10+ (tested on Python 3.14)
- **Machine Learning / NLP**: scikit-learn 1.6+, LightGBM 4.5+, Joblib 1.4+, NumPy, pandas
- **Computer Vision / Deep Learning**: PyTorch 2.6+, Torchvision 0.19+, Pillow (PIL) 11.0+
- **Testing & Verification**: Pytest 9.1.1 (162 automated unit/integration tests)
- **Documentation**: python-docx 1.2.0 (consolidated Word report generator)

---

## 4. Project Directory Structure

```
PashuCare_AI/
|-- frontend/                                # Primary Migrated User-Facing Interface (Vite + React)
|   |-- src/
|   |   |-- components/                      # Modular UI components (triage, layout, animals)
|   |   |-- pages/                           # 8 navigation views (Dashboard, Triage, Demo, etc.)
|   |   |-- utils/pashucareApi.js            # Unified API service layer connecting to backend
|   |-- public/samples/                      # Verified sample presets (five_class & binary_lsd)
|   |-- package.json                         # Node dependencies (vite 8.3.8, react 18.3.1)
|   |-- tailwind.config.cjs                  # Editorial color tokens and typography configuration
|-- local_inference/                        # FastAPI Backend Application
|   |-- app.py                               # FastAPI routes, CORS, exception handlers
|   |-- symptom_extractor.py                 # Natural language symptom parsing & vocabulary
|   |-- text_inference_engine.py             # 5-state safety gating, OOD Jaccard, differential
|   |-- image_inference.py                   # 197-feature LightGBM binary LSD screening
|   |-- five_class_inference.py              # ResNet-18 PyTorch five-class image classifier
|-- models/                                 # Serialized Model Artifacts
|   |-- symptom/                             # Logistic regression & random forest artifacts
|   |-- image/                               # LightGBM binary model & 197-feature metadata
|   |   |-- experimental/                    # ResNet-18 checkpoints (five_class_resnet18_exp2.pt)
|-- data/                                   # Datasets & manifests (D3, D4, D4.1, D4.2, D4.3)
|-- tests/                                  # Automated Pytest suite (162 unit & integration tests)
|-- reports/                                # Documentation, audit reports, and screenshot evidence
|   |-- final/                               # Consolidated Word report & technical documentation
|   |-- image_experiments/phase_d4_6/        # Verification reports and UI screenshots
|-- docs/                                   # Documentation copy of project report
|-- scripts/                                # Reproducible utility and verification scripts
|-- requirements.txt                        # Python backend dependencies
|-- README.md                               # This documentation file
```

---

## 5. Installation Instructions

### Prerequisites
- Python 3.10 or higher (Python 3.14 fully supported)
- Node.js 18 or higher (Node 24 supported)
- Google Chrome (for automated browser testing)

### Step 1: Install Python Backend Dependencies
From the repository root:
```powershell
pip install -r requirements.txt
```

### Step 2: Install Frontend Dependencies
```powershell
cd frontend
npm install
cd ..
```

---

## 6. Backend Startup Instructions

Start the FastAPI local inference server:
```powershell
python -m uvicorn local_inference.app:app --host 127.0.0.1 --port 8000
```
- Server URL: **`http://127.0.0.1:8000`**
- Health Check: `GET http://127.0.0.1:8000/health` (Returns 200 OK)

---

## 7. Frontend Startup Instructions

Start the React development server:
```powershell
cd frontend
npm run dev
```
- Client Application URL: **`http://127.0.0.1:5173`**

---

## 8. API Documentation Location

Interactive Swagger API documentation and OpenAPI schemas are automatically available at:
- **Swagger UI**: [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)
- **ReDoc**: [http://127.0.0.1:8000/redoc](http://127.0.0.1:8000/redoc)

### Summary of Implemented REST Endpoints:
- `POST /extract-symptoms`: Extracts present, absent, and unmatched clinical tokens from text.
- `POST /predict-text`: 5-state safety gating, distance-based OOD check, and multiclass differential diagnosis.
- `POST /predict-image`: 197-feature LightGBM binary nodular lesion screening with calibrated 0.4000 threshold.
- `POST /predict-five-class-image`: ResNet-18 five-class bovine dermatological classification with full Softmax probabilities.

---

## 9. Model Descriptions

| Model Name | Architecture | Input Representation | Artifact Path | Primary Purpose |
| :--- | :--- | :--- | :--- | :--- |
| **Text Symptom Classifier** | Multiclass Logistic Regression (L2) | 93-feature binary symptom vector | `models/symptom/experimental/logistic_regression_candidate.joblib` | Differential diagnosis ranking with 5-state safety gating and OOD Jaccard distance check ($d > 0.70$). |
| **Binary LSD Screening** | LightGBM Decision Trees | 197 handcrafted color/texture features | `models/image/lightgbm_lsd_model.joblib` | Binary screening for Lumpy Skin Disease nodules (calibrated threshold: `0.4000`). |
| **Five-Class Skin Classifier** | ResNet-18 Deep CNN (Exp2) | $224 \times 224$ RGB normalized tensors | `models/image/experimental/five_class_resnet18_exp2.pt` | Multi-class dermatological triage across Healthy, LSD, Ringworm, Dermatophilosis, and Pediculosis. |

---

## 10. Demo Mode Instructions (Viva Ready)

A dedicated **Evaluation Demo / Viva Mode** has been integrated directly into the application:

1. Open `http://127.0.0.1:5173` in your browser.
2. Click **"Evaluation Demo"** in the sidebar navigation (or the masthead CTA on the Dashboard).
3. The demo suite contains three interactive tabs:
   - **Tab 1: Text Symptom Triage**: Choose from 5 realistic synthetic scenarios (Metabolic, Lameness, LSD, Diarrhea, Mild) and click *"Run Live Backend Inference"* to see live 5-state gating and differential probabilities.
   - **Tab 2: Binary LSD Screening**: Select from Screening-Positive, Screening-Negative, or Borderline scenarios and run live LightGBM inference.
   - **Tab 3: 5-Class Skin Classifier**: Select from all 5 classes (plus a verified domain shift case) and inspect live ResNet-18 probability bars.
4. **Safety Guarantee**: Demo scenarios run strictly in isolated memory and **never pollute** permanent herd records or local storage history. Click *"Reset Demo States"* at any time to clear.

---

## 11. Test Execution Commands

### Run Full Backend & Model Regression Suite
```powershell
python -m pytest tests/
```
- **Verified Result**: `162 passed in ~28 seconds` (0 failures, 0 regressions).

### Run Frontend Production Build
```powershell
cd frontend
npm run build
```
- **Verified Result**: `✓ built in ~3.8 seconds` with 0 build errors.

---

## 12. Known Limitations

- **External Benchmark Sample Size**: The frozen external field benchmark comprises 14 images. While valuable for revealing domain shift, larger multi-center cohorts are needed before production deployment.
- **Visual Domain Shift**: Direct harsh tropical sunlight or heavy manure/dirt encrustation can alter visual dermal textures, causing occasional bias toward Ringworm.
- **Hardware Footprint**: Current models run on local CPU server instances; mobile on-device quantization (TFLite / ONNX) is planned for future phases.
- **Field Biopsy vs Reference Label**: Dataset labels represent clinical veterinary consensus rather than PCR or fungal culture biopsy.

---

## 13. Clinical and Safety Disclaimer

> **IMPORTANT CLINICAL & LEGAL NOTICE:**  
> PashuCare AI is an **educational research prototype and preliminary clinical decision-support tool**. It is **NOT** a certified veterinary diagnosis under the Indian Veterinary Council Act (1984). Model scores represent statistical approximations and must never substitute for direct examination by a licensed veterinary professional. Do not administer prescription drugs or perform invasive medical procedures based solely on automated recommendations.

---

## 14. Consolidated Project Report & Technical Documentation

The complete, formal academic project report and comprehensive technical manual has been compiled into a single publication-grade Microsoft Word document:

📄 **[reports/final/PashuCare_AI_Project_Report_and_Technical_Documentation.docx](reports/final/PashuCare_AI_Project_Report_and_Technical_Documentation.docx)**  
*(Also backed up at `docs/` and root `PashuCare_AI_Project_Report_and_Technical_Documentation.docx`)*

### Contents of the Consolidated Word Document:
- **Part I: Formal Academic Project Report** (18 sections: Title page, Abstract, Introduction, Problem Statement, Objectives, Scope, Existing vs Proposed, System Architecture diagram, Functional Modules, AI/ML Components, Technology Stack, Dataset Description, Experimental Results with D4.3 comparison table, System Testing with embedded screenshot figures, Limitations, Future Scope, Conclusion, Academic References).
- **Part II: Technical Documentation** (10 sections: Technical Overview, Repository Structure, Installation & Setup, Running the Application, API Documentation with all 4 endpoints and sample payloads, Model Documentation, Frontend Integration, Testing & Troubleshooting, Deployment Considerations, Safety & Privacy Disclaimers).
