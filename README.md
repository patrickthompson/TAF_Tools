# TAF_Tools

A repository of SAS code for use on T-MSIS Analytic Files (TAF) within the CMS Virtual Research Data Center (VRDC). Includes tools for appending and filtering datasets, view creation, and the application of public standardized research instruments such as the Charlson Comorbidity Index.

Maintained by the **Institute for Health Policy, Michigan State University**.

---

## Contents

| File | Description |
|------|-------------|
| `THOMPSON_CCI_TAF_Implement_2026.sas` | Applies the Charlson Comorbidity Index (CCI) to TAF Other Services (OTH) files. Extracts ICD-9 and ICD-10 diagnosis codes, stacks them into long format, and scores 16 chronic conditions. |

---

## Requirements

- **SAS** (version 9.4 or later recommended)
- Access to the **CMS Virtual Research Data Center (VRDC)**
- Access to **TAF OTH (Other Services)** files in your assigned VRDC library

---

## Script Details

### `THOMPSON_CCI_TAF_Implement_2026.sas`

Implements the NCI/Charlson Comorbidity Index adapted for Medicaid TAF data.

**What it does:**
1. Loops through all `TAFOTH` tables in a specified VRDC library
2. Extracts `DGNS_CD_1` and `DGNS_CD_2` diagnosis codes into a unified long-format table
3. Applies comorbidity logic for 16 chronic conditions using both ICD-9 and ICD-10 codes
4. Outputs one record per beneficiary with binary condition flags and a Charlson score

**Conditions scored:**

| Condition | Charlson Weight |
|-----------|----------------|
| Acute MI | 1 |
| History of MI | 1 |
| Congestive Heart Failure (CHF) | 1 |
| Peripheral Vascular Disease (PVD) | 1 |
| Cerebrovascular Disease (CVD) | 1 |
| COPD | 1 |
| Dementia | 1 |
| Diabetes (uncomplicated) | 1 |
| Ulcers | 1 |
| Rheumatic Disease | 1 |
| Paralysis | 2 |
| Diabetes with complications | 2 |
| Renal Disease | 2 |
| Mild Liver Disease | 1 |
| Severe Liver Disease | 3 |
| AIDS/HIV | 6 |

**User-defined parameters (edit at top of script):**

| Parameter | Default | Description |
|-----------|---------|-------------|
| `STUDYSTART` | `01JAN2022` | Start of study window |
| `STUDYEND` | `31DEC2022` | End of study window |
| `OTHERHEADERLIB` | `IN******` | VRDC library containing TAF OTH tables |
| `SAVELIBNAME` | `SAVELIB` | Output library |
| `SAVETABLENAME` | `COMORB` | Output table name |
| `clean_temptables` | `0` | Set to `1` to delete temporary WORK tables after run |
| `RULEOUT` | `N` | Set to `Y` to apply 30-day ruleout algorithm |

**Output variables:**

- `DIST_ID` — Beneficiary identifier (concatenation of MSIS_ID and BENE_ID)
- `acute_mi`, `history_mi`, `chf`, `pvd`, `cvd`, `copd`, `dementia`, `paralysis`, `diabetes`, `diabetes_comp`, `renal_disease`, `mild_liver_disease`, `liver_disease`, `ulcers`, `rheum_disease`, `aids` — Binary condition flags (0/1)
- `Charlson` — Charlson Comorbidity Index score
- `NCI_index` — NCI comorbidity index score

---

## Usage

1. Open the script in SAS within your VRDC session
2. Update the user-defined parameters in **Section 1** to match your study window and library names
3. Submit the program — output will be saved to `&SAVELIBNAME..&SAVETABLENAME`

---

## Citation

If you use this code in your research, please cite:

> Thompson, P.A. (2026). *TAF_Tools: SAS Code for T-MSIS Analytic Files*. Institute for Health Policy, Michigan State University. https://github.com/patrickthompson/TAF_Tools

The CCI coding logic is adapted from the NCI Comorbidity Index macro. Please also cite the original instrument as appropriate for your work.

---

## Contact

**Patrick Aaron Thompson, MSc**
Institute for Health Policy, Michigan State University
thomp705 at msu dot edu

---

## License

See [LICENSE](LICENSE) for terms of use.
