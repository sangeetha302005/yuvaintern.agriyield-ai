# AgriYield AI — Test Plan & Automated Verification Results

## 1. Quality Assurance Strategy

The **AgriYield AI** testing framework is designed to verify mathematical integrity, prevent data leakage, validate schema conformance, and ensure web application resilience. Automated tests are implemented using `pytest` under `application/tests/`.

---

## 2. Test Suite Execution Summary

- **Execution Command**: `pytest application/tests`
- **Framework**: Pytest 7.4.0
- **Python Version**: Python 3.11.7 (64-bit)
- **Execution Date**: 02 November 2026
- **Total Test Cases**: 11
- **Passed**: 11 (100.0%)
- **Failed**: 0 (0.0%)
- **Execution Time**: 7.05 seconds

```text
============================= test session starts =============================
platform win32 -- Python 3.11.7, pytest-7.4.0, pluggy-1.0.0
rootdir: c:\Users\Sangeetha Suresh\Downloads\yuvaintern.agriyield-ai\application
plugins: anyio-4.15.1, langsmith-0.10.10, mock-3.16.0
collected 11 items

tests\test_features.py .....                                             [ 45%]
tests\test_preprocessing.py ....                                         [ 81%]
tests\test_upload_logic.py ..                                            [100%]

======================= 11 passed in 7.05s =======================
```

---

## 3. Individual Test Case Inventory & Coverage

### 3.1 Preprocessing Validation (`tests/test_preprocessing.py`)

| Test Function | Target Function / Module | Verification Objective | Result |
|:---|:---|:---|:---:|
| `test_raw_schema_validation` | `load_data.validate_raw_schema` | Verifies presence of all 7 expected raw columns in uploaded/downloaded files. | **PASSED** |
| `test_clean_pipeline_removes_null_production` | `preprocess.clean_data` | Verifies that records lacking production data are dropped to preserve ground truth. | **PASSED** |
| `test_unit_type_assignment` | `preprocess.assign_unit_types` | Confirms Coconut is assigned `Thousand Nuts` while field crops receive `Metric Tonnes`. | **PASSED** |
| `test_icar_outlier_flagging` | `preprocess.flag_icar_outliers` | Asserts that extreme yields exceeding ICAR physiological limits receive `is_outlier_yield = True`. | **PASSED** |

### 3.2 Feature Engineering Validation (`tests/test_features.py`)

| Test Function | Target Function / Module | Verification Objective | Result |
|:---|:---|:---|:---:|
| `test_log_area_calculation` | `build_features.add_log_area` | Verifies $\ln(Area + 1.0)$ formula and checks boundary condition at $Area = 0.1$. | **PASSED** |
| `test_year_index_derivation` | `build_features.add_year_index` | Verifies secular trend offset calculation ($\text{Year} - 1997$). | **PASSED** |
| `test_kharif_indicator` | `build_features.add_monsoon_indicator`| Verifies binary flag mapping (1 for Kharif, 0 for other seasons). | **PASSED** |
| `test_farm_scale_binning` | `build_features.bin_farm_scale` | Validates operational holding categorizations (Marginal, Small, Semi-Medium, Medium, Large). | **PASSED** |
| `test_prediction_output_structure` | `predict.predict_yield` | Verifies end-to-end model inference pipeline, dictionary keys, and float output typing. | **PASSED** |

### 3.3 CSV Upload & User Interface Logic (`tests/test_upload_logic.py`)

| Test Function | Target Function / Module | Verification Objective | Result |
|:---|:---|:---|:---:|
| `test_valid_csv_parsing` | `app.parse_uploaded_csv` | Tests parsing and automatic column mapping of valid custom user-uploaded CSVs. | **PASSED** |
| `test_invalid_csv_schema_handling` | `app.validate_upload_schema` | Asserts that appropriate warning notifications are returned when required columns are missing. | **PASSED** |

---

## 4. How to Rerun Automated Tests

To execute the test suite locally:
```powershell
cd "c:\Users\Sangeetha Suresh\Downloads\yuvaintern.agriyield-ai\application"
$env:PYTHONPATH = "."
pytest
```
