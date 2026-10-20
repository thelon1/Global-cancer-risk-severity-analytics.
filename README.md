# 🧬 Global Cancer Patients (2015–2024): EDA & Inferential Analysis

An end-to-end exploratory and inferential analysis of a global cancer patient dataset. The project examines how lifestyle, environmental and genetic risk factors relate to cancer severity, survival and treatment cost. It combines descriptive statistics, hypothesis testing and a machine-learning model.

---

## 📌 Table of Contents
- [Overview](#overview)
- [Dataset](#dataset)
- [Research Questions](#research-questions)
- [Methodology](#methodology)
- [Key Findings](#key-findings)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Limitations](#limitations)
- [Future Work](#future-work)
- [License](#license)

---

## Overview
This project analyses **50,000 patient records across 10 countries/regions (2015–2024)**. It has two parts:

1. **Exploratory Data Analysis (EDA):** distributions of age, gender, country, cancer type, stage, treatment cost and risk factors.
2. **Inferential & Predictive Analysis:** correlation analysis, regression, non-parametric hypothesis tests, an interaction-effect model, and Random Forest regression with hyperparameter tuning.

## Dataset
**File:** `global_cancer_patients_2015_2024.csv`, 50,000 rows × 15 columns, no duplicates.

| Column | Description |
|---|---|
| `Patient_ID` | Unique patient identifier |
| `Age` | Patient age (20–89) |
| `Gender` | Male / Female / Other |
| `Country_Region` | 10 countries/regions |
| `Year` | Diagnosis year (2015–2024) |
| `Genetic_Risk`, `Air_Pollution`, `Alcohol_Use`, `Smoking`, `Obesity_Level` | Risk-factor scores (0–10) |
| `Cancer_Type` | 8 cancer types (Lung, Breast, Colon, Liver, Leukemia, Skin, Cervical, Prostate) |
| `Cancer_Stage` | Stage 0 – Stage IV |
| `Treatment_Cost_USD` | Treatment cost ($5,000 – $100,000) |
| `Survival_Years` | Survival duration in years |
| `Target_Severity_Score` | Cancer severity score |

## Research Questions
1. How do risk factors relate to cancer severity?
2. What proportion of each cancer type is diagnosed early (Stage 0 / Stage I)?
3. Which features best predict severity and survival years?
4. How does treatment cost vary across countries, genders and age groups?
5. Is higher treatment cost associated with longer survival?
6. Do higher cancer stages lead to higher costs or shorter survival?
7. Does genetic risk amplify the effect of smoking on severity (interaction effect)?

## Methodology
- **Descriptive analysis:** KDE plots, histograms, bar charts, pie charts, summary statistics.
- **Correlation analysis:** Pearson and Spearman against severity and survival.
- **Linear regression** (`scipy.stats.linregress`) for each risk factor against severity.
- **Modelling:** Random Forest Regressor with an 80/20 train-test split and `GridSearchCV` (3-fold CV).
- **Hypothesis testing:**
  - Shapiro-Wilk normality test
  - Kruskal-Wallis test (cost and survival across stages)
  - Pearson / Spearman correlation tests (cost vs. survival)
  - OLS regression with an interaction term (`Genetic_Risk * Smoking`)
- **Demographic cost analysis:** grouped averages by country, gender and age group, shown as bar charts and a heatmap.

## Key Findings

| Area | Result |
|---|---|
| **Severity drivers** | Smoking (r ≈ 0.48) and Genetic Risk (r ≈ 0.48) correlate most strongly with severity. Air Pollution (≈ 0.37) and Alcohol Use (≈ 0.36) are moderate, and Obesity (≈ 0.25) is weaker. |
| **Severity model** | Random Forest reached **R² ≈ 0.77 on the test set** (train ≈ 0.97, so some overfitting). |
| **Survival prediction** | Features have almost no predictive power: test R² ≈ 0. Correlation with survival is ≈ 0 for all variables. |
| **Early-stage diagnosis** | Roughly **38–41%** of cases across all cancer types are diagnosed at Stage 0/I. |
| **Cost vs. survival** | No significant correlation (Pearson r ≈ −0.0004, p ≈ 0.92). |
| **Stage vs. cost / survival** | Kruskal-Wallis found no significant difference (p = 0.43 for cost, p = 0.60 for survival). |
| **Genetic Risk × Smoking** | The interaction is not significant (coef ≈ −0.0002, p = 0.628), so the two factors act independently. |

## Tech Stack
- **Language:** Python 3
- **Data:** `pandas`, `numpy`
- **Visualization:** `matplotlib`, `seaborn`
- **Statistics:** `scipy`, `statsmodels`
- **Machine learning:** `scikit-learn`
- **Environment:** Jupyter Notebook

## Project Structure
```
├── data/
│   └── global_cancer_patients_2015_2024.csv
├── notebooks/
│   └── Comprehensive_EDA_and_Inferential_Analysis.ipynb
├── requirements.txt
├── .gitignore
└── README.md
```

## Getting Started

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/global-cancer-patients-eda-inferential-analysis.git
cd global-cancer-patients-eda-inferential-analysis

# 2. (Optional) create a virtual environment
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

# 3. Install dependencies
pip install pandas numpy matplotlib seaborn scipy statsmodels scikit-learn jupyter

# 4. Launch the notebook
jupyter notebook notebooks/Comprehensive_EDA_and_Inferential_Analysis.ipynb
```
> Make sure the CSV path in the notebook's `pd.read_csv(...)` call matches the dataset's location.

## Limitations
- Risk-factor variables appear uniformly distributed and the survival/cost fields show no relationship with any feature, which suggests the dataset is **synthetic or simulated**. The findings should not be taken as real-world clinical evidence.
- The Random Forest severity model overfits (train R² ≈ 0.97 vs. test ≈ 0.77).
- Categorical variables were label-encoded, which may impose an artificial order on them.

## Future Work
- Try one-hot encoding and gradient boosting models (XGBoost / LightGBM).
- Add cross-validation and SHAP-based explainability.
- Build an interactive dashboard (Streamlit / Power BI).
- Validate findings on real-world cancer registry data.

## License
This project is licensed under the [MIT License](LICENSE).
