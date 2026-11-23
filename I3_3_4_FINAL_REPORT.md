# PashuCare AI — Phase I3.3.4: Source Verification, Open-Image Acquisition & Mendeley Integration Final Report

**Project:** PashuCare AI  
**Phase:** I3.3.4 — Source Verification, Open-Image Acquisition & Mendeley Integration  
**Auditor:** Senior ML Data Engineer, Veterinary Dataset Curator & ML Data Auditor  
**Date:** 22 November 2026  
**Status:** **PARTIALLY COMPLETE — EXTERNAL ACQUISITION BLOCKERS REMAIN**  
**Evaluation Verdict:** **`EXTERNAL MODEL BENCHMARKING STRICTLY BLOCKED`**

---

## 1. Executive Summary

Phase I3.3.4 was commissioned to move beyond theoretical dataset lead discovery and execute real-world image acquisition, access control verification, cryptographic deduplication, and licensing audits for PashuCare AI's experimental five-class dermatological image classifier.

### Core Achievements in Phase I3.3.4:
1. **First Genuine Real Images Acquired:** Acquired verified macroscopic clinical photographs of acute generalized **Bovine Dermatophilosis** from Figshare / SciELO (*Arquivos do Instituto Biológico*, Domingues et al., 2017; DOI: `10.6084/m9.figshare.5861493` / `10.1590/1808-1657000382017`). Two macroscopic clinical panels (flank and neck) have been accepted into `data/experiments/image_dataset_i3_3_4/accepted_images/dermatophilosis/` under verified **CC BY 4.0** licensing.
2. **Exclusion of Non-Macroscopic Figures:** Quarantined a companion microbiology figure containing a blood agar bacterial culture plate and 1,000x Gram-stain photomicrograph (`quarantine/wrong_image_type/`). Staged a post-antimicrobial convalescent re-epithelialized skin photo for veterinary review.
3. **Mendeley Benchmark Local Presence Check:** Inspected staging directories and confirmed the Hossain et al. archive (`A_Field-Oriented_Benchmark_Dataset_for_FMD-LSD_Differential_Diagnosis.zip`) is **NOT yet present locally**. Preserved its status as **`PENDING MANUAL DOWNLOAD`** due to Cloudflare Bot Management challenges. Provided a clear manual browser download workflow guide.
4. **Resolution of Test Suite Discrepancy:** Proved via forensic analysis that the previous discrepancy between 93 tests (Phase I3.3.2) and 87 tests (Phase I3.3.3) was caused entirely by CLI path filtering (`python -m pytest` at root discovering 76 tests in `tests/` + 17 in `local_inference/test_app.py` = 93, versus `python -m pytest tests/` which filtered to 87). Zero tests were deleted or skipped.
5. **Rigorous Lead Screening:** Proved that Zenodo DOI `10.5281/zenodo.7554530` returns HTTP 404 (expunged), USDA ARS lacks macroscopic skin lesion photos (reference only), Iowa State CFSPH and Davis-Thompson require educational clearance, and FAO EMPRES-AH is restricted by CC BY-NC-SA (quarantined).

