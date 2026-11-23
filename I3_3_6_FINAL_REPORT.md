# PashuCare AI — Phase I3.3.6 Final Report: Mendeley Integration, Academic Image Acquisition & Dataset Consolidation

**Phase:** I3.3.6  
**Project Context:** Undergraduate College Project & Non-Commercial Academic Prototype  
**Date:** November 2026  
**Final Status:** `PARTIALLY COMPLETE — ACQUISITION BLOCKERS REMAIN`  
**Model Training / Evaluation Status:** `STRICTLY PROHIBITED (GATES REMAIN CLOSED)`

---

## 1. Executive Summary & Authorization Scope

Phase I3.3.6 was executed to transition PashuCare AI from source verification to meaningful dataset engineering and consolidation for the five-class dermatological image classifier:
1. **Healthy** (Target: 50)
2. **Lumpy Skin Disease (LSD)** (Target: 50)
3. **Ringworm (*Trichophyton verrucosum* / bovine dermatophytes)** (Target: 35)
4. **Dermatophilosis (*Dermatophilus congolensis*)** (Target: 35)
5. **Pediculosis (*Bovicola bovis* / *Linognathus vituli*)** (Target: 30)

In strict compliance with project authorization boundaries, **no model training, fine-tuning, threshold optimization, or external model evaluation was performed**. All frozen production models, Phase 6 LSD screening models, baseline D3 splits, inference endpoints, and frontend components remain 100% immutable.

