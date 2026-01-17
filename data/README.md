# Data Source

## Datasets Used

This analysis utilizes three complementary datasets provided by UIDAI:

### 1. **Aadhaar Enrolment Dataset**
- **Records:** 500,000+ rows
- **Variables:** Date, State, District, PIN code, Age groups (0-5, 5-17, 18+)
- **Purpose:** Spatial and temporal enrolment pattern analysis

### 2. **Aadhaar Demographic Update Dataset**
- **Records:** 500,000+ rows
- **Variables:** Date, State, District, PIN code, Update age groups
- **Updates Tracked:** Name, Address, Date of Birth, Gender, Mobile number
- **Purpose:** Citizen engagement and update behavior analysis

### 3. **Aadhaar Biometric Update Dataset**
- **Records:** 500,000+ rows
- **Variables:** Date, State, District, PIN code, Biometric update age groups
- **Modalities:** Fingerprint, Iris, Face recognition
- **Purpose:** Biometric update pattern and lifecycle analysis

---

## Dataset Information

**Source:** UIDAI via [event.data.gov.in](https://event.data.gov.in)  
**Time Period:** March 2025 - October 2025 (7 months)  
**Geographic Coverage:** 35+ states, 1,050+ districts  
**License:** OGD Platform Terms of Use (Creative Commons By 4.0)  
**Data Type:** Aggregated and anonymized (state/district level)

---

## Download Instructions

### **Step 1: Access Data Portal**
Visit: https://event.data.gov.in/challenge/uidai-data-hackathon-2026/

### **Step 2: Download ZIP Files**
Download all 3 compressed datasets:
- `api_data_aadhar_enrolment.zip` (6.5 MB)
- `api_data_aadhar_demographic.zip` (13.2 MB)
- `api_data_aadhar_biometric.zip` (12.6 MB)

### **Step 3: Choose Execution Environment**

**For Local Execution:**
```bash
# Extract ZIP files to project data folder
mkdir -p data/raw
unzip api_data_aadhar_enrolment.zip -d data/raw/
unzip api_data_aadhar_demographic.zip -d data/raw/
unzip api_data_aadhar_biometric.zip -d data/raw/
```

**For Google Colab (Recommended):**
- Upload ZIP files (as-is, do NOT extract) to Google Drive
- Place in: `/content/drive/MyDrive/`
- Notebooks will load directly from ZIP files

---

## Data File Structure

Each ZIP file contains a CSV with the following structure:

### Enrolment Dataset Columns:
| Column | Type | Description |
|--------|------|-------------|
| date | object | Enrollment date (DD-MM-YYYY) |
| state | object | State name |
| district | object | District name |
| pincode | int64 | 6-digit PIN code |
| age_0_5 | int64 | Count of enrolments age 0-5 years |
| age_5_17 | int64 | Count of enrolments age 5-17 years |
| age_18_greater | int64 | Count of enrolments age 18+ years |

### Demographic Update Dataset Columns:
| Column | Type | Description |
|--------|------|-------------|
| date | object | Update date (DD-MM-YYYY) |
| state | object | State name |
| district | object | District name |
| pincode | int64 | 6-digit PIN code |
| demo_age_5_17 | int64 | Demographic updates age 5-17 |
| demo_age_17_ | int64 | Demographic updates age 17+ |

### Biometric Update Dataset Columns:
| Column | Type | Description |
|--------|------|-------------|
| date | object | Update date (DD-MM-YYYY) |
| state | object | State name |
| district | object | District name |
| pincode | int64 | 6-digit PIN code |
| bio_age_5_17 | int64 | Biometric updates age 5-17 |
| bio_age_17_ | int64 | Biometric updates age 17+ |

---

## Important Notes

### Git Repository
Raw data files (.csv, .zip) are NOT committed to Git due to:
- Large file sizes (32+ MB total)
- GitHub file size limitations
- Data privacy and licensing considerations

### Data Loading Method
The analysis notebooks load data directly from ZIP files without extraction:

```python
import zipfile
import pandas as pd

with zipfile.ZipFile('api_data_aadhar_enrolment.zip') as z:
    csv_name = [f for f in z.namelist() if f.endswith('.csv')]
    with z.open(csv_name[0]) as f:
        enrol_df = pd.read_csv(f)
```

This approach:
- Saves disk space
- Maintains data integrity
- Simplifies Google Colab workflow

---

## Data Quality

**Completeness:**
- Enrolment Dataset: 99.8% complete
- Demographic Update Dataset: 98.5% complete
- Biometric Update Dataset: 97.2% complete

**Known Issues:**
- Missing data: August 2025 (1-month gap identified)
- State naming inconsistencies: Multiple spellings (e.g., "WEST BENGAL", "West Bengal")
- Handled in preprocessing pipeline

---

## Data Privacy & Ethics

All datasets are:
- **Anonymized** - No personally identifiable information (PII)
- **Aggregated** - State/district level only, no individual records
- **Public** - Released by UIDAI for research and analysis
- **Licensed** - Creative Commons By 4.0 (attribution required)

---

## Data Access Support

**For dataset-related queries:**
- UIDAI Data Portal: [event.data.gov.in](https://event.data.gov.in)
- OGD Platform: [data.gov.in](https://data.gov.in)

**For analysis-related questions:**
- Email: bk9761790@gmail.com
- GitHub: [@bharathbattu](https://github.com/bharathbattu)

---

**Last Updated:** January 20, 2026
