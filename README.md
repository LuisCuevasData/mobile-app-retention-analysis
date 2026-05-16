# Mobile App Installer Retention Analysis

> What predicts whether a mobile app user sticks around for 30 days? This project explores installer retention data across 9 months and 6,400+ records, building and comparing linear regression, logistic regression, decision tree, and random forest models to find out.

![Python](https://img.shields.io/badge/Python-3.7.2-blue?logo=python&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-0.24.2-150458?logo=pandas&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-0.20-F7931E?logo=scikit-learn&logoColor=white)
![matplotlib](https://img.shields.io/badge/matplotlib-3.0.3-11557c)
![seaborn](https://img.shields.io/badge/seaborn-0.9.0-4c72b0)

---

## Overview

This project analyzes mobile application installer retention data collected across nine months (April–December 2019), covering 6,417 records and 14 features including daily install counts and retention milestones at 1, 7, 15, 30, and 60 days. The goal is to determine whether install volume alone can predict long-term user retention, and if so, how well.

The full pipeline runs from raw, inconsistently encoded CSV ingestion through data curation, feature engineering, visualization, and predictive modeling — culminating in a random forest classifier that achieves **87% accuracy** and a **0.92 ROC AUC**.

---

## Findings

- The most frequent retention value at every time window (1, 7, 15, 30 days) is **0** — most installs result in single-session activity
- The binary logistic regression model shows retention probability at 30 days rises from **17.22%** with one install to **90.77%** with four installs, revealing a nonlinear relationship
- The random forest model (**87.05% accuracy, 0.9232 ROC AUC**) outperforms the single decision tree on generalization to unseen data
- Install count alone is a weak predictor — the company would benefit from incorporating user demographics, acquisition channel, and behavioral engagement data

---

## Project Structure

```
mobile-app-retention-analysis/
├── mobile_app_retention_analysis.ipynb   # Main analysis notebook
├── app_retention_final.csv               # Merged dataset (6,417 rows × 14 columns)
└── README.md
```

---

## Notebook Sections

| Section | Description |
|---|---|
| 1. Imports | All dependencies loaded in one place |
| 2. Data Ingestion | Parse 9 raw monthly CSVs with mixed UTF-8/UTF-16 encoding |
| 3. Merge & Exploration | Concatenate into single dataset, shape/describe/count |
| 4. Data Curation | Standardize date formats, fix blank country values, enforce numeric types |
| 5. Feature Engineering | Create binary `Install_30` target column |
| 6. Visualization | Bar charts, line chart, seaborn regression plots, pairplot, scatter plots |
| 7. Linear Regression | Predict expected retained users by install count |
| 8. Logistic Regression | Multiclass and binary models with probability scatter plots |
| 9. Decision Tree & Random Forest | Classification models with ROC AUC evaluation |
| 10. Results Summary | Model comparison table and business implications |

---

## Model Results

| Model | Accuracy | ROC AUC | MAE |
|---|---|---|---|
| Decision Tree (train) | 86.05% | — | — |
| Random Forest (test) | 87.05% | 0.9232 | 0.13 |

---

## Dataset

The dataset contains aggregated mobile app installer retention records with the following schema:

| Column | Description |
|---|---|
| `Date` | Record date (standardized to YYYY-MM-DD) |
| `App` | Application package name |
| `Country` | Country of install |
| `Installers` | Total installs for that date/country |
| `Retained_1d` | Users retained at 1 day |
| `Retained_7d` | Users retained at 7 days |
| `Retained_15d` | Users retained at 15 days |
| `Retained_30d` | Users retained at 30 days |
| `Retained_60d` | Users retained at 60 days |
| `Install_30` | Binary: 1 if retained at 30 days, 0 otherwise (engineered) |

> **Note:** Retention rate columns are included in the raw files but not used as model features.

---

## Getting Started

```bash
# Clone the repository
git clone https://github.com/LuisCuevasData/mobile-app-retention-analysis.git
cd mobile-app-retention-analysis

# Install dependencies
pip install pandas==0.24.2 scikit-learn==0.20 matplotlib==3.0.3 seaborn==0.9.0

# Launch the notebook
jupyter notebook mobile_app_retention_analysis.ipynb
```

---

## Author

**Luis Cuevas**  
[LinkedIn](www.linkedin.com/in/luis-fabian-cuevas) · [Portfolio](https://luiscuevasportfolio.netlify.app)
