# UK Workplace Salary — Regression Portfolio Project

> **An end-to-end regression case study** on a synthetic UK workplace salary dataset, framed as a portfolio piece: business problem, EDA, four-model comparison, residual diagnostics, feature importance, business interpretation, and responsible-AI governance.

**Author:** Jumma Mohammad Teli — Data Analyst (Birmingham, UK)
📧 [jummamohammad477@gmail.com](mailto:jummamohammad477@gmail.com) · 🔗 [LinkedIn](https://linkedin.com/in/jumma-mohammad) · 💻 [GitHub](https://github.com/jumma786)

---

## Why this project

Salary modelling sits at the intersection of three things I work on every day: **predictive analytics, business interpretation in £, and responsible deployment under UK GDPR / Equality Act constraints**. This notebook walks through that full loop — not just "did the model beat baseline" but "is the gain worth the governance cost".

## Skills demonstrated

| Area | Specifics |
|---|---|
| Data prep | quality checks, dtype audit, leakage-safe pipelines (`ColumnTransformer` inside `Pipeline`) |
| EDA | target distribution (raw + log), feature-target correlations, salary by seniority and role family |
| Modelling | `DummyRegressor` baseline, `LinearRegression`, `Ridge`, `RandomForestRegressor`; 5-fold CV |
| Evaluation | MAE, RMSE, R²; CV MAE for stability; residual analysis |
| Interpretability | Permutation importance on the test set |
| Communication | Executive summary, business interpretation in £ and % terms, plain-English limitations |
| Governance | UK GDPR / Equality Act framing, ICO AI guidance citations, four-step deployment gate |

## Headline results

| Model | Test MAE (£) | Test RMSE (£) | Test R² | 5-fold CV MAE (£) |
|---|---:|---:|---:|---:|
| Baseline (mean) | 10,844 | 13,581 | 0.000 | 11,452 |
| **Linear regression** | **4,600** | **5,928** | **0.809** | **4,394** |
| Ridge (α=1.0) | 4,609 | 5,944 | 0.808 | 4,393 |
| Random Forest | 6,588 | 8,173 | 0.638 | 6,378 |

**The recommended model is linear regression.** It cuts the typical prediction error by **58%** versus baseline, explains **~81%** of the variance, and beats Random Forest on this dataset — a useful reminder that more complex ≠ better, especially on a small (720-row) dataset whose salary signal is largely linear in experience and seniority.

## Dataset

Synthetic UK workplace salary dataset, 720 rows × 15 columns. Target is `annual_salary_gbp`. No personal data; **not suitable for real compensation decisions**. See `data_dictionary.md` from the source pack for the column schema.

## Repository layout

```
session-06-regression/
├── data/
│   └── workplace_salary_regression_dataset.csv
├── notebooks/
│   └── Session_06_Portfolio_Notebook.ipynb     ← portfolio piece (executed)
├── outputs/
│   ├── model_comparison_results.csv
│   ├── top_residuals.csv
│   ├── eda_target_distribution.png
│   ├── eda_numeric_correlations.png
│   ├── eda_salary_by_category.png
│   ├── model_mae_comparison.png
│   ├── actual_vs_predicted.png
│   └── permutation_importance.png
├── reports/
│   └── business_interpretation.md
└── README.md
```

## How to reproduce

```bash
# Python 3.10+ recommended
pip install pandas numpy scikit-learn matplotlib jupyter
jupyter notebook notebooks/Session_06_Portfolio_Notebook.ipynb
# Run all cells. Random seed is fixed at 42.
```

## Responsible-AI note

Even though this dataset is synthetic, the notebook treats it as if it were real and documents the four controls required before any salary model could be deployed: a Data Protection Impact Assessment, a fairness audit on protected characteristics, human-in-the-loop review on consequential decisions, and a documented retraining and drift-monitoring schedule. See §11 of the notebook for the full caveat.

## What I'd do next

1. Replace synthetic data with audited HRIS data under a documented lawful basis.
2. Add a fairness audit across protected characteristics with disaggregated error metrics.
3. Try `RidgeCV`/`LassoCV` and a tuned gradient-boosted tree (`XGBoost` / `LightGBM`) on a larger dataset.
4. Add SHAP values for per-prediction explanations.
5. Surface the model in a Power BI report (my day-to-day stack) with monitoring on drift and error-rate parity.

---

*Built as part of Session 06 — Supervised Learning and Regression. Portfolio-grade extension of the original course exercise.*
