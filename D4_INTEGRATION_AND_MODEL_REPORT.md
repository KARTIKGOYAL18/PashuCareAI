# PashuCare AI — Phase D4: Accelerated Dataset Acquisition, Integration & Five-Class Model Development Report

**Phase:** D4  
**Date:** November 2026  
**Status:** Completed & Validated  
**Primary Artifacts:**
- Master Manifest: [`data/experiments/image_dataset_d4/manifests/d4_master_manifest.csv`](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/data/experiments/image_dataset_d4/manifests/d4_master_manifest.csv)
- Split Manifest: [`data/experiments/image_dataset_d4/manifests/d4_split_manifest.csv`](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/data/experiments/image_dataset_d4/manifests/d4_split_manifest.csv)
- Class Inventory: [`reports/image_experiments/phase_d4/d4_class_inventory.csv`](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_d4/d4_class_inventory.csv)
- Quarantine Register: [`reports/image_experiments/phase_d4/d4_quarantine_register.csv`](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_d4/d4_quarantine_register.csv)
- Trained Checkpoint: [`models/image_experiments/phase_d4/d4_resnet18_classifier.pt`](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/models/image_experiments/phase_d4/d4_resnet18_classifier.pt)
- Evaluation Metrics: [`reports/image_experiments/phase_d4/d4_evaluation_metrics.json`](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_d4/d4_evaluation_metrics.json)
- Test Predictions: [`reports/image_experiments/phase_d4/d4_test_predictions.csv`](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_d4/d4_test_predictions.csv)
- Test Suite: [`tests/test_phase_d4_integration_and_model.py`](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/tests/test_phase_d4_integration_and_model.py)

---

## 1. Executive Summary

Phase D4 successfully achieved the primary objective of breaking past slow, single-image manual harvesting and moving directly into **accelerated multi-source dataset consolidation and deep learning model development**. 

From an initial candidate staging pool of only 11 peer-reviewed images in Phase I3.3.6, Phase D4 expanded the experimental collection to **658 verified, high-quality, multi-source cattle dermatological images** across all five target clinical classes (`dermatophilosis`, `healthy`, `lsd`, `pediculosis`, and `ringworm`). 

Using this consolidated D4 dataset, we established a **leakage-free, group-aware split (70% train / 15% validation / 15% test)**, implemented an automated transfer learning pipeline using a **ResNet-18 backbone with class-frequency reweighting**, trained the experimental five-class classifier, and conducted an unbiased evaluation on the unseen test cohort.

All 147 tests across the entire repository pass with zero errors, and strict boundary rules ensured that production models and inference endpoints remained completely untouched.

```
       [Phase I3.3.6: 11 Staged Images]
                       +
   [Mayara Karen Open Dataset: 221 Images]
                       +
   [Curated Deduplicated D3 Pool: 426 Images]
                       │
                       ▼
       [D4 Dataset: 658 Validated Images]
     (Strict Group-Aware Stratified Split)
       ├── Train: 461 images (70%)
       ├── Val:    99 images (15%)
       └── Test:   98 images (15%)
                       │
                       ▼
    [ResNet-18 Five-Class Transfer Learning]
     (Weighted Cross-Entropy + AdamW + Cosine LR)
                       │
                       ▼
       [Unseen Test Cohort Evaluation]
     Overall Accuracy:  64.29%
     Balanced Accuracy: 55.79%
     Macro F1-Score:    56.26%
     Weighted F1-Score: 63.73%
```

---

## 2. Dataset Expansion & Multi-Source Composition

The D4 dataset combines three distinct, auditable data streams:

1. **Verified Academic Literature Acquisitions (11 Images):**
   - High-certainty clinical photographs with explicit diagnostic confirmation (PCR, direct microscopy, fungal culture).
   - Source papers: Dantas et al. (2018), Dagnaw et al. (2025), Akpo et al. (2021), Valcárcel et al. (2021), Wang et al. (2020), Dyląg et al. (2026), Gnat et al. (2024), Deschauers et al. (2024), Albuquerque et al. (2026).
2. **Mayara Karen Bovine Dermatological Dataset (221 Images):**
   - Discovered and downloaded via GitHub REST API under permissive **MIT License**.
   - Contributed 75 normal skin controls (healthy) and 146 confirmed Lumpy Skin Disease (LSD) field photographs.
3. **Curated Deduplicated Base Pool from D3 (426 Images):**
   - Filtered exclusively for non-duplicate images (`is_duplicate == False`) to avoid near-duplicate contamination.
   - Selected 94 Dermatophilosis, 91 Ringworm, 91 Pediculosis, 75 LSD, and 75 Healthy images to create a balanced multi-class distribution.

