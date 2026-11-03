# AgriYield AI — Agricultural Crop Yield Prediction & Decision Support System

[![YuvaIntern Internship](https://img.shields.io/badge/YuvaIntern-Internship%202026-brightgreen.svg)](https://yuvaintern.com)
[![Role: Junior ML Data Analyst](https://img.shields.io/badge/Role-Junior%20ML%20Data%20Analyst-blue.svg)](#)
[![Python 3.11](https://img.shields.io/badge/Python-3.11.7-blue.svg)](https://python.org)
[![Streamlit App](https://img.shields.io/badge/Streamlit-Live%20App-FF4B4B.svg)](https://agriyield-ai-302005.streamlit.app/)
[![Tests](https://img.shields.io/badge/Pytest-11%20Passed-success.svg)](#)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

> **Internship Context**: Developed during the **YuvaIntern** 4-Week Internship Program (01 October 2026 – 29 October 2026) in the domain track **Junior Machine Learning Data Analyst — Agriculture & Agribusiness**.  
> **Candidate**: Sangeetha S | **Institution**: AMC Engineering College, Bengaluru  
> **Repository**: [https://github.com/sangeetha302005/yuvaintern.agriyield-ai](https://github.com/sangeetha302005/yuvaintern.agriyield-ai)

---

## LIVE APPLICATION

The AgriYield AI web application is live and accessible online:

**Live URL**: [https://agriyield-ai-302005.streamlit.app/](https://agriyield-ai-302005.streamlit.app/)

*(Official Submission Reference: `https://agriyield-ai-302005.streamlit.app/`)*

---

## 1. Project Overview

**AgriYield AI** is an end-to-end agricultural data analytics, machine learning, and decision-support system designed to analyze multi-decade agricultural productivity and provide leak-free crop yield predictions across India.

Utilizing official historical records (1997–2015) from the **Ministry of Agriculture and Farmers Welfare, Government of India**, AgriYield AI processes 242,361 cleaned observations across 33 States/UTs, 646 districts, and 124 crop varieties. The system implements an out-of-time chronological validation strategy (Train: 1997–2011; Test: 2012–2015) and evaluates regression architectures (Ridge Regression, Random Forest, and Histogram-based Gradient Boosting). The champion model achieves an **$R^2$ score of 0.8710** and an **MAE of 1.2562 t/ha** on unseen future harvest years, outperforming the baseline mean predictor by 77.8%.

---

## 2. Problem Statement

1. **Extreme Yield Volatility**: Crop productivity across Indian districts fluctuates significantly due to monsoon variability, regional soil conditions, and shifting seasonal dynamics.
2. **Administrative Data Inconsistencies**: Historical government datasets contain mixed reporting units (e.g. food grains in metric tonnes vs. coconuts in thousand nuts), missing harvest returns, and transcription errors.
3. **Pervasive Target Leakage in ML**: Naive crop prediction models often include post-harvest production data as inputs to predict yield ($\text{Yield} = \frac{\text{Production}}{\text{Area}}$), resulting in artificially inflated test scores that fail in real-world pre-harvest deployment.
4. **Lack of Accessible Decision Support Tools**: Agribusiness stakeholders, farmer producer organizations (FPOs), and agricultural planners often lack intuitive digital interfaces to explore historical trends and evaluate pre-sowing scenarios.

---

## 3. Key Objectives

- **Source Provenance**: Ingest and preserve multi-decade agricultural statistics from the Government of India Open Government Data (OGD) platform.
- **Data Quality Engineering**: Conduct missing-value audits, enforce ICAR physiological yield bounds, segregate mixed measurement units, and establish clean analytical uniqueness.
- **Leak-Free Modeling**: Engineer pre-harvest features (`Log_Area`, `Year_Index`, `Is_Kharif_Monsoon`, `Farm_Scale`, `Hist_Crop_State_Yield`) strictly isolated from post-harvest outcomes.
- **Chronological Benchmarking**: Benchmark regression candidates against an unconditioned baseline using an out-of-time chronological split (1997–2011 Train / 2012–2015 Test).
- **Interactive Delivery**: Provide a web application featuring an interactive yield prediction engine, historical data explorer, and custom CSV dataset uploader.
- **Agribusiness Decision Support**: Formulate evidence-based recommendations for crop portfolio diversification, risk-weighted procurement contract sizing, and climate-adaptive planning.

---

## 4. Existing Application Features

The existing Streamlit web application (`application/app.py`) provides five modular analytical capabilities:

1. **System Overview & KPI Telemetry**: High-level summary cards (242,361 records, 124 crops, 33 states), project methodology, and architectural roadmap.
2. **Historical Data Explorer**: Dynamic multi-filter explorer (State, District, Crop, Season) displaying multi-decade production trajectories and seasonal yield distributions.
3. **Interactive Yield Prediction**: Real-time pre-harvest ML inference engine. Users select region, crop, season, and acreage to receive instant yield predictions ($t/\text{ha}$ and total expected tonnes) alongside confidence bands.
4. **Data Quality Audit & Explorer**: Interactive transparency tool displaying data retention, missing value counts, and ICAR outlier distributions.
5. **Custom CSV Uploader & Analyzer**: Enables users to upload their own agricultural datasets, validating schema columns and generating automated EDA charts.

---

## 5. Dataset Source and Description

| Metadata Attribute | Specification |
|:---|:---|
| **Dataset File** | `dataset/crop_production_cleaned.csv` |
| **Original Dataset Title** | District-wise, Season-wise Crop Production Statistics from 1997 |
| **Publisher** | Directorate of Economics and Statistics (DES), Ministry of Agriculture and Farmers Welfare, Govt of India |
| **Official Source Portal** | [data.gov.in (Resource ID 87630)](https://data.gov.in/resource/district-wise-season-wise-crop-production-statistics-1997) |
| **Direct Endpoint** | `https://aps.dac.gov.in/APY/apy.csv` |
| **Licence** | Government Open Data License - India (GODL) |
| **Record Count** | **242,361** cleaned records (from 246,091 raw records; 98.48% retention) |
| **Feature Count** | **11** columns |
| **Temporal Span** | 1997 to 2015 (18 agricultural years) |
| **Geographic Coverage** | 33 States and Union Territories, 646 Administrative Districts |
| **Commodity Coverage** | 124 agricultural crops |

For complete column descriptions, data types, units, and transformation details, see [dataset/README.md](dataset/README.md) and [documentation/data_dictionary.md](documentation/data_dictionary.md).

---

## 6. Technology Stack

- **Core Runtime**: Python 3.11.7
- **Data Engineering**: Pandas 2.x, NumPy
- **Machine Learning**: Scikit-Learn (Pipelines, Ridge, Random Forest, HistGradientBoosting)
- **Web Application**: Streamlit 1.65.0
- **Interactive Visualizations**: Plotly, Matplotlib, Seaborn
- **Automated Testing**: Pytest 7.4.0 (11/11 tests passing)
- **Artifact Serialization**: Joblib

---

## 7. Project Structure

```text
yuvaintern.agriyield-ai/
├── README.md                                 # Primary repository guide & overview
├── LICENSE                                   # MIT Open Source License
├── .gitignore                                # Git ignore specification
│
├── application/                              # Complete AgriYield AI application
│   ├── app.py                                # Streamlit multi-tab application
│   ├── requirements.txt                      # Application dependencies
│   ├── Dockerfile                            # Docker containerization config
│   ├── .streamlit/                           # Streamlit configuration
│   ├── src/                                  # Core modular source code
│   │   ├── data/                             # Data loading and cleaning
│   │   ├── features/                         # Pre-harvest feature engineering
│   │   ├── models/                           # Training, evaluation & inference
│   │   └── visualization/                    # Plotly chart generators
│   ├── models/                               # Serialized models & metadata
│   │   ├── best_yield_model.joblib           # Champion HistGradientBoosting pipeline
│   │   └── model_metadata.json               # Model configuration & benchmark metrics
│   ├── notebooks/                            # Exploratory & experimental notebooks
│   ├── reports/                              # Automated data & model markdown reports
│   └── tests/                                # Automated unit test suite
│
├── dataset/                                  # Processed agricultural dataset
│   ├── crop_production_cleaned.csv           # 242,361 certified records (11 columns)
│   └── README.md                             # Dataset provenance & data dictionary
│
├── internship/                               # Complete weekly internship documentation
│   ├── week1/
│   │   └── tasks.md                          # Week 1 introduction & strategic design
│   ├── week2/
│   │   ├── tasks.md                          # Week 2 summary
│   │   ├── data_acquisition.md               # Data sourcing & provenance
│   │   ├── data_preparation.md               # Quality auditing & cleaning
│   │   └── feature_engineering.md            # Leak-free agronomic features
│   ├── week3/
│   │   ├── tasks.md                          # Week 3 summary
│   │   ├── exploratory_data_analysis.md      # Multi-decade EDA & distributions
│   │   ├── machine_learning.md               # ML formulation & temporal split
│   │   └── model_evaluation.md               # Model benchmarking & residual analysis
│   └── week4/
│       ├── tasks.md                          # Week 4 summary
│       ├── project_evaluation.md             # System testing & test suite audit
│       └── recommendations.md                # Agribusiness decision-support framework
│
├── reports/                                  # Formal Word (.docx) internship reports
│   ├── weekly/
│   │   ├── Week1.docx                        # Submitted Week 1 Strategic Plan
│   │   ├── Week2.docx                        # Completed Week 2 Preparation Report
│   │   ├── Week3.docx                        # Completed Week 3 Modeling Report
│   │   └── Week4.docx                        # Completed Week 4 Evaluation Report
│   └── final/
│       └── AgriYield_AI_Final_Internship_Report.docx  # Consolidated 22-section final report
│
├── documentation/                            # Technical system documentation
│   ├── screenshot_checklist.md               # Visual evidence audit & checklist
│   ├── project_architecture.md               # Architecture diagrams & component design
│   ├── data_dictionary.md                    # Attribute specifications & validation rules
│   ├── test_plan_and_results.md              # Automated test plan & pytest run logs
│   └── YuvaIntern_Offer_Letter.pdf           # Official internship appointment letter
│
└── screenshots/                              # Visual evidence repository
    ├── week1/                                # Program overview & offer letter
    ├── week2/                                # Data quality audit & top crops
    ├── week3/                                # Yield trajectories, states & parity
    ├── week4/                                # Model benchmark, residuals & test proof
    └── application/                          # Application assets & UI checklist
```

---

## 8. Weekly Internship Work & Deliverables

All four weekly internship Word documents have been regenerated, styled, verified, and embedded with **37 authentic high-resolution figures** in strict accordance with **ISO/IEC 29500 / ECMA-376 Office Open XML (DOCX)** standards. They are fully compatible with desktop Microsoft Word, Google Docs, and mobile viewers (Android / iOS) without raw XML display artifacts.

| Week | Focus Area | Key Deliverables Completed | Embedded Figures | Word Count | Formal Report Link |
|:---:|:---|:---|:---:|:---:|:---:|
| **Week 1** | Strategic Design & Planning | Problem definition, public data sourcing plan (DES APY & FAOSTAT), feature engineering rules, KPIs, risk mitigation, timeline | 3 figures | 1,564 | [reports/weekly/Week1.docx](reports/weekly/Week1.docx) |
| **Week 2** | Data Acquisition & Preparation | Ingested 246,091 raw rows, missing target handling (3,730 nulls dropped), unit segregation (Coconut in thousand nuts), ICAR yield bounding (190 flagged), 11 engineered features | 10 figures | 2,822 | [reports/weekly/Week2.docx](reports/weekly/Week2.docx) |
| **Week 3** | Data Analysis & Modeling | 18-year multi-dimensional EDA, chronological validation (1997–2011 Train / 2012–2015 Test), Ridge, Random Forest, HistGradientBoosting benchmarking, target leakage transparency | 12 figures | 2,896 | [reports/weekly/Week3.docx](reports/weekly/Week3.docx) |
| **Week 4** | Evaluation & Recommendations | Pytest suite (11/11 passed in 7.05s), residual symmetry diagnostics, 5 agribusiness strategic recommendations, final deployment review | 12 figures | 4,981 | [reports/weekly/Week4.docx](reports/weekly/Week4.docx) |

> 📋 **Quality Assurance Dossier**: For full 7-point audit results, technical root-cause analysis, and mobile viewing instructions, see [reports/weekly/README.md](reports/weekly/README.md).  
> 🔄 **Reproducible Report Generator**: All four documents can be programmatically re-built and validated via `python reports/weekly/generate_weekly_reports.py`.  
> 📦 **Pristine Backups**: Original document backups prior to repair are archived in [`reports/weekly/backup_originals/`](reports/weekly/backup_originals/).

### Consolidated Final Report
The complete 4-week internship lifecycle has been consolidated into a publication-quality final report:
- **Consolidated Final Report**: [reports/final/AgriYield_AI_Final_Internship_Report.docx](reports/final/AgriYield_AI_Final_Internship_Report.docx)

---

## 9. Machine Learning Benchmarking Results

Models were evaluated on the held-out out-of-time test set (37,726 records from 2012–2015):

| Model Candidate | MAE ($t/\text{ha}$) | RMSE ($t/\text{ha}$) | $R^2$ Score | Training Time (s) | Evaluation Note |
|:---|:---:|:---:|:---:|:---:|:---|
| **Baseline (Mean)** | 5.6576 | 12.5961 | -0.0027 | 0.00s | Unconditioned historical training mean ($4.2809\text{ t/ha}$) |
| **Ridge Regression** | 1.3765 | 4.5257 | 0.8706 | 0.35s | L2 regularized linear model with standard scaling |
| **Random Forest Regressor** | 1.2434 | 4.5536 | 0.8690 | 5.88s | 60 trees, max depth 14, min leaf 10 |
| **HistGradientBoosting** | **1.2562** | **4.5183** | **0.8710** | 5.96s | **Champion Model**: Lowest RMSE, highest $R^2$ (0.8710) |

### Subgroup Highlights (Champion Model)
- **Rice**: $\text{MAE} = 0.5382\text{ t/ha}$, $R^2 = 0.3814$ across 2,490 test samples.
- **Wheat**: $\text{MAE} = 0.4799\text{ t/ha}$, $R^2 = 0.6452$ across 1,139 test samples.
- **Moong (Green Gram)**: $\text{MAE} = 0.1520\text{ t/ha}$ across 1,893 test samples.
- **Sugarcane**: $\text{MAE} = 12.8607\text{ t/ha}$, $R^2 = 0.5162$ across 1,229 test samples (reflecting normal $\sim 20\%$ relative error on high-biomass crops).
- **Residual Distribution**: Mean residual error = $+0.2276\text{ t/ha}$ (near-zero directional bias).

---

## 10. Screenshot Evidence Master Catalogue

A total of 37 visual artifacts are embedded across the weekly reports and application documentation:

| Domain / Milestone | Visual Artifact | What It Demonstrates | Verified File Path |
|:---|:---|:---|:---|
| **Week 1 Planning** | Project Methodology Lifecycle | 10-phase end-to-end data science lifecycle from business problem to deployment | [screenshots/week1/project_methodology_lifecycle.png](screenshots/week1/project_methodology_lifecycle.png) |
| **Week 1 Architecture** | System Architecture Stack | Multi-tier technical architecture (Data, Feature, ML, UI, CI/CD, Docker) | [screenshots/week1/system_architecture_stack.png](screenshots/week1/system_architecture_stack.png) |
| **Week 1 Overview** | Internship Program Roadmap | YuvaIntern 4-week roadmap, deliverables, and role specifications | [screenshots/week1/yuva_internship_program_overview.png](screenshots/week1/yuva_internship_program_overview.png) |
| **Week 2 Data Prep** | Cleaned Schema Summary | Schema structure, data types, and record volume (242,361 rows) | [screenshots/week2/clean_dataset_schema_summary.png](screenshots/week2/clean_dataset_schema_summary.png) |
| **Week 2 Cleaning** | Quality Audit Breakdown | Donut chart: 98.41% yield-ready records, 1.52% null production dropped | [screenshots/week2/data_quality_audit_breakdown.png](screenshots/week2/data_quality_audit_breakdown.png) |
| **Week 2 Cleaning** | Missing Value Analysis | Before vs. After cleaning: 3,730 null production entries dropped to preserve ground truth | [screenshots/week2/missing_value_analysis_before_after.png](screenshots/week2/missing_value_analysis_before_after.png) |
| **Week 2 Units** | Coconut Heterogeneity | Segregation of Coconut (Thousand Nuts) from metric-tonne food grains | [screenshots/week2/unit_heterogeneity_coconut_resolution.png](screenshots/week2/unit_heterogeneity_coconut_resolution.png) |
| **Week 2 Outliers** | ICAR Biological Bounding | Physiological maximum yield bounding (190 records flagged transparently) | [screenshots/week2/icar_biological_yield_bounding.png](screenshots/week2/icar_biological_yield_bounding.png) |
| **Week 2 Engineering** | Logarithmic Transformation | Pre-harvest feature normalization and yield skewness reduction | [screenshots/week2/feature_engineering_log_transform.png](screenshots/week2/feature_engineering_log_transform.png) |
| **Week 2 Commodities** | Top 12 Crops Production | Historical production volume distribution across top Indian crops | [screenshots/week2/top-12-crops-by-historical-production.png](screenshots/week2/top-12-crops-by-historical-production.png) |
| **Week 3 EDA** | Seasonal Yield Dynamics | Density distribution across Kharif, Rabi, Summer, Autumn, Winter | [screenshots/week3/seasonal_yield_distribution.png](screenshots/week3/seasonal_yield_distribution.png) |
| **Week 3 Monsoon** | Kharif vs Rabi Impact | Monsoon-fed (Kharif) vs. irrigated winter (Rabi) productivity comparison | [screenshots/week3/monsoon_impact_kharif_vs_rabi.png](screenshots/week3/monsoon_impact_kharif_vs_rabi.png) |
| **Week 3 Longitudinal** | Crop Yield Trends | Multi-decade longitudinal yield trends across major agricultural commodities | [screenshots/week3/crop_yield_trends.png](screenshots/week3/crop_yield_trends.png) |
| **Week 3 Spread** | Top Crops Boxplots | Interquartile dispersion and yield variability across top 10 crops | [screenshots/week3/crop_yield_boxplots_top_crops.png](screenshots/week3/crop_yield_boxplots_top_crops.png) |
| **Week 3 Spatial** | State Productivity Map | State-wise agricultural yield productivity disparities across India | [screenshots/week3/state_wise_yield_productivity_map.png](screenshots/week3/state_wise_yield_productivity_map.png) |
| **Week 3 Ranking** | State Production Ranking | Total agricultural output contribution ranked across 33 States/UTs | [screenshots/week3/state_production_ranking.png](screenshots/week3/state_production_ranking.png) |
| **Week 3 Features** | Correlation Matrix Heatmap | Multi-feature correlation matrix across engineered agricultural predictors | [screenshots/week3/correlation_matrix_heatmap.png](screenshots/week3/correlation_matrix_heatmap.png) |
| **Week 3 Modeling** | Benchmark R² Comparison | Recorded model comparison: Baseline (-0.0027) vs HistGB (0.8710) | [screenshots/week3/fig2_model_benchmark_r2.png](screenshots/week3/fig2_model_benchmark_r2.png) |
| **Week 3 Importance** | Feature Importance Ranking | HistGradientBoosting relative feature importance breakdown | [screenshots/week3/feature_importance_ranking.png](screenshots/week3/feature_importance_ranking.png) |
| **Week 3 Residuals** | Actual vs Predicted Parity | Parity plot on out-of-time test set (2012–2015, N = 37,726) | [screenshots/week3/actual_vs_predicted_parity.png](screenshots/week3/actual_vs_predicted_parity.png) |
| **Week 4 Evaluation** | Project Evaluation Scorecard | End-to-end evaluation scorecard across data, ML, and software engineering | [screenshots/week4/end_to_end_evaluation_scorecard.png](screenshots/week4/end_to_end_evaluation_scorecard.png) |
| **Week 4 Application** | Live Streamlit UI Overview | Hero interface and analytical telemetry of the deployed application | [screenshots/application/app_hero_landing_overview.png](screenshots/application/app_hero_landing_overview.png) |
| **Week 4 Benchmarks** | Multi-Model Comparison | Comprehensive 4-model comparison across MAE, RMSE, and R² | [screenshots/week4/model_benchmark_comparison.png](screenshots/week4/model_benchmark_comparison.png) |
| **Week 4 Errors** | Crop-Wise MAE Breakdown | Mean absolute error breakdown across major agricultural commodities | [screenshots/week4/crop_wise_error_breakdown_mae.png](screenshots/week4/crop_wise_error_breakdown_mae.png) |
| **Week 4 Seasons** | Seasonal R² Breakdown | Segmented model performance across individual agricultural seasons | [screenshots/week4/seasonal_model_performance_r2.png](screenshots/week4/seasonal_model_performance_r2.png) |
| **Week 4 Residuals** | Residual Distribution | Error symmetry diagnostics showing near-zero bias (+0.2276 t/ha) | [screenshots/week4/residual_distribution.png](screenshots/week4/residual_distribution.png) |
| **Week 4 Strategy** | Agribusiness Decision Matrix | Strategic decision matrix: deployment readiness vs. agronomic risk | [screenshots/week4/agribusiness_decision_matrix.png](screenshots/week4/agribusiness_decision_matrix.png) |
| **Week 4 CI/CD** | Pytest Test Verification | Automated test suite execution: 11/11 unit tests passing in 7.05s | [screenshots/week4/pytest_test_verification.png](screenshots/week4/pytest_test_verification.png) |

For complete checklist details and pending UI screenshots, see [documentation/screenshot_checklist.md](documentation/screenshot_checklist.md).

---

## 11. Installation & Local Execution

### Prerequisites
- Python 3.10 or 3.11
- Git

### Setup Steps
```powershell
# 1. Clone the repository
git clone https://github.com/sangeetha302005/yuvaintern.agriyield-ai.git
cd yuvaintern.agriyield-ai/application

# 2. Create and activate a virtual environment
python -m venv venv
.\venv\Scripts\Activate.ps1   # On Windows
# source venv/bin/activate    # On Linux / macOS

# 3. Install required dependencies
pip install -r requirements.txt

# 4. Run automated unit tests
$env:PYTHONPATH = "."
pytest

# 5. Launch the Streamlit application
streamlit run app.py
```
The application will launch locally at `http://localhost:8501`.

---

## 12. Limitations & Risk Management

1. **Macro-Level Aggregation**: Data represents district-level statistical aggregations; it does not capture farm-scale soil chemistry (NPK) or parcel-level micro-topography.
2. **Pre-Harvest Weather Shocks**: Extreme catastrophic weather shocks occurring days before harvest (unseasonal hailstorms, flash floods) cannot be anticipated from pre-harvest acreage features alone.
3. **Target Leakage Safeguard**: Harvest production is strictly excluded from candidate feature sets. Predictions represent expected statistical ranges for planning, not guaranteed individual farm yields.

---

## 13. References

1. Directorate of Economics and Statistics (DES), Ministry of Agriculture and Farmers Welfare, Government of India. *District-wise, Season-wise Crop Production Statistics from 1997*. [data.gov.in](https://data.gov.in/resource/district-wise-season-wise-crop-production-statistics-1997).
2. Government of India Open Data Catalogue. *District-wise, Season-wise Crop Production Statistics*. [delhi.data.gov.in](https://delhi.data.gov.in/catalog/district-wise-season-wise-crop-production-statistics-0).
3. Indian Council of Agricultural Research (ICAR). *Handbook of Agriculture: Facts and Figures for Farmers, Students and All Interested in Farming*. New Delhi: ICAR, 2020.
4. Food and Agriculture Organization of the United Nations (FAO). *FAOSTAT Statistical Database: Crop Production and Yields*. Rome: FAO, 2024.
5. van Klompenburg, T., Kassahun, A., & Catal, C. (2020). *Crop yield prediction using machine learning: A systematic literature review*. Computers and Electronics in Agriculture, 177, 105709.
6. Pedregosa, F., et al. (2011). *Scikit-learn: Machine Learning in Python*. Journal of Machine Learning Research, 12, 2825–2830.