### Primary Achievements in Phase I3.3.6
1. **Staging Architecture Established:** Created an isolated, auditable candidate staging structure in `data/experiments/image_dataset_i3_3_6/` preserving raw sources, processed candidate folders, machine-readable manifests, contact sheets, and quarantine partitions.
2. **Ringworm Minority-Class Expansion:** Acquired, screened, and staged **4 new genuine macroscopic bovine ringworm candidate images** from peer-reviewed open-access journals (*Animals* 2024, *BMC Vet Res* 2020, *Vet Res Commun* 2026; CC BY 4.0), expanding the accepted Ringworm candidate pool from 2 to **6 images** (representing 5 independent herds/cases).
3. **Consolidated Candidate Dataset:** Consolidated **11 physical images representing 9 independent animals/cases** across Ringworm (6 images), Dermatophilosis (4 images), and Pediculosis (1 image) into a unified, provenance-preserving candidate manifest.
4. **Mendeley Benchmark Integration Protocol:** Completed a formal verification audit of the canonical Hossain et al. Mendeley dataset ([`10.17632/ggpwpscjvm.1`](https://doi.org/10.17632/ggpwpscjvm.1)). Due to Cloudflare anti-bot challenges on automated HTTP endpoints, the archive is designated as `PENDING MANUAL DOWNLOAD (BROWSER INTERACTION REQUIRED)`. Detailed screening protocols and an automated extraction pipeline have been pre-configured.
5. **Cryptographic Deduplication:** Audited all candidate images against 3,681 unique reference SHA-256 hashes and 2,715 perceptual dHashes across D3 (train/val/test), Phase 6 real benchmark, historical synthetic quarantine, and academic quarantine, confirming **0 exact collisions and 0 perceptual collisions**.
6. **Codebase Integrity:** Global test suite executed with **139 / 139 tests passing (100%)** with zero regressions.

---

## 2. Consolidated Candidate Dataset Overview

All 11 candidate images physically reside in `data/experiments/image_dataset_i3_3_6/processed_candidates/` and are fully indexed in [consolidated_candidate_image_manifest.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_6/consolidated_candidate_image_manifest.csv):

| Image ID | Disease Class | Source Publication | Species & Breed | Anatomical View | Diagnostic Proof | Resolution | Licence |
|---|---|---|---|---|---|---|---|
| **`I3_3_5_PMC_RW_001`** | Ringworm | *Animals* 2026 (10.3390/ani16131984) | *Bos taurus* (Cow) | Head / Face | 10% KOH microscopy + DTM culture (*T. verrucosum*) | 764 × 842 | CC BY 4.0 |
| **`I3_3_5_PMC_RW_002`** | Ringworm | *Pathogens* 2024 (10.3390/pathogens13100848) | *Bos taurus* (Cattle) | Trunk / Neck | Mycological identification & herd lesions (*T. verrucosum*) | 758 × 516 | CC BY 4.0 |
| **`I3_3_6_PMC_RW_003`** | Ringworm | *Animals* 2024 (10.3390/ani14030390) | *Bos taurus* (Calf) | Head / Neck | PCR + fungal culture confirmation (*T. verrucosum*) | 250 × 280 | CC BY 4.0 |
| **`I3_3_6_PMC_RW_004`** | Ringworm | *BMC Vet Res* 2020 (10.1186/s12917-020-02403-6) | *Bos taurus* (Cattle) | Neck / Dewlap | ITS sequencing + SDA fungal culture (*T. verrucosum*) | 393 × 393 | CC BY 4.0 |
| **`I3_3_6_PMC_RW_005`** | Ringworm | *BMC Vet Res* 2020 (10.1186/s12917-020-02403-6) | *Bos taurus* (Cattle) | Head / Cheek | ITS sequencing + SDA fungal culture (*T. verrucosum*) | 394 × 393 | CC BY 4.0 |
| **`I3_3_6_PMC_RW_006`** | Ringworm | *Vet Res Commun* 2026 (10.1007/s11259-026-11619-0) | *Bos taurus* (Calf) | Forehead / Eye | 20% KOH exam + Mycosel culture + ITS seq (*Paraphyton cookei*) | 1600 × 712 | CC BY 4.0 |
| **`I3_3_5_PMC_PED_001`** | Pediculosis | *Irish Vet J* 2021 (10.1186/s13620-021-00198-y) | *Bos taurus* (Beef Heifer) | Dorsal Shoulders | Dissection microscopy key morphology (*Bovicola bovis*) | 596 × 793 | CC BY 4.0 |
| **`I3_3_4_FIG_001A`** | Dermatophilosis | *Figshare / Vet World* 2018 (10.6084/m9.figshare.5861493) | *Bos indicus* (Nelore Heifer) | Lateral Flank | Giemsa cytological smear parallel cocci (*D. congolensis*) | 550 × 550 | CC BY 4.0 |
| **`I3_3_4_FIG_001B`** | Dermatophilosis | *Figshare / Vet World* 2018 (10.6084/m9.figshare.5861493) | *Bos indicus* (Nelore Heifer) | Lateral Neck | Giemsa cytological smear parallel cocci (*D. congolensis*) | 550 × 550 | CC BY 4.0 |
| **`I3_3_5_PMC_DERM_001`** | Dermatophilosis | *Vet Med Sci* 2025 (10.1002/vms3.70245) | *Bos indicus* (Zebu Bull) | Dorsum / Wither | Blood agar culture + Giemsa tram-track hyphae (*D. congolensis*) | 330 × 346 | CC BY 4.0 |
| **`I3_3_5_PMC_DERM_002`** | Dermatophilosis | *Vet World* 2021 (10.14202/vetworld.2021.2750-2756) | *Bos taurus x indicus* (Girolando Cow) | Costal / Trunk | Direct smear branching filaments (*D. congolensis*) | 565 × 436 | CC BY 4.0 |

---

## 3. Class-Wise Inventory & Remaining Target Deficits

| Disease Class | Target Sample Size | Existing Accepted Files | Newly Accepted Files | Total Accepted Candidates | Independent Animals | Independent Cases | Pending Review | Remaining Target Deficit | Current Status |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---|
| **Healthy** | 50 | 0 | 0 | **0** | 0 | 0 | 0 | **50** | `PENDING_MENDELEY_MANUAL_DOWNLOAD` |
| **LSD** | 50 | 0 | 0 | **0** | 0 | 0 | 0 | **50** | `PENDING_MENDELEY_MANUAL_DOWNLOAD` |
| **Ringworm** | 35 | 2 | 4 | **6** | 5 | 5 | 0 | **29** | `PARTIALLY_ACQUIRED_EXPANDED` |
| **Dermatophilosis** | 35 | 4 | 0 | **4** | 3 | 3 | 0 | **31** | `PARTIALLY_ACQUIRED_MULTI_CONTINENT` |
| **Pediculosis** | 30 | 1 | 0 | **1** | 1 | 1 | 0 | **29** | `PARTIALLY_ACQUIRED_ACADEMIC` |
| **TOTAL** | **200** | **7** | **4** | **11** | **9** | **9** | **0** | **189** | `PARTIALLY COMPLETE` |

> [!IMPORTANT]
> The remaining target deficit currently stands at **189 images**. While Healthy and LSD deficits (100 images) are fully resolvable upon manual placement of the Mendeley archive, Ringworm (29 deficit), Dermatophilosis (31 deficit), and Pediculosis (29 deficit) require formal institutional outreach to veterinary teaching collections (e.g. Iowa State University CFSPH).

---

## 4. Mendeley Benchmark Status & Screening Guardrails

- **Dataset Identifier:** [`10.17632/ggpwpscjvm.1`](https://doi.org/10.17632/ggpwpscjvm.1)
- **Status:** `PENDING MANUAL DOWNLOAD (BROWSER INTERACTION REQUIRED)`
- **Access Barrier:** Cloudflare anti-bot challenge prevents automated headless HTTP GET requests; bypass is strictly prohibited by core directives.
- **Screening Rules Enforced Upon Ingestion:**
  1. **Healthy-LSD Controls (692 images):** Admitted only where bovine skin/coat is clearly visible and unblemished. Images where skin is obstructed by mud, water, or severe shadowing will be quarantined.
  2. **LSD Candidates (476 images):** Admitted under preserved source diagnosis of nodular lesions.
  3. **FMD Branch Quarantine (247 images):** Foot and mouth disease lesions belong to the blocked FMD branch and **MUST NOT be merged into any dermatological class**.
  4. **Healthy-FMD Controls (268 images):** Segregated controls captured for oral/hoof screening; prohibited from merging into dermatological controls without explicit anatomical matching.
- **Full Guide:** Documented in [mendeley_archive_verification.md](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_6/mendeley_archive_verification.md) and [mendeley_image_manifest.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_6/mendeley_image_manifest.csv).

---

## 5. Animal and Clinical Case Independence Findings

To prevent ungrounded claims of biological independence:
- **Published Animal Identifiers:** All source articles describe patient clinical contexts (*"14-month-old Nelore heifer"*, *"4-year-old local zebu bull"*, *"auction market calf"*) but **do not publish individual ear tags or names**. In accordance with audit standards, published animal IDs are officially recorded as **`UNKNOWN`** rather than fabricated.
- **Biological Case Breakdown:**
  - Polish Cow 1 (Ringworm, Dyląg et al., 2026) -> Standalone case.
  - Polish Cattle 2 (Ringworm, Gnat et al., 2024) -> Standalone case.
  - Austrian Auction Calf (Ringworm, Deschauer et al., 2024) -> Standalone case.
  - Chinese Cattle Herd (Ringworm, Wang et al., 2020) -> 2 panels (`I3_3_6_PMC_RW_004` and `005`) originate from the same trial herd and must be co-assigned in future splits.
  - Brazilian Calf (Ringworm, Albuquerque et al., 2026) -> Standalone case.
  - Irish Beef Heifer (Pediculosis, Valcárcel et al., 2021) -> Standalone case.
  - Ethiopian Zebu Bull (Dermatophilosis, Dagnaw et al., 2025) -> Standalone case.
  - Beninese Girolando Cow (Dermatophilosis, Akpo et al., 2021) -> Standalone case.
  - Brazilian Nelore Heifer (Dermatophilosis, Dantas et al., 2018) -> **Single animal, two anatomical panels** (`I3_3_4_FIG_001A` and `001B`). Strict fold constraint enforced: both panels must remain in the same evaluation fold.
- Full details documented in [animal_case_independence_register.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_6/animal_case_independence_register.csv).

---

## 6. Cryptographic Deduplication & Data Leakage Audit

A comprehensive hash audit was executed across all reference datasets:
- **Reference Datasets Audited:**
  1. D3 Dataset (Train, Validation, Test): 2,822 images
  2. Phase 6 Real LSD Benchmark: 669 image hashes
  3. Historical Synthetic Quarantine: 208 images
  4. Academic Quarantine: 19 figures
- **Reference Coverage:** 3,681 unique SHA-256 hashes; 2,715 unique perceptual dHashes.
- **Audit Results for 11 Candidate Images:**
  - Exact SHA-256 collisions: **0 (0.0%)**
  - Perceptual dHash matches: **0 (0.0%)**
  - Verdict: **`100% CLEAN_INDEPENDENT`**.
  - Documented in [duplicate_overlap_report.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_6/duplicate_overlap_report.csv).

---

## 7. Test Suite Verification & Codebase Integrity

A dedicated verification test suite was established in `tests/test_phase_i3_3_6_consolidation.py` covering directory structures, deliverables, candidate image integrity, animal fold constraints, deduplication, and production immutability.
- `tests/test_phase_i3_3_6_consolidation.py`: **8 / 8 passed (100%)**
- Global repository test suite: **139 / 139 passed (100%) in 9.12s** with zero regressions.
- Immutability of `models/image_experiments/phase6/lumpy_skin_lightgbm.joblib` and baseline D3 manifests verified intact.

---

## 8. Deliverables Manifest

All deliverables have been generated in [reports/image_experiments/phase_i3_3_6/](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_6/) and [data/experiments/image_dataset_i3_3_6/](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/data/experiments/image_dataset_i3_3_6/):

### Reports & Provenance Registers:
1. Master Report: [I3_3_6_FINAL_REPORT.md](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/I3_3_6_FINAL_REPORT.md) (and [reports/image_experiments/phase_i3_3_6/I3_3_6_FINAL_REPORT.md](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_6/I3_3_6_FINAL_REPORT.md))
2. Mendeley Archive Verification: [mendeley_archive_verification.md](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_6/mendeley_archive_verification.md)
3. Mendeley Image Manifest: [mendeley_image_manifest.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_6/mendeley_image_manifest.csv)
4. Consolidated Candidate Manifest: [consolidated_candidate_image_manifest.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_6/consolidated_candidate_image_manifest.csv)
5. Class-Wise Inventory: [class_wise_inventory.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_6/class_wise_inventory.csv)
6. Source Verification Register: [source_verification_register.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_6/source_verification_register.csv)
7. Academic Licensing & Attribution: [academic_licensing_and_attribution_register.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_6/academic_licensing_and_attribution_register.csv)
8. Animal Independence Register: [animal_case_independence_register.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_6/animal_case_independence_register.csv)
9. Duplicate & Overlap Report: [duplicate_overlap_report.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_6/duplicate_overlap_report.csv)
10. Quarantine Register: [quarantine_register.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_6/quarantine_register.csv)
11. Remediation Roadmap: [outstanding_acquisition_blockers.md](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_6/outstanding_acquisition_blockers.md)

### Visual Inspection Contact Sheets:
- [contact_sheet_ringworm.png](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/data/experiments/image_dataset_i3_3_6/contact_sheets/contact_sheet_ringworm.png)
- [contact_sheet_dermatophilosis.png](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/data/experiments/image_dataset_i3_3_6/contact_sheets/contact_sheet_dermatophilosis.png)
- [contact_sheet_pediculosis.png](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/data/experiments/image_dataset_i3_3_6/contact_sheets/contact_sheet_pediculosis.png)
- [contact_sheet_all_candidates.png](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/data/experiments/image_dataset_i3_3_6/contact_sheets/contact_sheet_all_candidates.png)

---

## 9. Final Completion Verdict & Governance

### Final Phase Status:
**`PARTIALLY COMPLETE — ACQUISITION BLOCKERS REMAIN`**

### Evidence Behind Status:
- **Dataset Consolidation Verified:** Unified 11-image candidate dataset successfully constructed with 100% clean provenance and zero baseline collisions.
- **Acquisition Blockers Remain:** Deficits remain across all 5 classes (Healthy: 50, LSD: 50, Ringworm: 29, Dermatophilosis: 31, Pediculosis: 29). Total target deficit: 189 images.
- **Phase Gate Closed:** In strict compliance with guidelines, no models were trained or evaluated. We stop and await your explicit instructions before initiating any further phase.
