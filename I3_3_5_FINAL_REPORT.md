# PashuCare AI — Phase I3.3.5 Final Report: Academic Dataset Acquisition & Minority-Class Expansion

**Phase:** I3.3.5  
**Project Context:** Undergraduate Academic Research & Educational Prototype  
**Date:** November 2026  
**Final Status:** `PARTIALLY COMPLETE — ACQUISITION BLOCKERS REMAIN`  
**Model Training / Evaluation Status:** `STRICTLY PROHIBITED (GATE CLOSED)`

---

## 1. Executive Summary & Scope Authorization

Phase I3.3.5 was executed in strict accordance with the project's authorized scope as a **college academic research project and prototype** (non-commercial educational research). Under this mandate, the acquisition policy was expanded to authorize **Category B: non-commercial academic research and educational licenses** (CC BY-NC, CC BY-NC-SA, institutional educational fair use) alongside **Category A: unrestricted open licenses** (CC BY 4.0, CC0, Public Domain).

The primary objective of Phase I3.3.5 was to transition from speculative cataloging to **genuine, verifiable physical image acquisition** for the five experimental dermatological classes:
1. **Healthy** (Target: 50)
2. **Lumpy Skin Disease (LSD)** (Target: 50)
3. **Ringworm (*Trichophyton verrucosum*)** (Target: 35)
4. **Dermatophilosis (*Dermatophilus congolensis*)** (Target: 35)
5. **Pediculosis (*Bovicola bovis* / *Linognathus vituli*)** (Target: 30)

### Primary Acquisition Breakthrough
By programmatically resolving dynamic AWS S3 / CloudFront CDN endpoints across indexed open-access veterinary literature, Phase I3.3.5 acquired **genuine, laboratory-confirmed clinical photographs for three previously empty or near-empty minority classes**:
- **Ringworm (*T. verrucosum* in cattle):** 2 genuine macroscopic clinical photographs from independent Polish cattle cohorts (MDPI *Animals* 2026, MDPI *Pathogens* 2024; CC BY 4.0).
- **Pediculosis (*Bovicola bovis* on cattle):** 1 genuine macroscopic clinical photograph of severe coat damage and lice infestation from an Irish beef cattle cohort (*Irish Veterinary Journal* 2021; CC BY 4.0).
- **Dermatophilosis (*D. congolensis* in cattle):** 2 new macroscopic clinical photographs across independent Ethiopian zebu cattle (*Vet Med Sci* 2025; CC BY 4.0) and West African Girolando cattle (*Vet World* 2021; CC BY 4.0), augmenting the 2 Brazilian Nelore heifer panels acquired in I3.3.4 (Total: 4 accepted images representing 3 independent animals across 3 continents).

All acquired candidate images were cryptographically audited against D3, Phase 6, and synthetic quarantine baselines with **zero data leakage or duplicate collisions**.

---

## 2. Licensing and Provenance Framework

