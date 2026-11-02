# Week 2: Data Preparation & Quality Auditing

## 1. Data Quality Assessment Methodology

Before executing transformations on the raw dataset, a formal data quality audit was conducted across four fundamental dimensions:
1. **Completeness**: Identification and quantification of missing values across all fields.
2. **Uniqueness**: Assessment of full-row duplicates and administrative composite key collisions.
3. **Validity & Integrity**: Evaluation of numeric ranges, zero-value semantics, and string casing consistency.
4. **Agronomic Plausibility**: Verification of biological maximum yields and unit consistency.

---

## 2. Missing Value Analysis & Ground-Truth Preservation

### Audit Finding
- The raw dataset contained 3,730 null values in the `Production` column (1.516% of total records).
- All other 6 columns exhibited 0 missing values.

### Domain Decision & Rationale
In agricultural machine learning, crop yield is a derived ratio:
$$\text{Yield} = \frac{\text{Production}}{\text{Area}}$$
Applying statistical imputation (e.g. mean, median, iterative MICE, or K-Nearest Neighbors) to `Production` would generate **synthetic ground-truth labels**. Models trained on artificially imputed targets learn artificial artifacts rather than genuine agronomic patterns.

**Action Taken**:
- Rows with missing `Production` were systematically excluded from the supervised training dataset.
- The 3,730 omitted rows were documented in `reports/data_quality_summary.md` and tracked in audit metrics.
- Retention rate: $\frac{246,091 - 3,730}{246,091} = 98.484\%$.

---

## 3. Duplicate Detection & Key Uniqueness

### Full-Row Duplicate Check
A scan of all 246,091 rows for identical duplicate records across all 7 columns yielded **0 exact duplicate rows**.

### Administrative Key Conflict Check
An agricultural harvest report is theoretically unique at the compound key:
$$\text{Composite Key} = [\text{State\_Name}, \text{District\_Name}, \text{Crop\_Year}, \text{Season}, \text{Crop}]$$
Evaluating grouping on this composite key confirmed **0 conflicting key collisions**. Each observation corresponds to a distinct administrative harvest event.

---

## 4. Categorical Normalization & Text Cleaning

### Whitespace & Inconsistent Casing
Raw categorical fields contained inconsistent trailing whitespaces (e.g. `'Kharif   '`, `'Whole Year '`).
- Applied string trimming (`.str.strip()`) across `State_Name`, `District_Name`, `Season`, and `Crop`.
- Standardized `State_Name` to Title Case (e.g. `'Andaman and Nicobar Islands'` $\rightarrow$ `'Andaman And Nicobar Islands'`).
- Standardized `District_Name` to UPPERCASE.
- Mapped season entries to the 6 canonical Indian agricultural seasons: `Kharif`, `Rabi`, `Whole Year`, `Summer`, `Winter`, `Autumn`.

---

## 5. Resolving Unit Heterogeneity: The Coconut Discrepancy

### Observation
Preliminary statistical profiling revealed extreme production values exceeding $1.25 \times 10^9$ and derived yields exceeding $38,000\text{ units/ha}$.

### Agronomic Investigation
In the Government of India agricultural reporting framework:
- Food grains (Rice, Wheat, Maize, Pulses), oilseeds, and cash crops (Sugarcane, Cotton) are documented in **Metric Tonnes**.
- **Coconut** production is officially recorded in **Thousand Nuts** or **Nuts**.

Combining nuts with metric tonnes in a single loss function introduces extreme gradient distortion, causing regression models to prioritize coconut volume over grain food security crops.

### Solution Applied
- Engineered an explicit categorical indicator: `Unit_Type`.
- Assigned `Unit_Type = "Thousand Nuts"` to all Coconut records (1,958 rows).
- Assigned `Unit_Type = "Metric Tonnes"` to all remaining 123 crops (240,403 rows).
- Enabled filtering so models evaluating $t/\text{ha}$ operate strictly on metric tonne crops.

---

## 6. Biological Yield Bounding (ICAR Ceilings)

### Anomaly Identification
Transcription and typographical data-entry errors exist in historical government archives (e.g. Sugarcane yield recorded at 88,000 t/ha, Wheat yield recorded at 200 t/ha).

### Agronomic Benchmarking
Using physiological yield ceilings published by the **Indian Council of Agricultural Research (ICAR)** and the **Food and Agriculture Organization (FAO)**, maximum plausible yield bounds were mapped per crop category:

| Crop Category | Representative Crops | ICAR Maximum Plausible Yield ($t/\text{ha}$) |
|:---|:---|:---:|
| **Sugarcane** | Sugarcane | $250.0 \text{ t/ha}$ |
| **Cereals** | Rice, Wheat, Maize, Barley, Jowar, Bajra | $12.0 \text{ to } 15.0 \text{ t/ha}$ |
| **Pulses** | Gram, Arhar/Tur, Moong, Urad, Masoor | $6.0 \text{ t/ha}$ |
| **Oilseeds** | Groundnut, Mustard, Sunflower, Soybean | $8.0 \text{ t/ha}$ |
| **Vegetables & Tubers** | Potato, Onion, Sweet Potato, Tapioca | $60.0 \text{ to } 80.0 \text{ t/ha}$ |
| **Spices & Fibres** | Black Pepper, Cardamom, Cotton, Jute | $5.0 \text{ to } 10.0 \text{ t/ha}$ |

### Action Taken
- Assigned each crop its domain threshold in `Max_Plausible_Yield`.
- Evaluated `is_outlier_yield = Yield > Max_Plausible_Yield`.
- Flagged **190 records** (0.078% of the dataset) as physiological anomalies.
- These records remain visible in exploratory audits but are excluded from model training folds to prevent loss divergence.

---

## 7. Cleaned Dataset Acceptance

The cleaned dataset `dataset/crop_production_cleaned.csv` was verified:
- **Rows**: 242,361
- **Columns**: 11
- **Null Count**: 0 across all 11 columns
- **Integrity**: Division-by-zero free, unit-audited, outlier-flagged, and certified for leak-free model training.
