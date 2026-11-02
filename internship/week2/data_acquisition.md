# Week 2: Data Acquisition & Sourcing Provenance

## 1. Official Government Sourcing & Provenance

To ensure uncompromised credibility, reproducibility, and official backing for **AgriYield AI**, agricultural data was sourced from the Government of India Open Government Data (OGD) platform:

- **Official Dataset Title**: District-wise, Season-wise Crop Production Statistics from 1997
- **Publishing Authority**: Directorate of Economics and Statistics (DES), Department of Agriculture and Farmers Welfare, Ministry of Agriculture and Farmers Welfare, Government of India
- **Open Government Portal URL**: [data.gov.in (Resource ID 87630)](https://data.gov.in/resource/district-wise-season-wise-crop-production-statistics-1997)
- **Catalogue URL**: [delhi.data.gov.in Catalogue](https://delhi.data.gov.in/catalog/district-wise-season-wise-crop-production-statistics-0)
- **Direct CSV Download Endpoint**: `https://aps.dac.gov.in/APY/apy.csv`
- **Licence Terms**: Government Open Data License - India (GODL)
- **Acquisition Date**: October 2026
- **Storage Location**: Raw immutable copy stored in `application/data/raw/crop_production_raw.csv`

---

## 2. Selection Rationale & Agricultural Domain Suitability

The dataset was selected because it fulfills all essential criteria for longitudinal macro-level agricultural analysis:
1. **Administrative Resolution**: Observations are captured at the district level across 33 States and Union Territories, providing localized spatial granularity without sacrificing national coverage.
2. **Temporal Breadth**: Covers 18 agricultural calendar years (1997 to 2015), capturing multi-year monsoon anomalies, drought years (e.g. 2002, 2009, 2014, 2015), and technological yield growth.
3. **Comprehensive Crop Representation**: Includes 124 distinct crop varieties encompassing cereals, pulses, oilseeds, spices, and commercial plantation crops.
4. **Seasonal Specificity**: Distinguishes between the primary Indian agricultural seasons (`Kharif`, `Rabi`, `Whole Year`, `Summer`, `Winter`, `Autumn`), enabling seasonal productivity modeling.

---

## 3. Raw Data Inspection & Schema Profiling

Upon retrieval, the raw CSV file (`crop_production_raw.csv`) was inspected using Python and Pandas. The file profile is summarized below:

### Dimensions
- **Total Records (Rows)**: 246,091
- **Total Features (Columns)**: 7
- **File Size**: ~21.8 MB (uncompressed CSV)
- **Encoding**: UTF-8 / ASCII compatible, comma-separated (`delimiter=','`)

### Raw Schema Profile

| Column Index | Field Name | Raw Pandas Type | Missing Count | Missing % | Description |
|:---:|:---|:---:|:---:|:---:|:---|
| 0 | `State_Name` | `object` | 0 | 0.00% | Name of the Indian State / Union Territory |
| 1 | `District_Name` | `object` | 0 | 0.00% | Name of the administrative district |
| 2 | `Crop_Year` | `int64` | 0 | 0.00% | Agricultural calendar cropping year (1997–2015) |
| 3 | `Season` | `object` | 0 | 0.00% | Agricultural cropping season label |
| 4 | `Crop` | `object` | 0 | 0.00% | Common agricultural crop name |
| 5 | `Area` | `float64` | 0 | 0.00% | Cultivated sown land area (Hectares) |
| 6 | `Production` | `float64` | 3,730 | 1.516% | Harvested volume (Metric Tonnes / Thousand Nuts) |

### Key Observations from Raw Inspection
1. **Zero Nulls in Geographic & Crop Identifiers**: All rows contain valid state, district, year, season, and crop entries.
2. **Cultivated Area Completeness**: The `Area` attribute is 100% complete with zero missing values and zero negative or zero-area entries ($0.10 \le \text{Area} \le 8,580,100.00\text{ ha}$).
3. **Missing Target Values**: 3,730 rows lack harvested `Production` entries. These represent crop records where sowing acreage was reported by local agricultural departments, but harvesting data was not compiled or finalized.
