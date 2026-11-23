# PashuCare AI — Phase I3.3.5A Final Report: Acquisition Verification, DOI Reconciliation & Provenance Audit

**Phase:** I3.3.5A (Focused Verification Addendum)  
**Project Context:** Undergraduate Academic Research & Educational Prototype  
**Date:** November 2026  
**Final Status:** `VERIFIED — ALL FIVE ACQUISITIONS CONFIRMED`  
**Model Training / Evaluation Status:** `STRICTLY PROHIBITED (GATES REMAIN CLOSED)`

---

## 1. Executive Summary & Authorization Scope

Phase I3.3.5A was executed as a focused verification addendum to independently audit the claims and assets of Phase I3.3.5. In accordance with strict project boundaries, no models were trained, evaluated, fine-tuned, or deployed; frozen production artifacts, baseline D3 splits, backend inference endpoints, and frontend integration remain 100% immutable.

The audit verified:
1. **The Five Newly Acquired Images:** Inspected physical image files, confirmed laboratory diagnostic evidence from full-text journal XML, validated macroscopic bovine clinical status, and verified open-access CC BY 4.0 licensing.
2. **Bibliographic & DOI Reconciliation:** Reconciled three minor typographical transcription discrepancies in publication DOIs and solved the Mendeley external benchmark DOI conflict (`10.17632/ggpwpscjvm.1` verified valid; `10.17632/w8vbtghw3z.1` identified as an invalid 404 artefact).
3. **Animal and Clinical Case Independence:** Reconciled animal-level provenance across 6 distinct animals spanning 5 countries, explicitly designated published animal identifiers as `UNKNOWN` to prevent artificial provenance fabrication, and enforced the single-animal multi-panel fold constraint for the two Brazilian Nelore heifer panels.
4. **Cryptographic Deduplication Re-Audit:** Conducted an exhaustive hash comparison against 3,681 unique reference SHA-256 hashes and 2,715 perceptual dHashes across D3 (train/val/test), Phase 6 real benchmark, historical synthetic quarantine, and academic quarantine, confirming **0 exact collisions and 0 perceptual collisions**.
5. **Codebase Integrity:** Executed the complete test suite: **131 / 131 tests passing (100%)** with zero regressions.

---

## 2. Verification of the Five Newly Acquired Images (+ 2 Earlier Panels)

Every acquired image was cross-referenced against the original full-text XML from the National Center for Biotechnology Information (NCBI) PubMed Central (PMC) or Figshare repository.