### Class Inventory & Split Distribution

| Clinical Class | Total Images | Train (70%) | Val (15%) | Test (15%) | Unique Groups/Animals | Dominant Sources |
| :--- | :---: | :---: | :---: | :---: | :---: | :--- |
| **Dermatophilosis** | 98 | 69 | 15 | 14 | 97 | Curated Base (94), Academic Literature (4) |
| **Healthy Controls** | 150 | 105 | 22 | 23 | 150 | Mayara Karen (75), Curated Base (75) |
| **Lumpy Skin Disease (LSD)** | 221 | 155 | 33 | 33 | 221 | Mayara Karen (146), Curated Base (75) |
| **Pediculosis** | 92 | 64 | 14 | 14 | 92 | Curated Base (91), Academic Literature (1) |
| **Ringworm** | 97 | 68 | 15 | 14 | 96 | Curated Base (91), Academic Literature (6) |
| **TOTAL** | **658** | **461** | **99** | **98** | **656** | **Multi-source consolidated** |

---

## 3. Data Integrity, Quarantine & Leakage Prevention

### A. Strict Quarantine Protocol
A total of **47 images** were screened and quarantined into `data/experiments/image_dataset_d4/quarantine/` with entries logged in [`d4_quarantine_register.csv`](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_d4/d4_quarantine_register.csv):
- **30 Images Quarantined (`non_target_parasitic`):**
  - Origin: Mayara Karen `Berne - Tratada` folder.
  - Reason: Etiologic agent is *Dermatobia hominis* (botfly warble/cutaneous myiasis), which is biologically and clinically distinct from *Pediculosis* (cattle lice infestation).
- **17 Images Quarantined (`low_resolution`):**
  - Extremely small image patches (<50×50 px) from extreme crops.

### B. Group-Aware Stratified Splitting
To prevent data leakage:
- Multi-panel figures and multiple photographs of the same animal/case (e.g., Brazilian Nelore heifer, Chinese calf ringworm case) share a single `group_id`.
- The split algorithm operates at the **group level**, guaranteeing that all panels or angles from an individual animal or herd stay entirely within either train, val, or test.
- Tested and verified: Zero image ID overlap and zero group ID overlap across all splits.

---

## 4. Five-Class Model Architecture & Training

### Architecture
- **Backbone:** Torchvision Pretrained `ResNet-18` (ImageNet initial weights).
- **Classifier Head:** Custom multi-class projection head:
  $$\text{Dropout}(p=0.3) \longrightarrow \text{Linear}(512, 5)$$
- **Target Classes:** `['dermatophilosis', 'healthy', 'lsd', 'pediculosis', 'ringworm']`

### Training Hyperparameters & Techniques
- **Loss Function:** Cross-Entropy Loss with inverse class-frequency balancing:
  $$w_c = \frac{N_{\text{train}}}{C \cdot N_c}$$
  - Class weights: `dermatophilosis`: 1.3362, `healthy`: 0.8781, `lsd`: 0.5948, `pediculosis`: 1.4406, `ringworm`: 1.3559.
- **Optimizer:** AdamW ($\text{lr} = 10^{-4}$, $\text{weight\_decay} = 0.01$).
- **Learning Rate Scheduler:** Cosine Annealing LR ($T_{\max} = 15$).
- **Data Augmentation:** Random resized crop ($224\times 224$), random horizontal flip ($p=0.5$), color jitter (brightness, contrast, saturation $\pm 0.15$), ImageNet normalization.
- **Model Selection Criterion:** Composite validation score $(\text{Balanced Accuracy} + \text{Macro F1}) / 2$.

### Training Trajectory

| Epoch | Train Loss | Train Acc | Val Loss | Val Acc | Val BalAcc | Val Macro F1 | Checkpoint Status |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :--- |
| 01 | 1.4748 | 39.91% | 1.0745 | 56.57% | 53.85% | 50.86% | Saved best |
| 02 | 0.7780 | 73.97% | 0.9453 | 59.60% | 54.67% | 54.05% | Saved best |
| 03 | 0.5089 | 85.25% | 0.8613 | 65.66% | 61.64% | 61.71% | Saved best |
| 06 | 0.1674 | 95.88% | 0.8820 | 69.70% | 64.76% | 65.11% | Saved best |
| 09 | 0.0834 | 98.70% | 0.8318 | 71.72% | 65.55% | 65.83% | Saved best |
| **12** | **0.0622** | **99.57%** | **0.8509** | **71.72%** | **65.97%** | **66.50%** | **Selected Best Checkpoint** |
| 15 | 0.0447 | 99.78% | 0.8849 | 71.72% | 65.97% | 66.26% | Final Epoch |

---

