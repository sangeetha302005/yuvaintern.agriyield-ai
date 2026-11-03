# AgriYield AI — Screenshot Evidence Master Inventory & Audit

This master inventory catalogs all visual evidence artifacts, figures, analytical charts, and UI preview cards across the 4-week YuvaIntern internship lifecycle (**Junior Machine Learning Data Analyst — Agriculture & Agribusiness**).

All 38 visual artifacts have been generated, verified, and placed into their respective directories.

---

## 1. Master Screenshot Directory Summary

```text
screenshots/
├── week1/          # 4 artifacts: Program overview, Offer letter, Lifecycle, System architecture
├── week2/          # 7 artifacts: Data cleaning, Missingness, Coconut resolution, ICAR bounds, Log transform, Schema
├── week3/          # 10 artifacts: Longitudinal trends, Crop boxplots, State rankings, Correlation, Monsoon impact, Parity
├── week4/          # 8 artifacts: Benchmark scorecard, Crop MAE, Seasonal R², Residuals, Decision matrix, Pytest audit
└── application/    # 9 artifacts: Web application module previews (Landing, Explorer, Predictor, Audit, CSV Uploader)
```

---

## 2. Detailed Screenshot Inventory by Week

### Week 1 — Project Introduction, Strategic Design & Planning
| # | Filename | Description / What It Shows | Target Directory | Status |
|:---:|:---|:---|:---:|:---:|
| 1 | `yuva_internship_program_overview.png` | YuvaIntern 4-week internship roadmap, milestones, candidate role & objectives | `screenshots/week1/` | **Verified** |
| 2 | `YuvaIntern_Offer_Letter.pdf` | Official YuvaIntern Internship Appointment & Offer Letter for Sangeetha S | `screenshots/week1/` | **Verified** |
| 3 | `project_methodology_lifecycle.png` | 10-phase end-to-end data science lifecycle from business understanding to deployment | `screenshots/week1/` | **Verified** |
| 4 | `system_architecture_stack.png` | Multi-tier technical architecture diagram (Data, Feature, ML, UI, CI/CD, Container) | `screenshots/week1/` | **Verified** |

---

### Week 2 — Data Acquisition, Cleaning & Preparation
*Focus: Data cleaning, missingness treatment, unit segregation, biological outlier bounding, and feature transformations.*
| # | Filename | Description / What It Shows | Target Directory | Status |
|:---:|:---|:---|:---:|:---:|
| 5 | `missing_value_analysis_before_after.png` | Before vs. After cleaning comparison: 246,091 raw records vs. 242,361 cleaned records (3,730 null production entries dropped to protect ground truth) | `screenshots/week2/` | **Verified** |
| 6 | `data_quality_audit_breakdown.png` | Donut chart of raw dataset audit: 98.41% yield-ready records, 1.52% missing production, 0.08% biological outliers | `screenshots/week2/` | **Verified** |
| 7 | `unit_heterogeneity_coconut_resolution.png` | Coconut Unit Discrepancy analysis: pie distribution and logarithmic scale distortion showing why Coconut (Thousand Nuts) must be partitioned | `screenshots/week2/` | **Verified** |
| 8 | `icar_biological_yield_bounding.png` | Agronomic plausibility ceilings based on ICAR research benchmarks (Sugarcane 250 t/ha, Rice 15 t/ha, Wheat 12 t/ha, Pulses 6 t/ha) with 190 flagged outliers | `screenshots/week2/` | **Verified** |
| 9 | `feature_engineering_log_transform.png` | Cultivated acreage normalization: raw skewed Area (skewness > 30) vs. engineered Log_Area = ln(Area + 1) normalized bell curve | `screenshots/week2/` | **Verified** |
| 10 | `clean_dataset_schema_summary.png` | Certified schema summary card for `crop_production_cleaned.csv` (11 columns, data types, value ranges, and analytical roles) | `screenshots/week2/` | **Verified** |
| 11 | `top-12-crops-by-historical-production.png` | Historical production volume rankings across top 12 Indian agricultural commodities (Sugarcane, Rice, Wheat, etc.) | `screenshots/week2/` | **Verified** |

---

### Week 3 — Exploratory Data Analysis & Machine Learning Modeling
*Focus: Multi-decade yield patterns, crop diversity, state productivity hierarchies, seasonal regimes, and ML benchmarking.*
| # | Filename | Description / What It Shows | Target Directory | Status |
|:---:|:---|:---|:---:|:---:|
| 12 | `crop_yield_trends.png` | 18-year longitudinal yield trajectories (1997–2015) showing staple grain technological rise and severe drought drops in 2002 and 2009 | `screenshots/week3/` | **Verified** |
| 13 | `crop_yield_boxplots_top_crops.png` | Boxplot yield distributions (t/ha) across top 10 Indian field crops (Rice, Wheat, Maize, Pulses, Oilseeds) showing median, IQR, and natural variance | `screenshots/week3/` | **Verified** |
| 14 | `state_wise_yield_productivity_map.png` | Top 12 Indian States ranked by average agricultural productivity (t/ha) | `screenshots/week3/` | **Verified** |
| 15 | `state_production_ranking.png` | Top 10 Indian States by total historical agricultural production volume (Million Metric Tonnes) | `screenshots/week3/` | **Verified** |
| 16 | `seasonal_yield_distribution.png` | Productivity comparison (mean and median yield in t/ha) across 6 agricultural cropping seasons | `screenshots/week3/` | **Verified** |
| 17 | `monsoon_impact_kharif_vs_rabi.png` | Yield density curves comparing Kharif (monsoon-dependent) vs. Rabi (winter irrigated) stability | `screenshots/week3/` | **Verified** |
| 18 | `correlation_matrix_heatmap.png` | Agronomic correlation matrix heatmap between engineered numeric features (Area, Production, Yield, Log_Area, Year_Index, Is_Kharif) | `screenshots/week3/` | **Verified** |
| 19 | `feature_importance_ranking.png` | Champion HistGradientBoosting relative feature importance breakdown (Historical baseline, Log_Area, Crop, State) | `screenshots/week3/` | **Verified** |
| 20 | `actual_vs_predicted_parity.png` | Parity scatter plot comparing ground truth observed yields vs. predicted yields on the 2012–2015 holdout test set (R² = 0.8710) | `screenshots/week3/` | **Verified** |
| 21 | `top-12-crops-by-historical-production.png` | Multi-crop commodity distribution reference | `screenshots/week3/` | **Verified** |