| Image ID | Target Class | Verified DOI | Journal & Year | Species & Breed | Diagnostic Proof | Macroscopic? | Licence Status | Verification Verdict |
|---|---|---|---|---|---|---|---|---|
| **`I3_3_5_PMC_RW_001`** | Ringworm | [`10.3390/ani16131984`](https://doi.org/10.3390/ani16131984) | *Animals* (MDPI), 2026 | *Bos taurus* (Cow) | 10% KOH scrapings + DTM fungal culture (*T. verrucosum*) | Yes (Cow face) | CC BY 4.0 (Author owned) | **`VERIFIED`** |
| **`I3_3_5_PMC_RW_002`** | Ringworm | [`10.3390/pathogens13100848`](https://doi.org/10.3390/pathogens13100848) | *Pathogens* (MDPI), 2024 | *Bos taurus* (Cattle) | Mycological identification & herd lesions (*T. verrucosum*) | Yes (Body lesions) | CC BY 4.0 (Author owned) | **`VERIFIED`** |
| **`I3_3_5_PMC_PED_001`** | Pediculosis | [`10.1186/s13620-021-00198-y`](https://doi.org/10.1186/s13620-021-00198-y) | *Irish Vet J* (BMC), 2021 | *Bos taurus* (Beef Heifer) | Dissection microscopy key morphology (*Bovicola bovis*) | Yes (Dorsal shoulders) | CC BY 4.0 (Author owned) | **`VERIFIED`** |
| **`I3_3_5_PMC_DERM_001`** | Dermatophilosis | [`10.1002/vms3.70245`](https://doi.org/10.1002/vms3.70245) | *Vet Med Sci* (Wiley), 2025 | *Bos indicus* (Zebu Bull) | Blood agar culture + Giemsa tram-track hyphae (*D. congolensis*) | Yes (Panel A crop; bull lesions) | CC BY 4.0 (Author owned) | **`VERIFIED`** |
| **`I3_3_5_PMC_DERM_002`** | Dermatophilosis | [`10.14202/vetworld.2021.2750-2756`](https://doi.org/10.14202/vetworld.2021.2750-2756) | *Vet World*, 2021 | *Bos taurus x indicus* (Girolando Cow) | Direct smear branching filaments (*D. congolensis*) | Yes (Live cow lesions) | CC BY 4.0 (Author owned) | **`VERIFIED`** |
| **`I3_3_4_FIG_001A`** | Dermatophilosis | [`10.6084/m9.figshare.5861493`](https://doi.org/10.6084/m9.figshare.5861493) | *Figshare / Vet World*, 2018 | *Bos indicus* (Nelore Heifer) | Giemsa cytological smear parallel cocci (*D. congolensis*) | Yes (Flank panel crop) | CC BY 4.0 (Author owned) | **`VERIFIED`** |
| **`I3_3_4_FIG_001B`** | Dermatophilosis | [`10.6084/m9.figshare.5861493`](https://doi.org/10.6084/m9.figshare.5861493) | *Figshare / Vet World*, 2018 | *Bos indicus* (Nelore Heifer) | Giemsa cytological smear parallel cocci (*D. congolensis*) | Yes (Neck panel crop) | CC BY 4.0 (Author owned) | **`VERIFIED`** |

Full physical parameters and bibliographic data are documented in [five_image_publication_verification.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5a/five_image_publication_verification.csv).

---

## 3. Bibliographic and DOI Reconciliation

The audit identified and reconciled four digital object identifier (DOI) records:

1. **MDPI *Animals* (Ringworm 1):**
   - *Claimed in I3.3.5:* `10.3390/ani16121984` (Issue 12)
   - *Verified Ground Truth:* `10.3390/ani16131984` (Issue 13)
   - *Resolution:* Corrected transcription typo; resolves directly to PMC13359616.
2. **Irish Veterinary Journal (Pediculosis 1):**
   - *Claimed in I3.3.5:* `10.1186/s13620-021-00198-4` (Digit '4')
   - *Verified Ground Truth:* `10.1186/s13620-021-00198-y` (Letter 'y')
   - *Resolution:* Corrected check character; resolves directly to PMC8259056.
3. **Veterinary World (Dermatophilosis 2):**
   - *Claimed in I3.3.5:* `10.14202/vetworld.2021.2750-2755` (Page 2755)
   - *Verified Ground Truth:* `10.14202/vetworld.2021.2750-2756` (Page 2756)
   - *Resolution:* Corrected ending page range; resolves directly to PMC8654760.
4. **Mendeley External Benchmark (Critical Reconciliation):**
   - *Discrepancy:* `10.17632/ggpwpscjvm.1` (Historical) vs `10.17632/w8vbtghw3z.1` (Reported in I3.3.5).
   - *Investigation Findings:*
     - Direct query to `https://doi.org/10.17632/ggpwpscjvm.1` resolves with `HTTP 302 -> HTTP 200` to Mendeley Data: *A Field-Oriented Benchmark Dataset for FMD–LSD Differential Diagnosis in Beef Cattle Under Unconstrained Farm Conditions* (Audity Rani Paul & Susmoy Biswas, Oct 7, 2026, CC BY 4.0, 1,683 images: 692 Healthy-LSD, 476 LSD, 247 FMD, 268 Healthy-FMD).
     - Direct query to `https://doi.org/10.17632/w8vbtghw3z.1` returns **`HTTP 404: Not Found`**.
   - *Conclusion:* `10.17632/ggpwpscjvm.1` is the sole genuine and valid canonical DOI. The string `w8vbtghw3z` was an accidental clerical error in Phase I3.3.5.
   - Detailed evidence is documented in [mendeley_doi_reconciliation.md](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5a/mendeley_doi_reconciliation.md).

---

## 4. Image-Level Licensing & Third-Party Rights Audit

Under the academic prototype mandate:
- All five newly acquired images and two Figshare panels are licensed under **Creative Commons Attribution 4.0 International (CC BY 4.0)**.
- **Third-Party Rights Inspection:**
  - In `PMC11510394` (MDPI *Pathogens*), Figures 2 through 9 carry explicit third-party courtesy credits (*"courtesy of Honorata Kubisiak-Rzepczyk"*). These were correctly identified in Phase I3.3.5 and segregated into quarantine.
  - Figure 1 (*cattle lesions*), however, carries **zero third-party copyright restrictions** and is the direct work of the publication authors under CC BY 4.0.
  - All other accepted images (`PMC13359616` Fig 1, `PMC8259056` Fig 1, `PMC11800365` Fig 1A, `PMC8654760` Fig 1, and Figshare 5861493) are fully covered by author open-access licenses without third-party encumbrances.
- **Attribution Statements:** Formatted and cataloged in [image_level_licensing_audit.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5a/image_level_licensing_audit.csv). All images are assigned status: **`VERIFIED — ATTRIBUTION REQUIRED`**.

---

## 5. Animal and Clinical Case Independence Findings

To prevent ungrounded claims of provenance:
1. **Published Animal IDs:** The original peer-reviewed papers describe patient characteristics (e.g. *"4-year-old local zebu bull"*, *"3-year-old Girolando dairy cow"*, *"14-month-old Nelore heifer"*, *"cow with dermatophytosis from 50-head study cohort"*, *"heifer from Teagasc beef farm"*), but **do not publish ear tag IDs or individual animal names**. In accordance with audit instructions, published animal IDs are officially recorded as **`UNKNOWN`** rather than fabricated.
2. **Biological Independence:**
   - 6 independent clinical animals are verified:
     - Polish Cow 1 (Ringworm, Dyląg et al.)
     - Polish Cattle 2 (Ringworm, Gnat et al.)
     - Irish Beef Heifer (Pediculosis, Valcárcel et al.)
     - Ethiopian Zebu Bull (Dermatophilosis, Dagnaw et al.)
     - Beninese Girolando Cow (Dermatophilosis, Akpo et al.)
     - Brazilian Nelore Heifer (Dermatophilosis, Dantas et al.)
3. **Multi-Panel Constraint Enforcement:**
   - Images `I3_3_4_FIG_001A` (flank) and `I3_3_4_FIG_001B` (neck) represent the **same Nelore heifer** (`SINGLE_ANIMAL_MULTI_PANEL`).
   - In any future evaluation fold or split, both panels **must remain bound to the same fold** to prevent intra-animal cross-panel data leakage.
   - Documented in [animal_case_independence_reconciliation.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5a/animal_case_independence_reconciliation.csv).

---

## 6. Duplicate and Overlap Re-Audit

A comprehensive, automated hash audit was executed across all reference datasets:
- **Reference Datasets Audited:**
  1. D3 Dataset (Train, Validation, Test): 2,822 images
  2. Phase 6 Real LSD Benchmark: 669 image hashes
  3. Historical Synthetic Quarantine: 208 images
  4. I3.3.5 Academic Quarantine: 16 figures
- **Reference Coverage:** 3,681 unique SHA-256 hashes; 2,715 unique perceptual dHashes.
- **Audit Results for Accepted Candidate Images:**
  - Exact SHA-256 collisions detected: **0 (0.0%)**
  - Perceptual dHash matches detected: **0 (0.0%)**
  - Provenance Independence Verdict: **`100% CLEAN_PROVENANCE_INDEPENDENT`**.
  - Documented in [duplicate_overlap_reaudit.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5a/duplicate_overlap_reaudit.csv).

---

## 7. Reconciled Image Inventory

| Class Label | Target Size | Physical Files | Verified Labelled | Verified Licenced | Independent Animals | Independent Cases | Unknown Animal ID | Pending Manual Download | Quarantined | Remaining Deficit | Inventory Status |
|---|---|---|---|---|---|---|---|---|---|---|---|
| **Healthy** | 50 | 0 | 0 | 0 | 0 | 0 | 0 | 692 | 0 | **50** | `PENDING_MENDELEY_MANUAL_DOWNLOAD` ([10.17632/ggpwpscjvm.1](https://doi.org/10.17632/ggpwpscjvm.1)) |
| **LSD** | 50 | 0 | 0 | 0 | 0 | 0 | 0 | 476 | 0 | **50** | `PENDING_MENDELEY_MANUAL_DOWNLOAD` ([10.17632/ggpwpscjvm.1](https://doi.org/10.17632/ggpwpscjvm.1)) |
| **Ringworm** | 35 | 2 | 2 | 2 | 2 | 2 | 2 | 0 | 10 | **33** | `PARTIALLY_ACQUIRED_ACADEMIC` (Deficit: 33) |
| **Dermatophilosis** | 35 | 4 | 4 | 4 | 3 | 3 | 4 | 0 | 3 | **31** | `PARTIALLY_ACQUIRED_MULTI_CONTINENT` (3 animals, 4 images; Deficit: 31) |
| **Pediculosis** | 30 | 1 | 1 | 1 | 1 | 1 | 1 | 0 | 2 | **29** | `PARTIALLY_ACQUIRED_ACADEMIC` (Deficit: 29) |
| **TOTAL** | **200** | **7** | **7** | **7** | **6** | **6** | **7** | **1,168** | **15** | **193** | `PARTIALLY COMPLETE` |

Documented in [corrected_class_inventory.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5a/corrected_class_inventory.csv).

---

## 8. Test Suite Execution & Codebase Integrity

A dedicated verification test module was added in `tests/test_phase_i3_3_5a_verification.py`. The global workspace test suite was executed:
- **Command:** `python -m pytest`
- **Result:** **`131 passed in 9.87s (100%)`**
- **Regressions:** `0`
- Detailed breakdown documented in [test_suite_verification.md](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5a/test_suite_verification.md).

---

## 9. Deliverables Manifest (Phase I3.3.5A Audit Directory)

All audit outputs are isolated in `reports/image_experiments/phase_i3_3_5a/`:
- [I3_3_5A_FINAL_REPORT.md](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5a/I3_3_5A_FINAL_REPORT.md) (and [I3_3_5A_FINAL_REPORT.md](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/I3_3_5A_FINAL_REPORT.md))
- [five_image_publication_verification.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5a/five_image_publication_verification.csv)
- [figure_caption_and_diagnosis_evidence.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5a/figure_caption_and_diagnosis_evidence.csv)
- [image_level_licensing_audit.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5a/image_level_licensing_audit.csv)
- [animal_case_independence_reconciliation.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5a/animal_case_independence_reconciliation.csv)
- [mendeley_doi_reconciliation.md](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5a/mendeley_doi_reconciliation.md)
- [duplicate_overlap_reaudit.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5a/duplicate_overlap_reaudit.csv)
- [corrected_class_inventory.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5a/corrected_class_inventory.csv)
- [unresolved_provenance_register.csv](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5a/unresolved_provenance_register.csv)
- [test_suite_verification.md](file:///c:/Users/KINGB/Downloads/Coding/SML%20Project/reports/image_experiments/phase_i3_3_5a/test_suite_verification.md)

---

## 10. Final Completion Verdict & Recommended Next Actions

### Final Audit Status:
**`VERIFIED — ALL FIVE ACQUISITIONS CONFIRMED`**

### Summary of Evidence:
- **Acquisitions Confirmed:** All five newly acquired images (plus two earlier Figshare panels) have verified macroscopic bovine dermatology status, definitive laboratory diagnostic evidence in full publication text, and legal CC BY 4.0 authorization.
- **Reconciliation Complete:** All publication DOI typos are corrected; the canonical Mendeley DOI `10.17632/ggpwpscjvm.1` is confirmed active and official, while `w8vbtghw3z` is definitively identified as an invalid 404 string.
- **Independence & Clean Provenance:** 6 biological animals established with published IDs recorded as `UNKNOWN`; zero data leakage or duplicate collisions with baseline sets.

### Next Recommended Actions:
1. **Manual Mendeley Download:** Operator downloads `A_Field-Oriented_Benchmark_Dataset_for_FMD-LSD_Differential_Diagnosis.zip` from verified canonical URL [`https://data.mendeley.com/datasets/ggpwpscjvm/1`](https://data.mendeley.com/datasets/ggpwpscjvm/1) to resolve 692 Healthy and 476 LSD images.
2. **Institutional Outreach:** University research team transmits the ready-to-send draft letters in `reports/image_experiments/phase_i3_3_5/institutional_permission_requests.md` to Iowa State University CFSPH to resolve minority-class deficits (Ringworm 33, Dermatophilosis 31, Pediculosis 29).
3. **Phase Gate:** Model training, evaluation, and threshold tuning **remain strictly prohibited** until external test cohort quotas are resolved.
