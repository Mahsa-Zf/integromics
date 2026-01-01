# Folder Structure

**src.py**: Core Python module containing:

- `calculate_delta_radiomics`: Functions for data extraction from Excel files, filtering by SUV threshold (2.5), and calculating temporal changes ($\Delta = \text{pre-LD} - \text{baseline}$).
- `cox_univariate_analysis`: A standardized pipeline for univariate Cox Proportional Hazards regression, including feature scaling and proportional hazards assumption checking.

**cox_kaplan_analysis.ipynb**: The primary research notebook documenting the end-to-end workflow, from data preprocessing (missing value imputation, variance filtering) to Kaplan-Meier visualization and statistical testing.
