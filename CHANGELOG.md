# Changelog

All notable changes to TAF_Tools will be documented here.

---

## [1.0.0] - 2026-02-23

### Added
- `THOMPSON_CCI_TAF_Implement_2026.sas`: Initial release of the Charlson Comorbidity Index (CCI) implementation for TAF OTH files.
  - Supports ICD-9 and ICD-10 diagnosis codes
  - Scores 16 chronic conditions with Charlson and NCI index weights
  - Includes optional 30-day ruleout algorithm
  - Designed for use in the CMS VRDC environment