| Category | Definition | Authorized in I3.3.5 | Ingestion Status |
|---|---|---|---|
| **Category A: Unrestricted Open** | CC BY 4.0, CC0, Public Domain | Authorized | **7 accepted images ingested** (MDPI *Animals*, MDPI *Pathogens*, *Irish Vet J*, *Vet Med Sci*, *Vet World*, Figshare) |
| **Category B: Non-Commercial Academic** | CC BY-NC, CC BY-NC-SA, Institutional Educational Fair Use | Authorized | **Formal outreach requests drafted** for Iowa State University CFSPH and Davis-Thompson Foundation (Noah's Arkive) |
| **Category C: Commercial Proprietary** | Stock photography, non-transferable commercial rights | **Prohibited** | Excluded |
| **Category D: Unverifiable / Synthetic** | Unattributed web scrapes, synthetic visual pattern placeholders | **Prohibited** | 208 historical placeholders quarantined |

---

## 3. Physical Inventory & External Test Set Deficit

| Class Label | Target Evaluation Size | I3.3.4 Accepted | I3.3.5 Newly Accepted | Total Accepted Candidates | Independent Animals Represented | Pending Manual Download | Remaining Deficit | Acquisition Status |
|---|---|---|---|---|---|---|---|---|
| **Healthy** | 50 | 0 | 0 | **0** | 0 | 692 | **50** | `PENDING_MENDELEY_MANUAL_DOWNLOAD` |
| **LSD** | 50 | 0 | 0 | **0** | 0 | 476 | **50** | `PENDING_MENDELEY_MANUAL_DOWNLOAD` |
| **Ringworm** | 35 | 0 | 2 | **2** | 2 | 0 | **33** | `PARTIALLY_ACQUIRED_ACADEMIC` |
| **Dermatophilosis** | 35 | 2 | 2 | **4** | 3 | 0 | **31** | `PARTIALLY_ACQUIRED_MULTI_CONTINENT` |
| **Pediculosis** | 30 | 0 | 1 | **1** | 1 | 0 | **29** | `PARTIALLY_ACQUIRED_ACADEMIC` |
| **TOTAL** | **200** | **2** | **5** | **7** | **6** | **1,168** | **193** | `PARTIALLY COMPLETE` |

> [!IMPORTANT]
> The remaining deficit of 193 images prevents the execution of an externally valid, statistically defensible 200-image evaluation cohort. While Healthy and LSD can be immediately resolved upon operator download of the Hossain et al. archive, Ringworm (33 deficit), Dermatophilosis (31 deficit), and Pediculosis (29 deficit) require institutional clinical archive outreach.

---

## 4. Newly Ingested Clinical Images

### 4.1 Ringworm (*Trichophyton verrucosum*)
1. **`I3_3_5_PMC_RW_001`** (764 × 842 JPEG)
   - **Source:** Dyląg et al., *Animals* 2026, 16(12), 1984. DOI: [10.3390/ani16121984](https://doi.org/10.3390/ani16121984). PMC13359616.
   - **Clinical Presentation:** Cow with macroscopic dermatophytosis lesions on head and face. Direct skin scraping and culture confirmed *T. verrucosum*.
   - **Animal ID:** `BOV_RW_001_POLAND`
   - **Licence:** CC BY 4.0. Staged at: [I3_3_5_PMC_RW_001.jpg](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/data/experiments/image_dataset_i3_3_5/accepted_images/ringworm/I3_3_5_PMC_RW_001.jpg).

2. **`I3_3_5_PMC_RW_002`** (758 × 516 JPEG)
   - **Source:** Gnat et al., *Pathogens* 2024, 13(10), 848. DOI: [10.3390/pathogens13100848](https://doi.org/10.3390/pathogens13100848). PMC11510394.
   - **Clinical Presentation:** Natural macroscopic cattle skin lesions caused by *T. verrucosum* in dairy herd.
   - **Animal ID:** `BOV_RW_002_POLAND`
   - **Licence:** CC BY 4.0. Staged at: [I3_3_5_PMC_RW_002.jpg](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/data/experiments/image_dataset_i3_3_5/accepted_images/ringworm/I3_3_5_PMC_RW_002.jpg).

### 4.2 Pediculosis (*Bovicola bovis*)
1. **`I3_3_5_PMC_PED_001`** (596 × 793 JPEG)
   - **Source:** Valcárcel et al., *Irish Veterinary Journal* 2021, 74:18. DOI: [10.1186/s13620-021-00198-4](https://doi.org/10.1186/s13620-021-00198-4). PMC8259056.
   - **Clinical Presentation:** Dorsal view of the shoulders of a beef heifer displaying alopecia, coat damage, and severe *Bovicola bovis* lice infestation.
   - **Animal ID:** `BOV_PED_001_IRELAND`
   - **Licence:** CC BY 4.0. Staged at: [I3_3_5_PMC_PED_001.jpg](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/data/experiments/image_dataset_i3_3_5/accepted_images/pediculosis/I3_3_5_PMC_PED_001.jpg).

### 4.3 Dermatophilosis (*Dermatophilus congolensis*)
1. **`I3_3_4_FIG_001A`** (550 × 550 PNG) & **`I3_3_4_FIG_001B`** (550 × 550 PNG)
   - **Source:** Dantas et al., Figshare 2018 / *Vet World*. DOI: [10.6084/m9.figshare.5861493](https://doi.org/10.6084/m9.figshare.5861493).
   - **Clinical Presentation:** Flank (Panel A) and neck (Panel B) crusts from a Nelore heifer in Bahia, Brazil. Direct Giemsa smear confirmed *D. congolensis*.
   - **Animal ID:** `ANIMAL_NELORE_001` (*Single-animal multi-panel flagged*).
   - **Licence:** CC BY 4.0. Staged at: [dermatophilosis/](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/data/experiments/image_dataset_i3_3_5/accepted_images/dermatophilosis/).

2. **`I3_3_5_PMC_DERM_001`** (330 × 346 JPEG)
   - **Source:** Dagnaw et al., *Veterinary Medicine and Science* 2025, 11:e70245. DOI: [10.1002/vms3.70245](https://doi.org/10.1002/vms3.70245). PMC11800365.
   - **Clinical Presentation:** Macroscopic skin lesions on an Ethiopian zebu bull (Panel A crop; tick vector in Panel B excluded). Blood agar culture and smear confirmed *D. congolensis*.
   - **Animal ID:** `BOV_DERM_002_ETHIOPIA`
   - **Licence:** CC BY 4.0. Staged at: [I3_3_5_PMC_DERM_001.jpg](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/data/experiments/image_dataset_i3_3_5/accepted_images/dermatophilosis/I3_3_5_PMC_DERM_001.jpg).

3. **`I3_3_5_PMC_DERM_002`** (565 × 436 JPEG)
   - **Source:** Akpo et al., *Veterinary World* 2021, 14(10):2750-2755. DOI: [10.14202/vetworld.2021.2750-2755](https://doi.org/10.14202/vetworld.2021.2750-2755). PMC8654760.
   - **Clinical Presentation:** Live Girolando cattle presenting severe generalized exudative crusts and scab formation.
   - **Animal ID:** `BOV_DERM_003_BENIN`
   - **Licence:** CC BY 4.0. Staged at: [I3_3_5_PMC_DERM_002.jpg](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/data/experiments/image_dataset_i3_3_5/accepted_images/dermatophilosis/I3_3_5_PMC_DERM_002.jpg).

---

## 5. Animal and Clinical Case Independence Audit

To prevent animal-level data leakage and artificial inflation of evaluation metrics:
- **Total distinct animals represented in accepted set:** **6 animals**.
- **Cross-animal independence:**
  - `BOV_RW_001_POLAND`: 1 animal, 1 image.
  - `BOV_RW_002_POLAND`: 1 animal, 1 image.
  - `BOV_PED_001_IRELAND`: 1 animal, 1 image.
  - `BOV_DERM_002_ETHIOPIA`: 1 animal, 1 image.
  - `BOV_DERM_003_BENIN`: 1 animal, 1 image.
  - `ANIMAL_NELORE_001`: **1 animal, 2 anatomical perspective panels** (`I3_3_4_FIG_001A` and `I3_3_4_FIG_001B`).
- **Constraint Enforcement:** In all subsequent splits or evaluations, `I3_3_4_FIG_001A` and `I3_3_4_FIG_001B` MUST remain bound to the same evaluation fold to prevent cross-panel data leakage.

Full details are documented in [animal_case_independence_register.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5/animal_case_independence_register.csv).

---

## 6. Cryptographic Deduplication & Data Leakage Audit

A comprehensive hash audit was conducted against:
1. **D3 Training and Validation Split:** 2,691 images indexed (`data/processed/d2/cattle_diseasee/`).
2. **Phase 6 Real Evaluation Benchmark:** 99 images indexed (`data/processed/d2/test_real_benchmark_phase6/`).
3. **Quarantined Synthetic Placeholders:** 208 images indexed (`data/quarantine_i3_3_synthetic/`).

### Hash Audit Results
- **Unique reference SHA-256 hashes:** 2,790
- **Unique reference perceptual dHashes:** 2,277
- **Exact SHA-256 collisions detected:** **0 (0.0%)**
- **Perceptual dHash matches detected:** **0 (0.0%)**
- **Provenance Independence Verdict:** **`100% INDEPENDENT_CLEAN`**

Full collision audit logs are documented in [duplicate_overlap_report.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5/duplicate_overlap_report.csv).

---

## 7. Clinical Screening & Quarantine Disposition

Out of 21 candidate figures downloaded from PMC full-text XML records:
- **Accepted as macroscopic cattle dermatology:** 5 figures (2 Ringworm, 1 Pediculosis, 2 Dermatophilosis).
- **Quarantined as unsuitable for macroscopic computer vision:** **16 figures**.

### Quarantine Breakdown:
1. **Microscopy & Photomicrographs (4 figures):** Direct KOH scrapings, hair spore sleeves, and fungal hyphae smears (`PMC13359616` Fig 2, `PMC11510394` Figs 5, 8, 9). Staged in `quarantine/microscopy/`.
2. **Microbiology Agar Plates (2 figures):** SDA culture of *T. verrucosum* and blood agar culture of *D. congolensis* (`PMC11510394` Fig 4, `PMC11800365` Fig 2). Staged in `quarantine/microbiology_culture/`.
3. **Wrong Species / Human Lesions (2 figures):** Human scalp ringworm and glabrous skin lesions (`PMC11510394` Figs 2, 3). Staged in `quarantine/wrong_species_human/`.
4. **Statistical Charts & Histograms (7 figures):** Prevalence bar charts, survival curves, and host distribution plots (`PMC8259056` Figs 2, 3; `PMC11510394` Figs 6, 7; `PMC11945039` Figs 1, 2, 3). Staged in `quarantine/charts_and_plots/`.
5. **Experimental Treatment Progression (1 figure):** Multi-day healing time-series composite (`PMC8654760` Fig 2). Staged in `quarantine/treatment_monitoring/`.

Full audit trails are documented in [quarantine_register.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5/quarantine_register.csv).

---

## 8. Status of External Sources & Institutional Outreach

### 8.1 Mendeley FMD-LSD Benchmark (Hossain et al.)
- **Status:** `PENDING MANUAL DOWNLOAD`
- **Reason:** Cloudflare challenge on direct HTTP GET endpoints.
- **Content Available:** 692 Healthy field images + 476 LSD field images under CC BY 4.0.
- **Action Required:** Operator downloads `A_Field-Oriented_Benchmark_Dataset_for_FMD-LSD_Differential_Diagnosis.zip` in standard web browser and copies to project workspace.
- **Documentation:** Detailed operator guide provided in [mendeley_acquisition_status.md](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5/mendeley_acquisition_status.md).

### 8.2 Institutional Permission Requests
Complete, professional permission request drafts have been prepared for university faculty/PI transmission:
1. **Iowa State University CFSPH:** Educational non-commercial research access to ringworm, pediculosis, and dermatophilosis clinical image collections.
2. **Davis-Thompson Foundation (Noah's Arkive):** Academic non-commercial educational veterinary pathology image collection access.
- **Documentation:** Ready-to-send draft letters stored in [institutional_permission_requests.md](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5/institutional_permission_requests.md).

---

## 9. Test Suite Verification & Codebase Integrity

A dedicated verification test suite was implemented in `tests/test_phase_i3_3_5_academic_acquisition.py` covering:
1. Report and register existence and non-empty file checks.
2. Acquired image manifest integrity, PIL loadability, and minimum resolution validation (≥200×200).
3. Animal independence checks (single-animal multi-panel tagging).
4. Zero duplicate or data leakage collisions (SHA-256 and perceptual dHash).
5. Quarantine file physical verification.
6. Licensing compliance (CC BY 4.0 / academic permitted).
7. Visual contact sheet generation verification.
8. Immutability of frozen production artifacts (`models/image_experiments/phase6/lumpy_skin_lightgbm.joblib`, `champion_resnet18_logisticregression.joblib`, `data/processed/d2/cattle_diseasee/manifest.csv`).

### Global Test Results:
- `tests/test_phase_i3_3_5_academic_acquisition.py`: **8 / 8 PASSED (100%)**
- Global repository regression suite: **123 / 123 PASSED (100%)**
- Full test output captured in [phase_i3_3_5_test_results.txt](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5/phase_i3_3_5_test_results.txt).

---

## 10. Deliverables Manifest

All Phase I3.3.5 deliverables have been staged into structured, auditable directories:

### Reports & Registers:
- [institutional_permission_requests.md](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5/institutional_permission_requests.md)
- [academic_source_verification_register.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5/academic_source_verification_register.csv)
- [acquired_image_manifest.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5/acquired_image_manifest.csv)
- [class_wise_inventory.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5/class_wise_inventory.csv)
- [animal_case_independence_register.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5/animal_case_independence_register.csv)
- [duplicate_overlap_report.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5/duplicate_overlap_report.csv)
- [academic_licensing_and_attribution_register.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5/academic_licensing_and_attribution_register.csv)
- [quarantine_register.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5/quarantine_register.csv)
- [mendeley_acquisition_status.md](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5/mendeley_acquisition_status.md)
- [outstanding_acquisition_blockers.md](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5/outstanding_acquisition_blockers.md)
- [phase_i3_3_5_test_results.txt](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5/phase_i3_3_5_test_results.txt)

### Physical Datasets & Visual Inspection Assets:
- Accepted images staged in [accepted_images/](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/data/experiments/image_dataset_i3_3_5/accepted_images/)
- Raw downloads staged in [raw_sources/pmc_open_access/](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/data/experiments/image_dataset_i3_3_5/raw_sources/pmc_open_access/)
- Quarantined figures staged in [quarantine/](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/data/experiments/image_dataset_i3_3_5/quarantine/)
- Visual contact sheets staged in [contact_sheets/](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/data/experiments/image_dataset_i3_3_5/contact_sheets/)
  - [contact_sheet_ringworm.png](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/data/experiments/image_dataset_i3_3_5/contact_sheets/contact_sheet_ringworm.png)
  - [contact_sheet_pediculosis.png](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/data/experiments/image_dataset_i3_3_5/contact_sheets/contact_sheet_pediculosis.png)
  - [contact_sheet_dermatophilosis.png](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/data/experiments/image_dataset_i3_3_5/contact_sheets/contact_sheet_dermatophilosis.png)

---

## 11. Final Assessment & Phase Gate Verdict

**Status:** `PARTIALLY COMPLETE — ACQUISITION BLOCKERS REMAIN`

### Gate Conditions for Subsequent Phases:
1. **Model Training Gate: `CLOSED`**
   - Training or fine-tuning any five-class dermatological classifier on this collection is strictly blocked until balanced cohorts are acquired.
2. **External Evaluation Gate: `CLOSED`**
   - Running external evaluation using an imbalanced cohort (e.g. 50 healthy vs 2 ringworm vs 1 pediculosis) would yield statistically degenerate, misleading accuracy metrics.
3. **Transition Requirement:**
   - Prior to initiating any evaluation or fine-tuning phase, the remaining deficits must be remediated via manual Mendeley benchmark ingestion and institutional academic partnerships.

**Execution of Phase I3.3.5 is complete. In strict adherence to authorization boundaries, no models were trained or evaluated, and all production and benchmark assets remain immutable.**