---

### Week 4 — Project Evaluation, Software Testing & Recommendations
*Focus: Out-of-time model evaluation, software test verification, residual analysis, and agribusiness decision support.*
| # | Filename | Description / What It Shows | Target Directory | Status |
|:---:|:---|:---|:---:|:---:|
| 22 | `model_benchmark_comparison.png` | Multi-algorithm regression scorecard comparing Baseline (Mean), Ridge Regression, Random Forest, and HistGradientBoosting | `screenshots/week4/` | **Verified** |
| 23 | `crop_wise_error_breakdown_mae.png` | Horizontal bar chart of MAE (t/ha) across individual crops (Rice 0.54, Wheat 0.48, Moong 0.15, Sugarcane 12.86) with relative error bands | `screenshots/week4/` | **Verified** |
| 24 | `seasonal_model_performance_r2.png` | Champion model generalization: Explained variance (R²) across seasons (Kharif R²=0.9316, Rabi R²=0.8683) | `screenshots/week4/` | **Verified** |
| 25 | `residual_distribution.png` | Test set residual error distribution (Mean: +0.2276 t/ha, Std: 4.5126 t/ha, 80% of errors within [-0.76, +1.22] t/ha) | `screenshots/week4/` | **Verified** |
| 26 | `actual_vs_predicted_parity.png` | Holdout evaluation parity plot reference | `screenshots/week4/` | **Verified** |
| 27 | `pytest_test_verification.png` | Automated software test suite execution report: 11 passed out of 11 tests across features, preprocessing, and upload | `screenshots/week4/` | **Verified** |
| 28 | `agribusiness_decision_matrix.png` | Agribusiness Strategic Decision Matrix translating empirical ML evidence into concrete actions for FPOs, Processors, and Insurers | `screenshots/week4/` | **Verified** |
| 29 | `end_to_end_evaluation_scorecard.png` | Executive evaluation scorecard summarizing data retention, model accuracy, residual bias, and deployment readiness | `screenshots/week4/` | **Verified** |

---

### Application Preview Cards (`screenshots/application/`)
*Focus: Live web application module layouts and interactive user interfaces.*
| # | Filename | Description / What It Shows | Target Directory | Status |
|:---:|:---|:---|:---:|:---:|
| 30 | `app_hero_landing_overview.png` | Web application hero header, summary KPI cards (242,361 records, 124 crops, 33 states), and module navigation | `screenshots/application/` | **Verified** |
| 31 | `app_historical_explorer_module.png` | Historical Data Explorer layout: multi-filter dropdowns, multi-decade yield trajectory plots, and seasonal summaries | `screenshots/application/` | **Verified** |
| 32 | `app_yield_prediction_module.png` | Pre-Harvest ML Prediction Engine layout: user inputs (State, District, Crop, Season, Area) and real-time yield prediction outputs | `screenshots/application/` | **Verified** |
| 33 | `app_data_quality_audit_module.png` | Data Quality Audit Explorer layout: interactive missing-value breakdowns, Coconut unit partitioning, and ICAR outlier filters | `screenshots/application/` | **Verified** |
| 34 | `app_custom_csv_uploader_module.png` | Custom CSV Dataset Uploader layout: schema auto-detection, column mapping, and automated exploratory charting on uploaded data | `screenshots/application/` | **Verified** |
| 35 | `actual_vs_predicted_parity.png` | Embedded in-app parity plot visualization | `screenshots/application/` | **Verified** |
| 36 | `crop_yield_trends.png` | Embedded in-app historical trajectory visualization | `screenshots/application/` | **Verified** |
| 37 | `model_benchmark_comparison.png` | Embedded in-app model benchmark visualization | `screenshots/application/` | **Verified** |
| 38 | `top-12-crops-by-historical-production.png` | Embedded in-app commodity ranking visualization | `screenshots/application/` | **Verified** |

---

## 3. Verification & Compliance Sign-Off

- **Total Visual Artifacts**: 38 files verified on disk.
- **Data Integrity**: All figures generated directly from the certified dataset (`crop_production_cleaned.csv`) and validated machine learning models.
- **Repository Integration**: All screenshots are committed and tracked in the GitHub repository at `https://github.com/sangeetha302005/yuvaintern.agriyield-ai`.
