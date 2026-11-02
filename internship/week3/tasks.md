# Week 3: Data Analysis and Modeling — Task Summary

**Internship Role**: Junior Machine Learning Data Analyst — Agriculture & Agribusiness  
**Internship Organization**: YuvaIntern  
**Internship Period**: 01 October 2026 – 29 October 2026  
**Intern**: Sangeetha S (AMC Engineering College, Bengaluru)  
**Deliverable**: Week 3 Task Report (`reports/weekly/Week3.docx`)

---

## 1. Overview of Week 3 Objectives

Week 3 advances the AgriYield AI project from data preparation to exploratory data analysis (EDA), rigorous predictive problem formulation, leak-free model training, and multi-model benchmarking.

### Key Milestones Completed
1. **Exploratory Data Analysis (EDA)**: Analyzed yield trajectories across 18 years, established state production rankings, evaluated seasonal productivity patterns, and examined crop distributions across 124 commodities.
2. **Prediction Task Formulation**: Defined pre-harvest regression task predicting crop productivity ($t/\text{ha}$) using exclusively pre-harvest variables.
3. **Out-of-Time Chronological Validation**: Adopted temporal split:
   - **Training Set**: 1997–2011 (202,487 records)
   - **Test Set (Held-Out Future)**: 2012–2015 (37,726 records)
   - Total Modeling Corpus: 240,213 records (excluding coconut and flagged biological outliers)
4. **Model Benchmarking**: Trained and benchmarked four distinct regression models on identical out-of-time test folds:
   - Baseline Predictor (Unconditioned Training Mean)
   - Ridge Regression (Regularized Linear Model)
   - Random Forest Regressor (Ensemble Bagging)
   - Histogram-based Gradient Boosting Regressor (Champion Model)
5. **Evaluation Metrics**: Evaluated MAE, RMSE, $R^2$, and training execution times.
6. **Detailed Granular Subgroup Analysis**: Evaluated prediction error across major agricultural crops (Rice, Wheat, Maize, Sugarcane, Pulses) and cropping seasons (Kharif, Rabi, Whole Year, Summer, Winter, Autumn).
7. **Model Persistence**: Serialized the champion model pipeline (`models/best_yield_model.joblib`) and exported complete metadata (`models/model_metadata.json`).

---

## 2. Benchmark Summary Table

| Model Candidate | MAE ($t/\text{ha}$) | RMSE ($t/\text{ha}$) | $R^2$ Score | Training Time (s) | Model Rationale & Status |
|:---|:---:|:---:|:---:|:---:|:---|
| **Baseline (Mean)** | 5.6576 | 12.5961 | -0.0027 | 0.00s | Unconditioned historical training sample mean ($4.2809\text{ t/ha}$) |
| **Ridge Regression** | 1.3765 | 4.5257 | 0.8706 | 0.35s | L2 regularized linear model with standard scaling |
| **Random Forest Regressor** | 1.2434 | 4.5536 | 0.8690 | 5.88s | 60 estimators, max depth 14, min samples leaf 10 |
| **HistGradientBoosting** | **1.2562** | **4.5183** | **0.8710** | 5.96s | **Champion Model**: Non-linear tree boosting with categorical support |

---

## 3. Weekly Documentation Structure

Detailed documentation for Week 3 is organized across the following dedicated documents:
- [Exploratory Data Analysis](file:///c:/Users/Sangeetha%20Suresh/Downloads/yuvaintern.agriyield-ai/internship/week3/exploratory_data_analysis.md): Distribution profiling, crop ranking, state-level analysis, and seasonal comparisons.
- [Machine Learning Methodology](file:///c:/Users/Sangeetha%20Suresh/Downloads/yuvaintern.agriyield-ai/internship/week3/machine_learning.md): Task definition, chronological split strategy, algorithm selection, and training pipeline.
- [Model Evaluation](file:///c:/Users/Sangeetha%20Suresh/Downloads/yuvaintern.agriyield-ai/internship/week3/model_evaluation.md): Benchmark results, crop-wise performance, seasonal breakdowns, and residual diagnostics.
