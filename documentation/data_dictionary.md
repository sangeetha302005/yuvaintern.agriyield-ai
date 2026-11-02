# AgriYield AI — Complete Agricultural Data Dictionary

## 1. Schema Overview

The primary analytical dataset `crop_production_cleaned.csv` consists of **242,361 rows** and **11 columns**. Each observation represents an administrative agricultural yield report across India between 1997 and 2015.

---

## 2. Field Specifications

### 1. `State_Name`
- **Data Type**: `object` (string)
- **Format**: Title Case (e.g. `'Karnataka'`, `'Uttar Pradesh'`, `'Andaman And Nicobar Islands'`)
- **Cardinality**: 33 unique States and Union Territories
- **Missing Count**: 0 (0.00%)
- **Analytical Role**: Spatial stratification, regional grouping, and state-level historical yield baselining.

### 2. `District_Name`
- **Data Type**: `object` (string)
- **Format**: UPPERCASE (e.g. `'MANDYA'`, `'VARANASI'`, `'LUDHIANA'`)
- **Cardinality**: 646 administrative districts
- **Missing Count**: 0 (0.00%)
- **Analytical Role**: Primary local administrative resolution for agricultural reporting.

### 3. `Crop_Year`
- **Data Type**: `int64` (integer)
- **Range**: 1997 to 2015 (18 continuous agricultural years)
- **Missing Count**: 0 (0.00%)
- **Analytical Role**: Temporal indexing, multi-decade time-series analysis, and chronological train/test split cutoff ($2011$).

### 4. `Season`
- **Data Type**: `object` (string)
- **Values**: `Kharif` (38.8%), `Rabi` (27.5%), `Whole Year` (18.2%), `Summer` (6.1%), `Winter` (5.3%), `Autumn` (4.1%)
- **Missing Count**: 0 (0.00%)
- **Analytical Role**: Seasonal regime categorization and monsoon dependency indicator.

### 5. `Crop`
- **Data Type**: `object` (string)
- **Cardinality**: 124 distinct botanical varieties
- **Missing Count**: 0 (0.00%)
- **Analytical Role**: Crop commodity identification for botanical categorization and baseline yield assignment.

### 6. `Area`
- **Data Type**: `float64` (continuous numeric)
- **Measurement Unit**: Hectares ($\text{ha}$)
- **Range**: $0.10 \le \text{Area} \le 8,580,100.00\text{ ha}$
- **Distribution**: Mean: $12,167.4\text{ ha}$, Median: $603.0\text{ ha}$, Std Dev: $50,857.4\text{ ha}$
- **Missing Count**: 0 (0.00%)
- **Analytical Role**: Pre-harvest acreage predictor; input for logarithmic acreage transformation (`Log_Area`).

### 7. `Production`
- **Data Type**: `float64` (continuous numeric)
- **Measurement Unit**: Metric Tonnes ($\text{t}$) for field crops; Thousand Nuts for coconut.
- **Range**: $0.00 \le \text{Production} \le 1,250,800,000.00$
- **Missing Count**: 0 in cleaned dataset (3,730 null records excluded during preprocessing).
- **Analytical Role**: Harvest outcome numerator for deriving target yield; strictly excluded from pre-harvest input predictors.

### 8. `Unit_Type`
- **Data Type**: `object` (string flag)
- **Values**: `"Metric Tonnes"` (240,403 rows, 99.19%), `"Thousand Nuts"` (1,958 rows, 0.81%)
- **Missing Count**: 0 (0.00%)
- **Analytical Role**: Prevents unit contamination between mass tonnage crops and nut plantation counts.

### 9. `Yield`
- **Data Type**: `float64` (continuous numeric)
- **Measurement Unit**: Metric Tonnes per Hectare ($t/\text{ha}$) or Thousand Nuts per Hectare.
- **Formula**: $\text{Yield} = \frac{\text{Production}}{\text{Area}}$ (where $\text{Area} > 0$)
- **Distribution (Tonnes/ha crops)**: Mean: $4.28\text{ t/ha}$, Median: $1.00\text{ t/ha}$
- **Missing Count**: 0 (0.00%)
- **Analytical Role**: Supervised target variable for machine learning regressors.

### 10. `Max_Plausible_Yield`
- **Data Type**: `float64` (discrete numeric threshold)
- **Measurement Unit**: Tonnes per Hectare ($t/\text{ha}$)
- **Range**: $5.0 \text{ to } 250.0\text{ t/ha}$ based on ICAR physiological ceilings per crop category.
- **Missing Count**: 0 (0.00%)
- **Analytical Role**: Agronomic domain sanity bound for outlier screening.

### 11. `is_outlier_yield`
- **Data Type**: `bool` (boolean flag)
- **Values**: `False` (242,171 rows, 99.92%), `True` (190 rows, 0.08%)
- **Missing Count**: 0 (0.00%)
- **Analytical Role**: Filters unphysical transcription anomalies from model training folds.
