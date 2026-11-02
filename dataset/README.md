# AgriYield AI — Processed Agricultural Dataset

## 1. Overview & Dataset Identity

| Metadata Attribute | Specification |
|:---|:---|
| **Dataset File Name** | `crop_production_cleaned.csv` |
| **Storage Location** | `dataset/crop_production_cleaned.csv` |
| **Dataset Class** | Processed & Cleaned Agricultural Records |
| **Original Dataset Title** | District-wise, Season-wise Crop Production Statistics from 1997 |
| **Publisher** | Directorate of Economics and Statistics (DES), Department of Agriculture and Farmers Welfare, Ministry of Agriculture and Farmers Welfare, Government of India |
| **Official Source Portal** | [Open Government Data (OGD) Platform India (data.gov.in)](https://data.gov.in/resource/district-wise-season-wise-crop-production-statistics-1997) |
| **Catalogue Entry** | [delhi.data.gov.in Catalogue](https://delhi.data.gov.in/catalog/district-wise-season-wise-crop-production-statistics-0) |
| **Direct Official Endpoint** | `https://aps.dac.gov.in/APY/apy.csv` |
| **Licence** | Government Open Data License - India (GODL) |
| **Temporal Coverage** | 1997 to 2015 (18 agricultural years) |
| **Geographic Coverage** | 33 States and Union Territories, 646 Administrative Districts across India |
| **Commodity Coverage** | 124 distinct agricultural crops across cereals, pulses, oilseeds, spices, cash crops, and plantation crops |
| **Verified Record Count** | **242,361** rows |
| **Verified Feature Count** | **11** columns |

---

## 2. Dataset Description

The `crop_production_cleaned.csv` dataset is the certified, curated analytical core of the **AgriYield AI** project. Originating from the official administrative crop reporting system of the Ministry of Agriculture and Farmers Welfare, Government of India, it provides detailed historical records of agricultural acreage, harvesting volumes, and derived productivity metrics.

Each observation represents a unique agricultural crop yield report aggregated at the intersection of:
$$\text{Administrative State} \times \text{Administrative District} \times \text{Crop Variety} \times \text{Cropping Season} \times \text{Agricultural Year}$$

---

## 3. Distinction: Raw vs. Processed Data

To guarantee end-to-end scientific transparency and auditability, the differences between raw administrative data and this processed dataset are formally outlined below:

| Dimension | Raw Input Data (`crop_production_raw.csv`) | Processed Data (`crop_production_cleaned.csv`) |
|:---|:---|:---|
| **Total Rows** | 246,091 records | **242,361 records** (98.48% retention) |
| **Total Columns** | 7 raw columns | **11 engineered & audited columns** |
| **Missing Production** | 3,730 rows (1.516% missing values) | **0 missing values** (rows excluded to prevent synthetic label distortion) |
| **Missing Area** | 0 missing values | 0 missing values verified |
| **Zero Area (`Area <= 0`)** | 0 records | 0 records (confirmed free of division-by-zero errors) |
| **Zero Production (`Production == 0`)**| 3,523 records (1.432%) | **3,523 records preserved** (verified genuine crop failures) |
| **String Formatting** | Trailing whitespace (e.g. `'Kharif   '`), irregular letter casing | Stripped, Title Case for States, UPPERCASE for Districts, canonical 6 Seasons |
| **Unit Discrepancies** | Mixed metrics without indicator: Coconut documented in *Thousand Nuts*; food grains in *Metric Tonnes* | Explicit `Unit_Type` column segregating 240,403 Metric Tonne crops from 1,958 Coconut records |
| **Derived Target** | No explicit yield field present | Derived $\text{Yield} = \frac{\text{Production}}{\text{Area}}$ computed with unit-consistent safeguards |
| **Physiological Outliers** | Unfiltered transcription anomalies (e.g. Sugarcane @ 88,000 t/ha) | Bounded against ICAR biological ceilings (`Max_Plausible_Yield`), flagged via `is_outlier_yield` (190 flagged) |

---

## 4. Schema and Column Specifications

The table below provides the full technical profile for all 11 columns in `crop_production_cleaned.csv`:

| # | Column Name | Pandas Data Type | Measurement Unit | Value Range / Cardinality | Description & Analytical Role |
|:---:|:---|:---:|:---:|:---|:---|
| 1 | `State_Name` | `object` (string) | N/A | 33 Unique States & UTs | Administrative State or Union Territory name formatted in Title Case. Used for regional grouping and stratified spatial analysis. |
| 2 | `District_Name` | `object` (string) | N/A | 646 Unique Districts | Administrative District name formatted in UPPERCASE. Serves as primary local administrative resolution. |
| 3 | `Crop_Year` | `int64` | Agricultural Year | 1997 to 2015 | Cropping cycle calendar year. Serves as temporal key for time-series trends and out-of-time chronological train/test splitting. |
| 4 | `Season` | `object` (string) | N/A | 6 Standard Seasons | Cropping calendar season: `Kharif` (Monsoon), `Rabi` (Winter post-monsoon), `Whole Year`, `Summer`, `Winter`, `Autumn`. |
| 5 | `Crop` | `object` (string) | N/A | 124 Unique Crop Types | Specific botanical/commercial agricultural crop name (e.g. `Rice`, `Wheat`, `Sugarcane`, `Maize`, `Moong(Green Gram)`). |
| 6 | `Area` | `float64` | Hectares (ha) | $0.10 \text{ ha} \le \text{Area} \le 8,580,100.00 \text{ ha}$ | Total land area planted/sown for the designated crop in the specified district and season. Mean: 12,167.4 ha; Median: 603.0 ha. |
| 7 | `Production` | `float64` | Metric Tonnes (t) or Thousand Nuts | $0.00 \le \text{Production} \le 1,250,800,000.00$ | Total recorded harvest output. Strictly recorded in metric tonnes for field crops and thousand nuts for coconut. Mean: 582,503.4; Median: 729.0. |
| 8 | `Unit_Type` | `object` (string) | Categorical Flag | `"Metric Tonnes"` (240,403 rows), `"Thousand Nuts"` (1,958 rows) | Measurement unit classification engineered to prevent cross-unit loss degradation and ensure physical metric purity. |
| 9 | `Yield` | `float64` | Tonnes / Hectare ($t/\text{ha}$) or Nuts / ha | $0.00 \le \text{Yield} \le 88,000.00$ (Outliers flagged) | Derived crop productivity metric calculated strictly as $\frac{\text{Production}}{\text{Area}}$. Primary target variable for machine learning regressors. |
| 10 | `Max_Plausible_Yield` | `float64` | Tonnes / Hectare ($t/\text{ha}$) | $5.0 \text{ to } 250.0 \text{ t/ha}$ | Domain ceiling established by the Indian Council of Agricultural Research (ICAR) biological research benchmarks per crop group. |
| 11 | `is_outlier_yield` | `bool` | Boolean Flag | `False` (242,171 rows), `True` (190 rows) | Outlier detection indicator identifying values where $\text{Yield} > \text{Max\_Plausible\_Yield}$. Excluded from machine learning training folds. |

---

## 5. Preprocessing Methodology & Transformations Applied

The cleaning pipeline (`src/data/preprocess.py`) executes five sequential validation steps:

1. **Target Authenticity & Missing Label Removal**:
   - 3,730 records had null values in `Production`.
   - *Rationale*: Imputing missing values in the target numerator would fabricate ground-truth labels and compromise model generalization. Therefore, these rows were omitted.
2. **Text Normalization & Deduplication**:
   - Applied whitespace stripping (`.strip()`) to eliminate trailing spaces in categorical columns (`Kharif `, `Whole Year `).
   - Standardized casing across geographic entities (`Andaman and Nicobar Islands` $\rightarrow$ `Andaman And Nicobar Islands`).
   - Audited administrative key uniqueness across `[State_Name, District_Name, Crop_Year, Season, Crop]` — verified zero duplicate administrative collisions.
3. **Unit Type Partitioning (The Coconut Resolution)**:
   - Coconut harvest numbers in India are reported in thousands of nuts rather than mass tonnage.
   - Identified 1,958 coconut records with raw yield values exceeding 38,000 units/ha.
   - Flagged with `Unit_Type = "Thousand Nuts"` while assigning all remaining 123 crops to `Unit_Type = "Metric Tonnes"`.
4. **ICAR Agronomic Plausibility Bounding**:
   - Defined maximum theoretical crop productivity thresholds from Indian Council of Agricultural Research (ICAR) and Food and Agriculture Organization (FAO) crop manuals:
     - Sugarcane: $\le 250.0 \text{ t/ha}$
     - Rice: $\le 15.0 \text{ t/ha}$
     - Wheat: $\le 12.0 \text{ t/ha}$
     - Maize: $\le 15.0 \text{ t/ha}$
     - Pulses: $\le 6.0 \text{ t/ha}$
     - Oilseeds: $\le 8.0 \text{ t/ha}$
     - Vegetables / Tubers: $\le 60.0 \text{ to } 80.0 \text{ t/ha}$
   - Flagged 190 records (0.078%) with `is_outlier_yield = True`. These remain auditable in EDA but are filtered out during model training folds to prevent gradient explosion.
5. **Yield Ratio Calculation**:
   - Evaluated $\text{Yield} = \frac{\text{Production}}{\text{Area}}$ for all records where $\text{Area} > 0$.

---

## 6. Dataset Limitations

1. **Macro-Administrative Granularity**: Records reflect district-wide statistical aggregations. They do not capture parcel-level or farm-scale soil micro-heterogeneity.
2. **Exclusion of Micro-Meteorology**: The administrative dataset does not include contemporaneous daily meteorological records (cumulative rainfall, solar radiation, diurnal temperature ranges) or fertilizer application rates (NPK ratio).
3. **Historical Administrative Boundary Shifts**: Certain district boundaries were bifurcated or realigned by state governments during the 1997–2015 period, introducing minor longitudinal variances in district-level sample counts.
4. **Non-Tonnage Crops**: Coconut is measured in units of nuts and must be modeled separately from biomass-tonnage crops.

---

## 7. Attribution, Citation & Licence

- **License**: Government Open Data License - India (GODL)
- **Source**: Ministry of Agriculture and Farmers Welfare, Directorate of Economics & Statistics (DES), Government of India.
- **Citation**:
  > Directorate of Economics and Statistics, Department of Agriculture and Farmers Welfare, Ministry of Agriculture and Farmers Welfare, Government of India. *District-wise, Season-wise Crop Production Statistics from 1997*. Open Government Data Platform India (data.gov.in), Resource ID: 87630. Available at: `https://data.gov.in/resource/district-wise-season-wise-crop-production-statistics-1997`.
