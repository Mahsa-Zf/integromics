# Radiomics and Clinical Feature Integration for Survival Prediction in CAR T-Cell Therapy (SVM / Random Forest)

## Overview
This repository implements an end-to-end machine-learning workflow to evaluate whether **PET-based radiomics features**, and in particular **delta radiomics (Time B − Time A)**, provide additional predictive value beyond **clinical variables** for short-term survival prediction in patients with diffuse large B-cell lymphoma (DLBCL) treated with CAR T-cell therapy.

Due to the **very small cohort size (n = 30)** and a **small held-out test set (n = 6)**, all analyses are **exploratory** and intended for **hypothesis generation**, not clinical decision-making.

---

## Data and study design
- Retrospective cohort: **30 DLBCL patients**
- Train / Test split: **24 / 6** (stratified)
- Radiomics timepoints:
  - **Time A:** baseline PET/CT
  - **Time B:** pre-lymphodepletion PET/CT
- Delta radiomics computed as: **B − A**

---

## Feature configurations
Each model is trained and evaluated independently using the following feature sets:

- **clinical** — clinical variables only  
- **clin + A** — clinical + baseline radiomics  
- **clin + B** — clinical + pre-lymphodepletion radiomics  
- **clin + delta** — clinical + delta radiomics (B − A)

This design allows direct comparison of single-timepoint and longitudinal radiomics information.

---

## Models and evaluation

### Models
- **Support Vector Machine (RBF kernel)**
- **Random Forest**

Both models are implemented using **scikit-learn pipelines** with:
- Median imputation
- Feature scaling
- Class-weight balancing
- Hyperparameter tuning via **GridSearchCV**

### Evaluation metrics
- Accuracy  
- Balanced Accuracy  
- F1-score  
- ROC-AUC (reported when defined)

> **Important note:** With only 6 test samples, performance metrics—especially ROC-AUC—are highly unstable and should be interpreted with extreme caution.

---

## Repository structure
- `config.py`  
  Loads and validates paths from `config.yaml`.

- `io.py`  
  Reads per-patient radiomics files, extracts the `suv2.5` segmentation row, and constructs radiomics feature tables for:
  - Time A
  - Time B
  - Delta (B − A)

- `models.py`  
  Defines SVM and Random Forest pipelines and a reusable training/evaluation routine that returns consistent result dictionaries across feature sets.

- `plots.py`  
  Visualization utilities for summarizing results, including:
  - Metric heatmaps across models and feature sets
  - Confusion matrix strips for selected scenarios

- `*.ipynb`  
  Main analysis notebook(s) containing the full workflow: preprocessing, modeling, evaluation, visualization, and interpretation.

---

## Setup

### Requirements
- Python 3.x  
- `numpy`, `pandas`, `pyyaml`, `matplotlib`  
- `scikit-learn`

### Installation (example)
```bash
pip install numpy pandas pyyaml matplotlib scikit-learn
