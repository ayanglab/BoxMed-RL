# Filtered Dataset

This folder contains the **filtered subsets** of medical imaging datasets used for the **SVR (Spatial Verification and Reasoning)** stage in our study.
Each CSV file lists the `dicom_id` entries that have **consistent split alignment** (train / validate / test) with the official **MIMIC-CXR v2.0.0** split, ensuring **no data leakage** between the SVR pretraining datasets and the downstream report-generation phase.

---

## 📂 Files Overview

| File                               | Source Dataset                | Overlap Checked Against | Description                                                                                                                 
| ---------------------------------- | ----------------------------- | ----------------------- | --------------------------------------------------------------------------------------------------------------------------- 
| **`MS-CXR_filtered_ID.csv`**       | MS-CXR Local Alignment v1.1.0 | MIMIC-CXR v2.0.0        | Contains DICOM IDs from MS-CXR whose split labels match those in MIMIC-CXR. Inconsistent samples (train↔test) were removed. 
| **`LATTE_Phase2_filtered_ID.csv`** | LATTE-CXR Phase 2             | MIMIC-CXR v2.0.0        | All overlapping samples had perfectly aligned train/test/validate splits.                                                  
| **`LATTE_Phase3_filtered_ID.csv`** | LATTE-CXR Phase 3             | MIMIC-CXR v2.0.0        | Minor validate↔train mismatches (392) removed; no train↔test conflicts remain.                                              

---

## 🧠 Background

During SVR pretraining, we used **LATTE-CXR** and **MS-CXR** for bounding-box and phrase supervision, while **MIMIC-CXR** was used in the downstream report generation stage.
Because LATTE and MS are partially derived from MIMIC images, we carefully checked for **split inconsistencies** that could lead to data leakage between training and testing phases.

### Leakage check procedure

1. Matched all datasets by `dicom_id`.
2. Compared split assignments (`train`, `validate`, `test`).
3. Removed any entries with mismatched assignments (e.g., `train` in MS-CXR but `test` in MIMIC-CXR).
4. Saved only consistent entries to the filtered CSVs in this folder.

All code used for verification is available in the project’s analysis scripts.

---

## 📊 Summary of Consistency Checks

| Dataset               | Total Overlap | Split Mismatches          | Filtered Count | 
| --------------------- | ------------- | ------------------------- | -------------- | 
| **MS-CXR**            | 1,227         | 349                       | 878            | 
| **LATTE-CXR Phase 2** | 240           | 0                         | 240            | 
| **LATTE-CXR Phase 3** | 2,507         | 392 (validate↔train only) | 2,115          | 

---

## 📜 How to Use

Each CSV contains at least:

* `dicom_id`
* `split` (train / validate / test)
* Additional metadata columns as provided by the original dataset release.

You can safely use these filtered splits for:

* **SVR (box-detection supervision)** training
* **Downstream report-generation fine-tuning**
  without any risk of cross-split contamination.

Example:

```python
import pandas as pd
ms_filtered = pd.read_csv("Filtered Dataset/MS-CXR_filtered_ID.csv")
print(ms_filtered['split'].value_counts())
```

---

## 🧾 Citation and Data Access

Original datasets are hosted on **PhysioNet**:

* [MIMIC-CXR v2.0.0](https://physionet.org/content/mimic-cxr/2.1.0/)
* [MS-CXR Local Alignment v1.1.0](https://physionet.org/content/ms-cxr/1.1.0/)
* [LATTE-CXR v1.0.0](https://physionet.org/content/latte-cxr/1.0.0/)

