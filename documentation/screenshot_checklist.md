# AgriYield AI — Screenshot Evidence Checklist & Audit

This checklist catalogs all visual evidence artifacts, figures, and UI screenshots across the 4-week YuvaIntern internship lifecycle. In accordance with strict audit standards:
- **Completed**: The file physically exists in the designated directory and has been verified.
- **Pending manual capture**: The visual representation requires live browser capture of specific runtime UI states on the deployed Streamlit dashboard (`https://agriyield-ai-302005.streamlit.app/`).

---

## Master Screenshot Inventory

| # | Filename | Description / What It Must Show | Target Folder | Report Reference | Status |
|:---:|:---|:---|:---|:---|:---:|
| 1 | `yuva_internship_program_overview.png` | YuvaIntern Internship 4-week roadmap, milestone definitions, and role summary | `screenshots/week1/` | Week 1, Final Report | **Completed** (Exists) |
| 2 | `YuvaIntern_Offer_Letter.pdf` | Official YuvaIntern Internship Offer Letter for Junior Machine Learning Data Analyst | `screenshots/week1/` | Week 1, Final Report | **Completed** (Exists) |
| 3 | `data_quality_audit_breakdown.png` | Audit distribution of 246,091 raw records: 98.41% valid records, 1.52% missing production, 0.08% biological outliers | `screenshots/week2/` | Week 2, Final Report | **Completed** (Exists) |
| 4 | `top-12-crops-by-historical-production.png` | Historical production rankings for top 12 Indian agricultural commodities (Sugarcane, Rice, Wheat, etc.) | `screenshots/week2/` | Week 2, Final Report | **Completed** (Exists) |
| 5 | `crop_yield_trends.png` | Multi-crop yield trajectory (tonnes/ha) across 1997–2015 showing historical yield volatility and growth | `screenshots/week3/` | Week 3, Final Report | **Completed** (Exists) |
| 6 | `top_10_producing_states.png` | State-level total agricultural output volume across top 10 agricultural states (UP, AP, TN, etc.) | `screenshots/week3/` | Week 3, Final Report | **Completed** (Exists) |
| 7 | `seasonal_yield_distribution.png` | Yield productivity comparison across 6 cropping seasons (Kharif, Rabi, Summer, Winter, Autumn, Whole Year) | `screenshots/week3/` | Week 3, Final Report | **Completed** (Exists) |
| 8 | `actual_vs_predicted_parity.png` | Actual vs. Predicted Yield parity plot ($R^2 = 0.8710$) on 2012–2015 holdout test set | `screenshots/week3/` | Week 3, Week 4, Final Report | **Completed** (Exists) |
| 9 | `model_benchmark_comparison.png` | Multi-model regression benchmark comparing Baseline Mean, Ridge, Random Forest, and HistGradientBoosting | `screenshots/week4/` | Week 4, Final Report | **Completed** (Exists) |
| 10 | `residual_distribution.png` | Residual error distribution ($y - \hat{y}$) for champion HistGradientBoosting model ($\mu=0.2276$, $\sigma=4.5126$) | `screenshots/week4/` | Week 4, Final Report | **Completed** (Exists) |
| 11 | `pytest_test_verification.png` | Automated test suite execution summary showing 11/11 passing tests across features, preprocessing, and upload | `screenshots/week4/` | Week 4, Final Report | **Completed** (Exists) |
| 12 | `app_overview_landing_hero.png` | Web application hero header, project badges, metrics tiles, and system architecture summary | `screenshots/application/` | Week 4, Final Report | **Pending manual capture** |
| 13 | `app_historical_data_explorer.png` | Interactive multi-filter exploratory dashboard showing state, crop, and season dynamic filtering | `screenshots/application/` | Week 3, Week 4, Final Report | **Pending manual capture** |
| 14 | `app_ml_prediction_interface.png` | Interactive ML yield inference form with inputs (State, District, Crop, Season, Area) and predicted yield display | `screenshots/application/` | Week 4, Final Report | **Pending manual capture** |
| 15 | `app_data_quality_audit_view.png` | In-app data quality audit tab displaying missing value metrics and physiological outlier filters | `screenshots/application/` | Week 2, Week 4, Final Report | **Pending manual capture** |
| 16 | `app_custom_csv_uploader.png` | Custom CSV uploader tab with schema auto-detection and dynamic visualization generation | `screenshots/application/` | Week 4, Final Report | **Pending manual capture** |

---

## Capture Instructions for Pending UI Screenshots

To capture the 5 pending live web UI screenshots from the deployed dashboard:
1. Open the live application URL: `https://agriyield-ai-302005.streamlit.app/`
2. **Hero Landing Page (`app_overview_landing_hero.png`)**:
   - Capture full viewport displaying the AgriYield AI header, summary KPI cards (242,361 records, 124 crops, 33 states), and navigation sidebar.
3. **Historical Explorer Tab (`app_historical_data_explorer.png`)**:
   - Navigate to "Historical Data Explorer", select a State (e.g. Karnataka / Uttar Pradesh) and Crop (e.g. Rice), capture the dynamic trend charts.
4. **ML Yield Prediction Tab (`app_ml_prediction_interface.png`)**:
   - Navigate to "Yield Prediction", enter sample parameters (e.g. Karnataka, Mandya, Kharif, Rice, Area: 120 ha), click "Predict Yield", and capture the prediction card with confidence intervals.
5. **Data Quality Audit Tab (`app_data_quality_audit_view.png`)**:
   - Navigate to "Data Quality Audit", capture the audit statistics table and donut distribution.
6. **CSV Dataset Uploader Tab (`app_custom_csv_uploader.png`)**:
   - Navigate to "Upload & Analyze Dataset", upload a sample CSV (e.g. `application/tests/fixtures/sample_upload.csv` or `dataset/crop_production_cleaned.csv`), and capture the automated summary report.
7. Save the captured PNG images directly into `screenshots/application/` using the exact filenames listed above.