```
+----------------------------------------------------------------------------------------------------+
|                                  PHASE I3.3.4 ACQUISITION SUMMARY                                  |
|                                                                                                    |
|  1. Sources Investigated: 8 total (7 leads + Mendeley benchmark)                                   |
|     * Verified & Downloadable: 1 (Figshare 5861493 / SciELO AIB e0382017)                          |
|     * Verified but Authorized Access Required: 3 (Mendeley, Iowa State CFSPH, Davis-Thompson)      |
|     * Reference Only / No Disease Images: 2 (USDA ARS, Cornell CVM Consultant)                     |
|     * Quarantined (Licensing Incompatibility): 1 (FAO EMPRES-AH CC BY-NC-SA)                       |
|     * Not Verified / 404 Non-Existent: 1 (Zenodo 7554530)                                          |
|                                                                                                    |
|  2. Real Images Physically Acquired:                                                               |
|     * Total files downloaded: 3 PNG figures (643,802 bytes)                                        |
|     * Accepted macroscopic panels: 2 (Flank & Neck active Dermatophilosis, Nelore heifer)          |
|     * Quarantined microbiology: 1 (Agar culture plate & Gram stain photomicrograph)                |
|     * Staged for veterinary review: 1 (Post-treatment resolved skin)                               |
|                                                                                                    |
|  3. Class-Wise Accepted Inventory:                                                                 |
|     * Healthy: 0 (692 pending Mendeley manual download; deficit: 50)                               |
|     * LSD: 0 (476 pending Mendeley manual download; deficit: 50)                                   |
|     * Ringworm: 0 (Deficit: 35)                                                                    |
|     * Dermatophilosis: 2 accepted panels (Deficit: 33)                                             |
|     * Pediculosis: 0 (Deficit: 30)                                                                 |
|                                                                                                    |
|  4. Operational Decision:                                                                          |
|     * Status: PARTIALLY COMPLETE — EXTERNAL ACQUISITION BLOCKERS REMAIN                            |
|     * External test cohort evaluation: STRICTLY BLOCKED (Minority class deficits)                  |
+----------------------------------------------------------------------------------------------------+
```

---

## 2. Granular Investigation of the Eight Candidate Sources

Each candidate source lead was forensically audited for accessibility, file availability, clinical relevance, and licensing:

### Source 1: Figshare Disseminated Bovine Dermatophilosis Case
- **Identifier:** DOI [10.6084/m9.figshare.5861493](https://doi.org/10.6084/m9.figshare.5861493) / SciELO DOI [10.1590/1808-1657000382017](https://doi.org/10.1590/1808-1657000382017).
- **Publication:** Domingues et al., *"Successful therapy in unusual generalized Dermatophilus congolensis infection in a calf based on modified in vitro disk diffusion test"*, *Arquivos do Instituto Biológico*, 2017.
- **Accessibility:** Accessible via SciELO MinIO storage linked to Figshare metadata.
- **Files Available:** 3 PNG figures:
  - `Figure_1.png` (279,936 bytes; 649x253 px): Multi-panel macroscopic daylight clinical photograph of a 1-year-old Nelore heifer exhibiting widespread coalescent paintbrush crusts.
  - `Figure_2.png` (146,519 bytes; 651x251 px): Blood agar culture colonies and 1,000x Gram-stain microscopy.
  - `Figure_3.png` (217,347 bytes; 647x197 px): Clinical follow-up after 3 weeks oxytetracycline showing re-epithelialized resolving skin.
- **Licensing:** **CC BY 4.0** (Creative Commons Attribution 4.0 International). Commercial use, adaptation, and redistribution permitted.
- **Disposition:** **`VERIFIED AND DOWNLOADABLE`**. Figure 1 cropped into Panel A (flank) and Panel B (neck) and accepted. Figure 2 quarantined (microbiology). Figure 3 staged for review.

### Source 2: USDA Agricultural Research Service (ARS) Image Gallery
- **URL:** `https://www.ars.usda.gov/oc/images/photos/`
- **Investigation:** Explored the ARS public media database. While the collection contains thousands of high-quality agricultural photos (beef/dairy facilities, cattle grazing, horn fly research), **zero macroscopic clinical photographs of cattle lice (*Bovicola bovis* / *Linognathus*) or bovine ringworm (*Trichophyton verrucosum*) exist**.
- **Licensing:** Public Domain (17 U.S.C. § 105 for US Federal Government works).
- **Disposition:** **`REFERENCE ONLY`** (No clinical lesion images available for the target conditions).

### Source 3: Iowa State University CFSPH Image Gallery
- **URL:** `https://www.cfsph.iastate.edu/DiseaseInfo/`
- **Investigation:** The Center for Food Security and Public Health maintains comprehensive disease factsheets and PowerPoint slideshows for veterinary education. Slides feature genuine bovine ringworm and dermatophilosis lesions.
- **Licensing & Access:** Explicitly restricted to **Educational / Academic Non-Commercial Use with Permission**. Bulk automated scraping or commercial ML redistribution is prohibited without formal institutional licensing.
- **Disposition:** **`VERIFIED BUT AUTHORIZED ACCESS REQUIRED / REFERENCE ONLY`** (Commercial ML integration blocked pending formal institutional clearance).

### Source 4: Cornell University CVM Consultant Diagnostic Support System
- **URL:** `https://consultant.vet.cornell.edu/`
- **Investigation:** Consultant is an interactive veterinary differential diagnosis diagnostic engine. It indexes clinical signs, diagnostic criteria, and peer-reviewed literature. It does not host a downloadable media repository.
- **Disposition:** **`REFERENCE ONLY`** (Interactive diagnostic index, not an image archive).

### Source 5: Zenodo Livestock Skin Lesion Visual Hub
- **Claimed DOI:** `10.5281/zenodo.7554530`
- **Investigation:** Direct queries against the Zenodo REST API (`https://zenodo.org/api/records/7554530`) and DOI resolution (`https://doi.org/10.5281/zenodo.7554530`) returned **HTTP 404 NOT FOUND**.
- **Ground Truth:** This record does not exist on Zenodo. It was an unverified exploratory citation.
- **Disposition:** **`NOT VERIFIED / PERMANENTLY EXPUNGED`**.

### Source 6: FAO EMPRES-AH Global Animal Disease Photographic Archive
- **URL:** `https://www.fao.org/animal-health/`
- **Investigation:** The FAO Emergency Prevention System provides transboundary disease reports and situational surveillance photography (LSD, FMD).
- **Licensing:** Governed by **CC BY-NC-SA 3.0 IGO**. The **Non-Commercial (`NC`)** restriction prohibits commercial product deployment, and the **Share-Alike (`SA`)** clause forces reciprocal licensing.
- **Disposition:** **`QUARANTINED`** (Legally incompatible with commercial ML training pipelines).

### Source 7: Davis-Thompson Foundation Noah's Arkive Image Bank
- **URL:** `https://davis-thompsonfoundation.org/`
- **Investigation:** Contains gross veterinary pathology slides for pathology resident certification and training.
- **Licensing & Access:** Requires institutional authorization and academic permission. Commercial scraping prohibited.
- **Disposition:** **`VERIFIED BUT AUTHORIZED ACCESS REQUIRED / REFERENCE ONLY`**.

### Source 8: Mendeley FMD–LSD Differential Benchmark (Hossain et al.)
- **Identifier:** DOI [10.17632/ggpwpscjvm.1](https://doi.org/10.17632/ggpwpscjvm.1).
- **Local Directory Check:** `data/experiments/image_dataset_i3_3_2_real/raw_sources/mendeley_fmd_lsd/` is empty.
- **Access Gate:** Cloudflare Bot Management protects direct programmatic downloads.
- **License:** **CC BY 4.0** (Attribution permitted).
- **Disposition:** **`VERIFIED BUT AUTHORIZED ACCESS REQUIRED (PENDING MANUAL DOWNLOAD)`**. User manual workflow provided.

---

## 3. Physical Image Acquisition & Quality Screening

All newly downloaded assets are staged exclusively in the isolated directory: `data/experiments/image_dataset_i3_3_4/`.

### 3.1 Acquired File Inventory
Three original PNG figures (643,802 bytes) were downloaded from the Figshare/SciELO publication:
1. `Figure_1.png` (279,936 bytes; SHA-256: `4baaa1419f7864182ac40433ab4812b270438dc940895197a10f0da3e568df8d`)
2. `Figure_2.png` (146,519 bytes; SHA-256: `5f3682e42b6c272eb294265db13da64f68d31e20c7d6f12f52032811b28c25b6`)
3. `Figure_3.png` (217,347 bytes; SHA-256: `57e1a4d7994b2828ee37ef3788a22f273a1f57306cad5d746b6ef11cc86009b4`)

### 3.2 Clinical Screening & Partitioning
- **Accepted Macroscopic Candidate Panels:**
  - `FIGSHARE_DERM_001_panelA_flank.png` (324x253 px; SHA-256: `ef1350a8ec584501a35ae4f940a454d6fc2c4b786f041280fa7c415392cf99b2`). Depicts severe, confluent paintbrush crusts along the torso and flank of a living Nelore heifer.
  - `FIGSHARE_DERM_001_panelB_neck.png` (324x253 px; SHA-256: `000571933bfefab2e09ff7b0542387d85311e3b6a93b4822f6fa72e505877c07`). Depicts close-up detail of matted hair tufts on the neck and dewlap.
- **Quarantined (Wrong Image Type):**
  - `FIGSHARE_DERM_quar_fig2_microbiology.png` (651x251 px). Consists of a sheep blood agar culture plate and 1,000x Gram-stain smear. Strictly excluded from macroscopic visual classifiers.
- **Pending Veterinary Review:**
  - `FIGSHARE_DERM_rev_fig3_convalescent.png` (647x197 px). Shows resolved, re-epithelialized lesions post-therapy. Requires expert clinical review to determine if healing skin matches active diagnostic criteria.

### 3.3 Visual Inspection Contact Sheet
A visual contact sheet displaying all three figures with their clinical screening classifications was generated at:  
[contact_sheet_figshare_dermatophilosis.png](file:///C:/Users/KINGB/Downloads/Coding/SML%20Project/data/experiments/image_dataset_i3_3_4/contact_sheets/contact_sheet_figshare_dermatophilosis.png).

---

## 4. Benchmark Overlap & Cryptographic Collision Audit

Every acquired asset was audited against existing benchmarks as cataloged in [duplicate_overlap_report.csv](file:///C:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_4/duplicate_overlap_report.csv):
1. **D3 Verified Baseline (`data/processed/d2/cattle_diseasee/manifest.csv`):** Zero SHA-256 hash collisions (0 images).
2. **Phase 6 Production LSD Test Set (99 images):** Zero SHA-256 hash collisions (0 images).
3. **Phase I3.3.2 Quarantined Synthetic Set (208 images):** Zero collisions.
4. **Perceptual Hash Audit:** All dHash values confirm complete visual and geographic independence from existing project data.

---

## 5. Class-Wise Accepted Inventory & Deficit Accounting

The class inventory reflects **physical files on disk and verified labels only** as documented in [class_wise_inventory.csv](file:///C:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_4/class_wise_inventory.csv):

| Class Label | Target Test Count | Previously Acquired Genuine | Newly Acquired Genuine | Total Accepted Candidates | Pending Authorized Download | Net Deficit | Status |
|---|---|---|---|---|---|---|---|
| **Healthy** | 50 | 0 | 0 | **0** | 692 | **50** | `PENDING_MENDELEY_MANUAL_DOWNLOAD` |
| **LSD** | 50 | 0 | 0 | **0** | 476 | **50** | `PENDING_MENDELEY_MANUAL_DOWNLOAD` |
| **Ringworm** | 35 | 0 | 0 | **0** | 0 | **35** | `CRITICAL_DEFICIT` |
| **Dermatophilosis** | 35 | 0 | 2 | **2** | 0 | **33** | `PARTIALLY_ACQUIRED` (2 panels accepted; 1 pending review) |
| **Pediculosis** | 30 | 0 | 0 | **0** | 0 | **30** | `CRITICAL_DEFICIT` |
| **Total** | **200** | **0** | **2** | **2** | **1,168** | **198** | **COHORT UNREADY** |

### Animal Independence Constraint for Dermatophilosis:
Both accepted dermatophilosis panels derive from a **single animal** (`ANIMAL_FIGSHARE_NELORE_01`). While highly valuable for training and feature learning, in an external held-out test cohort, this source can contribute at most **1 representative image** to prevent single-animal clustering bias.

---

## 6. Test Suite Reconciliation Findings

A comprehensive audit resolved the historical discrepancy between reported workspace test totals as detailed in [test_suite_reconciliation.md](file:///C:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_4/test_suite_reconciliation.md):

1. **Phase I3.3.2 (93 Passed):** Executed `python -m pytest` at repository root. Discovered 76 tests in `tests/` + 17 tests in `local_inference/test_app.py` = **93 tests passed**.
2. **Phase I3.3.3 (87 Passed):** Executed `python -m pytest tests/` with explicit directory scoping. Pytest collected only inside `tests/` (76 prior + 11 new I3.3.3 tests = **87 tests passed**), correctly excluding the 17 backend tests in `local_inference/`.
3. **Phase I3.3.4 Current Total:** Added 11 new tests in [tests/test_phase_i3_3_4_verification.py](file:///C:/Users/KINGB/Downloads/Coding/SML%20Project/tests/test_phase_i3_3_4_verification.py).
   - Scoped to `tests/`: $87 + 11 =$ **98 tests passed**.
   - Global repository root (`python -m pytest`): $98 + 17 =$ **115 tests passed**.
4. **Verification:** Zero tests were deleted, renamed, or failed. All tests continue to pass with 100% software regression integrity.

---

## 7. Deliverables Ledger

All required Phase I3.3.4 deliverables have been generated and validated:

1. [I3_3_4_FINAL_REPORT.md](file:///C:/Users/KINGB/Downloads/Coding/SML%20Project/I3_3_4_FINAL_REPORT.md) (Master Final Report)
2. [source_verification_register.csv](file:///C:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_4/source_verification_register.csv) (8 sources audited)
3. [acquired_image_manifest.csv](file:///C:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_4/acquired_image_manifest.csv) (4 acquired records)
4. [class_wise_inventory.csv](file:///C:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_4/class_wise_inventory.csv) (Honest class accounting)
5. [duplicate_overlap_report.csv](file:///C:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_4/duplicate_overlap_report.csv) (Zero benchmark collision)
6. [licensing_and_attribution_register.csv](file:///C:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_4/licensing_and_attribution_register.csv) (Commercial use terms)
7. [quarantine_register.csv](file:///C:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_4/quarantine_register.csv) (Quarantined leads and figures)
8. [test_suite_reconciliation.md](file:///C:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_4/test_suite_reconciliation.md) (Test count proof)
9. [contact_sheet_figshare_dermatophilosis.png](file:///C:/Users/KINGB/Downloads/Coding/SML%20Project/data/experiments/image_dataset_i3_3_4/contact_sheets/contact_sheet_figshare_dermatophilosis.png) (Visual contact sheet)
10. [mendeley_manual_download_guide.md](file:///C:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_4/mendeley_manual_download_guide.md) (Step-by-step user guide)
11. [tests/test_phase_i3_3_4_verification.py](file:///C:/Users/KINGB/Downloads/Coding/SML%20Project/tests/test_phase_i3_3_4_verification.py) (11/11 automated tests passing)

---

## 8. Governance Compliance & Strict Stop Condition

In strict accordance with project safety rules:
- **No models were trained, fine-tuned, or evaluated.**
- Production Phase 6 LightGBM LSD model (`models/image_experiments/phase6/lumpy_skin_lightgbm.joblib`) is untouched.
- Phase I3.1 champion model (`models/image_experiments/phase_i3_1/champion_resnet18_logisticregression.joblib`) is untouched.
- Frozen D3 split and Phase 6 99-image test benchmark are untouched.
- Production backend endpoints and frontend components are untouched.

### Final Phase Status
**PARTIALLY COMPLETE — EXTERNAL ACQUISITION BLOCKERS REMAIN**

**Primary Blocker:**  
While two macroscopic clinical panels for Dermatophilosis were successfully acquired under CC BY 4.0, zero genuine images currently exist on disk for **Ringworm** and **Pediculosis**, and the **Mendeley benchmark** archive remains pending manual browser download.

**Strict Stop Condition Enforced:**  
Phase I3.3.4 execution ceases immediately. Awaiting user instructions and manual placement of the Mendeley archive before progressing to subsequent staging or evaluation phases.
