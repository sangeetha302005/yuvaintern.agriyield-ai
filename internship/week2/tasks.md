# Week 2: Data Acquisition and Preparation — Task Summary

**Internship Role**: Junior Machine Learning Data Analyst — Agriculture & Agribusiness  
**Internship Organization**: YuvaIntern  
**Internship Period**: 01 October 2026 – 29 October 2026  
**Intern**: Sangeetha S (AMC Engineering College, Bengaluru)  
**Deliverable**: Week 2 Task Report (`reports/weekly/Week2.docx`)

---

## 1. Overview of Week 2 Objectives

Week 2 transitions the strategic plan from Week 1 into hands-on data engineering, source verification, quality auditing, cleaning, and leak-free feature engineering. 

### Key Deliverables Completed
1. **Official Data Sourcing**: Downloaded and authenticated the primary government dataset: *District-wise, Season-wise Crop Production Statistics from 1997* published by the Directorate of Economics and Statistics (DES), Ministry of Agriculture and Farmers Welfare, Government of India.
2. **Raw Schema Inspection**: Verified the raw file (`crop_production_raw.csv`) containing 246,091 records and 7 attributes.
3. **Data Quality Audit**: Quantified missing values (3,730 missing production records), audited duplicates (0 exact duplicate rows, 0 administrative key collisions), and checked numeric limits.
4. **Data Cleaning & Harmonization**: Standardized categorical strings, trimmed trailing whitespaces, resolved measurement unit heterogeneity (segregating 1,958 Coconut records reported in thousand nuts from 240,403 metric tonne crops), and flagged 190 biological outliers using ICAR physiological maximum yield ceilings.
5. **Feature Engineering**: Engineered target variable $\text{Yield} = \frac{\text{Production}}{\text{Area}}$ ($t/\text{ha}$), `Log_Area`, `Year_Index`, `Is_Kharif_Monsoon`, `Farm_Scale`, `Crop_Category`, and `Hist_Crop_State_Yield`.
6. **Cleaned Dataset Export**: Produced certified `crop_production_cleaned.csv` (242,361 rows, 11 columns) stored under `dataset/`.
7. **Automated Unit Tests**: Built and executed automated tests in `tests/test_preprocessing.py` and `tests/test_features.py` verifying data schema and transformation consistency.

---

## 2. Before-and-After Pipeline Summary Table

| Metric / Dimension | Raw Dataset (`crop_production_raw.csv`) | Cleaned Dataset (`crop_production_cleaned.csv`) | Transformation Action & Justification |
|:---|:---:|:---:|:---|
| **Total Rows** | 246,091 | **242,361** | 3,730 rows with null target (`Production`) removed (98.48% retention) |
| **Total Columns** | 7 | **11** | Expanded with `Unit_Type`, `Yield`, `Max_Plausible_Yield`, `is_outlier_yield` |
| **Missing Production** | 3,730 (1.516%) | **0 (0.00%)** | Excluded from supervised target to prevent synthetic ground-truth fabrication |
| **Missing Cultivated Area** | 0 (0.00%) | **0 (0.00%)** | Cultivated acreage verified complete for all observations |
| **Zero Area Records (`Area <= 0`)** | 0 (0.00%) | **0 (0.00%)** | Zero-division errors prevented in Yield calculation |
| **Zero Production Records** | 3,523 (1.432%) | **3,523 (1.453%)** | Retained with `Yield = 0.00 t/ha` (genuine drought/pest crop failure events) |
| **String Formatting** | Trailing spaces (`'Kharif   '`) | Fully normalized | Applied string trimming, Title Case for States, UPPERCASE for Districts |
| **Unit Heterogeneity** | Mixed metrics (Nuts & Tonnes) | Formally segregated | Tagged 1,958 Coconut rows with `Unit_Type = "Thousand Nuts"` |
| **Biological Outliers** | Unchecked entries (e.g. 88,000 t/ha) | Flagged via ICAR ceilings | Flagged 190 records (0.078%) as `is_outlier_yield = True` |

---

## 3. Weekly Documentation Structure

Detailed documentation for Week 2 is organized across the following dedicated documents:
- [Data Acquisition](file:///c:/Users/Sangeetha%20Suresh/Downloads/yuvaintern.agriyield-ai/internship/week2/data_acquisition.md): Provenance, source metadata, download verification, and schema profiling.
- [Data Preparation](file:///c:/Users/Sangeetha%20Suresh/Downloads/yuvaintern.agriyield-ai/internship/week2/data_preparation.md): Cleaning rules, missingness handling, unit partitioning, and ICAR outlier bounding.
- [Feature Engineering](file:///c:/Users/Sangeetha%20Suresh/Downloads/yuvaintern.agriyield-ai/internship/week2/feature_engineering.md): Agronomic feature derivation, leakage prevention, and mathematical formulations.
