# AgriYield AI — Weekly Internship Reports Dossier

**Author**: Sangeetha S  
**Institution**: AMC College of Engineering, Bengaluru  
**Track**: Junior Machine Learning Data Analyst — Agriculture & Agribusiness  
**Internship Organization**: YuvaIntern  
**Project**: Agricultural Crop Yield Prediction and Agribusiness Decision Support System Using Machine Learning (AgriYield AI)  
**Repository**: [github.com/sangeetha302005/yuvaintern.agriyield-ai](https://github.com/sangeetha302005/yuvaintern.agriyield-ai)  
**Live Application**: [agriyield-ai-302005.streamlit.app](https://agriyield-ai-302005.streamlit.app/)

---

## 1. Executive Summary & Repair Register

All four weekly internship reports have been generated, repaired, and validated in strict adherence to **ISO/IEC 29500 / ECMA-376 Office Open XML (DOCX)** standards. 

### Why This Repair Was Required
On mobile devices (e.g. Android Microsoft Word, Google Docs, WPS Office) and certain desktop viewers, previous document exports or Git checkouts with automated CRLF line-ending translations caused binary ZIP header corruption. This resulted in mobile applications falling back to raw plain-text viewing, rendering raw OpenXML tags (`PK [Content_Types].xml`, `word/document.xml`, `docProps/app.xml`).

### How the Issue Was Permanently Resolved
1. **Repository Binary Protection**: Configured `.gitattributes` with `*.docx binary` to permanently forbid Git from applying CRLF transformations to document files.
2. **Clean OpenXML Generation**: Every weekly report was generated from the ground up using `python-docx` with standards-compliant OpenXML package structures.
3. **Typography & Styling**: Formatted with 1.0-inch page margins, Calibri typography (11pt body, 15pt bold green `#1B5E20` H1 headings, 12.5pt H2 headings), justified paragraphs, custom cell padding, and alternating row shading.
4. **Headers, Footers & Dynamic Pagination**: Integrated running headers and dynamic `PAGE` / `NUMPAGES` Word fields in the footers.
5. **Enhanced Visual Evidence Suite**: Embedded 37 genuine, high-resolution figures across all four weekly documents, with special emphasis on **Data Cleaning (Week 2)**, **Exploratory Data Analysis (Week 3)**, and **Model Evaluation & Deployment Safeguards (Week 4)**.

---

## 2. Seven-Point Formal Validation Scorecard

Every deliverable in this directory has undergone programmatic inspection against the 7 mandatory quality checks:

| Deliverable | File Size | Paragraphs | Tables | Embedded Figures | Word Count | 7-Point Audit Status |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| [`Week1.docx`](./Week1.docx) | 582,107 B | 79 | 7 | 3 | 1,564 | **PASSED** |
| [`Week2.docx`](./Week2.docx) | 948,084 B | 106 | 13 | 10 | 2,822 | **PASSED** |
| [`Week3.docx`](./Week3.docx) | 1,032,287 B | 123 | 13 | 12 | 2,896 | **PASSED** |
| [`Week4.docx`](./Week4.docx) | 1,172,511 B | 143 | 17 | 12 | 4,981 | **PASSED** |

### Audit Criteria Definition
1. **Valid ZIP-Based Container**: Verified via `zipfile.ZipFile.testzip()`.
2. **`[Content_Types].xml` Presence**: Confirmed MIME content-type mapping for WordprocessingML.
3. **`word/document.xml` Presence**: Confirmed main document XML stream.
4. **Programmatic Open**: Verified zero schema or relationship errors upon load in `python-docx`.
5. **Text & Data Extraction**: Complete body paragraphs, tables, and worked equations extracted without truncation.
6. **Embedded Relationship Integrity**: All PNG images verified with valid Part URIs and dimensions.
7. **Format & Extension Verification**: Validated authentic `.docx` MIME type `application/vnd.openxmlformats-officedocument.wordprocessingml.document`.

---

## 3. Weekly Report Contents & Embedded Visual Evidence

### Week 1 — Strategic Design & Planning
- **Focus**: Problem formulation, public data acquisition plan (DES APY & FAOSTAT), feature engineering definitions, risk mitigation, and evaluation KPIs.
- **Embedded Figures**:
  - `Figure 1`: 10-Phase End-to-End Data Science and Machine Learning Lifecycle (`screenshots/week1/project_methodology_lifecycle.png`)
  - `Figure 2`: Multi-Tier System Architecture and Technological Component Stack (`screenshots/week1/system_architecture_stack.png`)
  - `Figure 3`: YuvaIntern Internship Program Overview and Four-Week Milestone Roadmap (`screenshots/week1/yuva_internship_program_overview.png`)

### Week 2 — Data Acquisition & Preparation
- **Focus**: Empirical data profiling, ground truth preservation, handling 3,730 null production rows, partitioning 1,958 Coconut rows (Thousand Nuts), ICAR biological bounding (190 flagged outliers), and target normalization.
- **Embedded Figures**:
  - `Figure 1`: Cleaned 242,361-Record Dataset Schema and Data Types Summary (`screenshots/week2/clean_dataset_schema_summary.png`)
  - `Figure 2`: Comprehensive Data Quality Audit Breakdown and Defect Resolution Summary (`screenshots/week2/data_quality_audit_breakdown.png`)
  - `Figure 3`: Missing Value Analysis: Dropping 3,730 Null Production Records to Preserve Ground Truth (`screenshots/week2/missing_value_analysis_before_after.png`)
  - `Figure 4`: Unit Heterogeneity Resolution: Partitioning Coconut (Thousand Nuts) from Metric Tonnes (`screenshots/week2/unit_heterogeneity_coconut_resolution.png`)
  - `Figure 5`: ICAR Biological Agronomic Yield Bounding and Outlier Screening (`screenshots/week2/icar_biological_yield_bounding.png`)
  - `Figure 6`: Feature Engineering: Target Distribution Normalization and Skewness Reduction (`screenshots/week2/feature_engineering_log_transform.png`)
  - `Figure 7`: Number of Prepared Records by Agricultural Season (`screenshots/week2/fig1_records_by_season.png`)
  - `Figure 8`: Ten Crops with Highest Record Counts in Prepared Dataset (`screenshots/week2/fig2_top_10_crops_records.png`)
  - `Figure 9`: Distribution of Non-Flagged Metric-Tonne Yield Records (`screenshots/week2/fig3_yield_distribution_99th.png`)
  - `Figure 10`: Top 12 Agricultural Commodities in India Ranked by Historical Production Volume (`screenshots/week2/top-12-crops-by-historical-production.png`)

### Week 3 — Execution of Data Analysis & Modeling
- **Focus**: Multi-dimensional Exploratory Data Analysis, chronological train/test split (1997–2011 vs 2012–2015), 4-model benchmarking (Baseline, Ridge, Random Forest, HistGradientBoosting), segmented crop/season analysis, and transparent target leakage disclosure.
- **Embedded Figures**:
  - `Figure 1`: Seasonal Yield Density Distribution & Extreme Value Dynamics Across Indian Crop Seasons (`screenshots/week3/seasonal_yield_distribution.png`)
  - `Figure 2`: Monsoon Impact Analysis: Kharif vs Rabi Productivity Comparison (`screenshots/week3/monsoon_impact_kharif_vs_rabi.png`)
  - `Figure 3`: Crop Yield Historical Trends Across Major Commodities (`screenshots/week3/crop_yield_trends.png`)
  - `Figure 4`: Top 10 Major Agricultural Commodities Yield Dispersion and Interquartile Spread (`screenshots/week3/crop_yield_boxplots_top_crops.png`)
  - `Figure 5`: State-Wise Agricultural Productivity Map: Historical Yield Disparities Across India (`screenshots/week3/state_wise_yield_productivity_map.png`)
  - `Figure 6`: State-Wise Total Historical Crop Production Volume Contribution Ranking (`screenshots/week3/state_production_ranking.png`)
  - `Figure 7`: Multi-Feature Correlation Matrix Heatmap Across Engineered Agricultural Predictors (`screenshots/week3/correlation_matrix_heatmap.png`)
  - `Figure 8`: Recorded Model Benchmark R² Comparison (`screenshots/week3/fig2_model_benchmark_r2.png`)
  - `Figure 9`: HistGradientBoosting Relative Feature Importance Ranking (`screenshots/week3/feature_importance_ranking.png`)
  - `Figure 10`: MAE for Ten Major Crops by Test Sample Count (`screenshots/week3/fig3_histgb_mae_top_crops.png`)
  - `Figure 11`: Model R² by Agricultural Season (`screenshots/week3/fig4_histgb_r2_seasons.png`)
  - `Figure 12`: Actual vs. Predicted Yield Parity Plot Demonstrating Model Fit and Residual Dispersion (`screenshots/week3/actual_vs_predicted_parity.png`)

### Week 4 — Final Project Evaluation & Agribusiness Recommendations
- **Focus**: Consolidated project evaluation scorecard, automated CI/CD Pytest verification (11/11 passing), model risk and critical technical review, agribusiness decision matrix, and production Streamlit application overview.
- **Embedded Figures**:
  - `Figure 1`: AgriYield AI End-to-End Evaluation Scorecard Across Data, Modeling, and Engineering (`screenshots/week4/end_to_end_evaluation_scorecard.png`)
  - `Figure 2`: Production Streamlit Application — Hero Interface and Interactive Overview (`screenshots/application/app_hero_landing_overview.png`)
  - `Figure 3`: Number of Prepared Records by Season (`screenshots/week4/fig1_records_by_season.png`)
  - `Figure 4`: Ten Most Represented Crops in Prepared CSV (`screenshots/week4/fig2_top_10_crops_records.png`)
  - `Figure 5`: Comprehensive 4-Model Benchmark Comparison: MAE, RMSE, and R² (`screenshots/week4/model_benchmark_comparison.png`)
  - `Figure 6`: Segmented Model R² Performance Across Major Crops (`screenshots/week4/fig4_recorded_crop_r2.png`)
  - `Figure 7`: Crop-Wise Absolute Error Breakdown (MAE) Across Major Commodities (`screenshots/week4/crop_wise_error_breakdown_mae.png`)
  - `Figure 8`: Seasonal Model Performance Breakdown (`screenshots/week4/seasonal_model_performance_r2.png`)
  - `Figure 9`: Model Prediction Residual Distribution and Error Symmetry Diagnostics (`screenshots/week4/residual_distribution.png`)
  - `Figure 10`: Actual vs. Predicted Parity Plot Demonstrating Model Fit Across Held-Out Test Records (`screenshots/week4/actual_vs_predicted_parity.png`)
  - `Figure 11`: Agribusiness Strategic Decision Matrix: Deployment Readiness vs Agronomic Risk (`screenshots/week4/agribusiness_decision_matrix.png`)
  - `Figure 12`: Automated CI/CD Pytest Verification Suite — 11/11 Unit Tests Passing in 7.05s (`screenshots/week4/pytest_test_verification.png`)

---

## 4. Key Data & Empirical Benchmarks

### Prepared Dataset Counts
- **Raw Records Ingested**: 246,091 rows
- **Missing Production Dropped**: 3,730 rows (preserves empirical ground truth)
- **Prepared Processed CSV**: **242,361 rows** (`data/processed/crop_production_cleaned.csv`)
- **Coconut Records (Thousand Nuts)**: 1,958 rows (`Unit_Type = 'Thousand Nuts'`)
- **Metric Tonne Crops**: 240,403 rows (`Unit_Type = 'Metric Tonnes'`)
- **ICAR Biological Yield Outliers Flagged**: 190 rows (`is_outlier_yield = True`)
- **Non-Outlier Metric Tonne Rows**: 240,213 rows (used for machine-learning modeling)

### Chronological Model Benchmark Performance (Test Period: 2012–2015, N = 37,726)
| Model | MAE (t/ha) | RMSE (t/ha) | R² Score | Deployment Decision |
| :--- | :---: | :---: | :---: | :--- |
| **Baseline (Train Mean)** | 5.6576 | 12.5961 | -0.0027 | Reject (Naive benchmark) |
| **Ridge Regression** | 1.3765 | 4.5257 | 0.8706 | Secondary benchmark |
| **Random Forest (60 Trees)** | **1.2434** | 4.5536 | 0.8690 | Competitive ensemble |
| **HistGradientBoosting (Champion)** | 1.2562 | **4.5183** | **0.8710** | **Designated Champion Model** |

---

## 5. Mobile & Desktop Viewing Guidance

To open and view these reports without formatting issues:
1. **Android & iOS Devices**: Open directly using the official **Microsoft 365 / Microsoft Word** app or **Google Docs**. 
2. **Desktop (Windows / macOS / Linux)**: Open with **Microsoft Word 2016+**, **LibreOffice 7.0+**, or **WPS Office**.
3. **Backup Copies**: Pristine copies of the original files prior to repair are safely maintained in the `backup_originals/` subdirectory.
