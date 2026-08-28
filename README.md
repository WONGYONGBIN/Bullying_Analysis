# Bullying Analysis — BTPR3203 Python for Data Science Project

**Group 4: Student Bullying Analysis**
BTPR3203 Python for Data Science — Project (30%), Semester B 2026

## Group Members

| Name | Student ID |
|---|---|
| Wong Yong Bin | B230051C |
| Wong Kai Xiang | B230265C |
| Teoh Yong Lin | B230254C |

## Overview

This project investigates school bullying through three research questions, each analysed with its own data pipeline (loading → cleaning → feature engineering → statistical testing → visualisation → predictive modelling) and consolidated into a single notebook, [`BTPR3203_Bullying_Analysis.ipynb`](./BTPR3203_Bullying_Analysis.ipynb).

## Research Questions

- **RQ1.** What are the major factors associated with bullying among students?
- **RQ2.** How does bullying severity differ across demographic groups, and how is it associated with students' behaviour and well-being?
- **RQ3.** What is the relationship between bullying and students' mental well-being?

## Datasets

| Dataset | Used for | Source |
|---|---|---|
| `mental_records.csv` | RQ1, RQ3 | [Student Stress Factors — Kaggle](https://www.kaggle.com/datasets/rxnach/student-stress-factors-a-comprehensive-analysis) (1,100 records, 21 variables, bullying severity 0–5) |
| `bullying_2018.csv` | RQ2 | [Bullying in Schools — Kaggle](https://www.kaggle.com/datasets/leomartinelli/bullying-in-schools) (Global School-based Student Health Survey, Argentina 2018; 56,981 records) |

Place both files in `data/` before running the notebook.

## Repository Structure

```
.
├── BTPR3203_Bullying_Analysis.ipynb   # Combined notebook — all 3 RQ pipelines
├── requirements.txt                   # Python dependencies
├── data/                              # Raw datasets (see above)
├── R1_output/                         # RQ1 outputs — factors associated with bullying
│   ├── correlation_heatmap.png            # Correlation matrix across all variables
│   ├── regression_coefficients.png        # Ordinal logistic regression coefficients
│   └── bullying_records_cleaned.csv       # Cleaned RQ1 dataset
├── R2_bullyinglevel_demographic/      # RQ2 outputs — severity, demographics, well-being
│   ├── fig1.1_bullying_severity_distribution.png
│   ├── fig1.2_type_prevalence.png
│   ├── fig2_pattern_by_sex.png
│   ├── fig3_pattern_by_age.png
│   ├── fig4_outcomes_by_severity.png
│   ├── fig5_correlation_heatmap.png
│   ├── bullying_severity_outcomes_summary.csv   # Summary table (severity × sex × age)
│   └── bullying_severity_test_statistics.json   # All test statistics (χ², H, F, p, V)
└── R3_mental_health_analysis/         # RQ3 outputs — bullying vs mental health
    ├── bullying_mental_health_analysis.png      # 4-panel regression + ML comparison
    ├── correlation_heatmap.png                  # Full-feature correlation matrix
    ├── processed_bullying_mental_health_summary.csv
    └── ML_Model_Results.csv                     # Classifier comparison (accuracy/precision/recall/F1)
```

## Setup

```bash
git clone https://github.com/WONGYONGBIN/Bullying_Analysis.git
cd Bullying_Analysis
pip install -r requirements.txt
```

Requirements: `pandas`, `numpy`, `matplotlib`, `seaborn`, `scipy`, `scikit-learn`, `statsmodels`, `jupyter`, `nbformat`.

## How to Run

```bash
jupyter notebook BTPR3203_Bullying_Analysis.ipynb
```

Run all cells top to bottom. Each RQ's pipeline is self-contained (its own load → clean → analyse → save-output flow), so cells can also be run RQ-by-RQ. Figures and summary files are written to the matching `R1_output/`, `R2_bullyinglevel_demographic/`, or `R3_mental_health_analysis/` folder.

## Method Summary

| | RQ1 | RQ2 | RQ3 |
|---|---|---|---|
| **Dataset** | `mental_records.csv` | `bullying_2018.csv` | `mental_records.csv` |
| **Key techniques** | Pearson correlation, ordinal logistic regression | Chi-square (Cramer's V), Kruskal-Wallis, one-way ANOVA, Spearman correlation | Correlation, Logistic/Random Forest/Gradient Boosting classifiers |
| **Predictive model** | Ordinal logistic regression (6-level target) | Ridge regression predicting `Loneliness_Score` (R² ≈ 0.21) | Multi-model classifier comparison predicting bullying level |

## Key Findings

- **RQ1:** Stress level is the clearest major factor associated with bullying severity — it has both the strongest correlation (r = 0.751) and the largest regression coefficient (β = 0.624) among all 20 candidate factors.
- **RQ2:** Bullying co-occurrence is common — 6.5% of students (about 1 in 6 bullied students) experience all three bullying forms (school, outside school, cyber) simultaneously. Severity — not sex or age — is the dominant correlate of poor mental well-being, school engagement, and social support outcomes.
- **RQ3:** Regression and multi-model classification were used to test whether bullying exposure predicts anxiety, depression, and self-esteem outcomes; see `R3_mental_health_analysis/ML_Model_Results.csv` for the model comparison and `processed_bullying_mental_health_summary.csv` for outcome means by bullying-exposure category.

## Course

BTPR3203 Python for Data Science, Semester B 2026.