## 5. Quantitative Test Evaluation & Confusion Matrix

The model was loaded from the best checkpoint (Epoch 12) and evaluated strictly on the **unseen D4 test split (98 images)**.

### Master Test Metrics
- **Overall Accuracy:** **64.29%** (63 / 98)
- **Balanced Accuracy:** **55.79%**
- **Macro Precision:** **58.72%**
- **Macro Recall:** **55.79%**
- **Macro F1-Score:** **56.26%**
- **Weighted F1-Score:** **63.73%**

### Per-Class Performance Breakdown

| Class | Precision | Recall | F1-Score | Support (N) | Clinical Visual Characteristics |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **Healthy** | **83.33%** | **86.96%** | **85.11%** | 23 | Smooth coat, absence of circumscribed nodular or alopecoid lesions |
| **LSD** | **77.78%** | **84.85%** | **81.16%** | 33 | Raised, circumscribed cutaneous nodules across neck, flank, and perineum |
| **Ringworm** | **70.00%** | **50.00%** | **58.33%** | 14 | Circular, asbestos-like greyish-white crusts and localized alopecia |
| **Dermatophilosis** | 25.00% | 35.71% | 29.41% | 14 | Paintbrush-like crusts and exudative matting along dorsal midline |
| **Pediculosis** | 37.50% | 21.43% | 27.27% | 14 | Diffuse pruritic alopecia, excoriations, and tiny ectoparasite speckles |

### Confusion Matrix

```
True \ Pred      dermatophilosis   healthy   lsd   pediculosis   ringworm
dermatophilosis        5              0       4         4           1
healthy                1             20       1         0           1
lsd                    2              3      28         0           0
pediculosis            6              1       3         3           1
ringworm               6              0       0         1           7
```

---

## 6. Clinical & Technical Error Analysis

1. **Robust Discriminating Power on Distinctive Morphologies:**
   - **Healthy** achieved **85.1% F1** and **LSD** achieved **81.2% F1**, confirming that the model easily distinguishes unaffected skin from prominent nodular pathology.
   - 28 out of 33 true LSD test cases were correctly classified, demonstrating strong diagnostic sensitivity (84.85%).
2. **Ringworm Shows High Specificity:**
   - Ringworm achieved **70.0% Precision**, meaning when the model predicts ringworm, it is correct 70% of the time. Recall was 50.0%, with misclassifications primarily going to Dermatophilosis due to overlapping superficial crusted patches.
3. **Clinical Overlap between Dermatophilosis and Pediculosis:**
   - Superficial crusted exudative dermatitis (Dermatophilosis) and severe lice excoriations (Pediculosis) frequently present with very similar macro-level patterns: patchy hair loss, dried serous crusts, and scabs.
   - At standard $224\times 224$ image resolutions, microscopic ectoparasites (lice eggs/nits) are physically invisible without macro-lens magnification. This accounts for the confusion between these two minority classes.
4. **Actionable Direction for Clinical Improvement:**
   - Future dataset refinement will benefit significantly from integrating close-up macro photography for pediculosis, and multi-spectral or higher-resolution inputs ($384\times 384$ or $512\times 512$) for dermatophilosis crust detection.

---

## 7. Protection Boundaries & Verification Summary

All operations adhered strictly to safety constraints:
1. **Production Assets Protected:**
   - Production LightGBM model (`models/image_experiments/phase6/lumpy_skin_lightgbm.joblib`) was untouched.
   - Production inference endpoints (`/predict-text`, `/predict-image`) remain fully functional and backwards compatible.
   - Frozen D3 dataset and Phase 6 benchmarks remain unmodified.
2. **Full Workspace Test Health:**
   - Pytest execution: **147 passed in 46.23s** across the entire workspace (100% success rate).
   - Dedicated Phase D4 test suite (`tests/test_phase_d4_integration_and_model.py`): **8 passed in 3.39s**.

---

## 8. Conclusion & Next Steps

Phase D4 has successfully delivered an auditable, high-volume multi-source dataset (658 images) and a working, defensible five-class cattle dermatological classifier for this undergraduate prototype. 

### Ready for Next Phase:
- **Phase D4.1 (Mendeley Drop-In Ingestion):** Whenever the 1.4 GB Mendeley benchmark archive is downloaded into the workspace, the pre-built script `scripts/research/ingest_mendeley_benchmark.py` can immediately unpack and ingest 400+ additional Healthy and LSD benchmark images into D4.2.
- **Phase D4.2 (Model Refinement & Hyperparameter Tuning):** Fine-tune backbones (e.g. EfficientNet-B0 or ConvNeXt-Tiny) with higher resolution inputs ($384\times 384$) to enhance minority-class crust differentiation.
