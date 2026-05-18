# Session 06 — Business Interpretation

**Author:** Jumma Mohammad Teli
**Task:** Compare a mean-predictor baseline against linear regression for predicting `annual_salary_gbp` on a synthetic UK workplace dataset.

## Metrics

| Model                    | MAE (£) | RMSE (£) | R²    |
|--------------------------|--------:|---------:|------:|
| Baseline: mean predictor |  10,844 |   13,581 |  0.00 |
| Linear regression        |   4,600 |    5,928 |  0.81 |

## Business interpretation (≈ 300 words)

The headline result is that the linear regression substantially beats the mean-predictor baseline on every metric. The baseline simply guesses the average training salary (around £60.6k) for everyone, which leaves an average absolute error of roughly **£10,800** per employee and an R² of effectively zero — by construction it explains none of the variation in pay. The linear regression cuts that absolute error to about **£4,600**, an improvement of around **£6,200 per prediction or 58%**, and lifts R² to **0.81**, meaning the model captures roughly four-fifths of the variation in salaries across the test set.

In practical terms, a typical predicted salary is within roughly £4.6k of the actual figure — about 7–8% of the mean salary. That accuracy is good enough for **low-stakes planning use cases** such as workforce-cost forecasting, sense-checking job-advert salary bands, or producing rough budget envelopes for new hires. RMSE (£5,928) is noticeably higher than MAE, which tells us the model occasionally makes larger misses; the top-residual table shows these are concentrated among senior, high-experience, or specialist roles where compensation is driven by negotiation, equity, or scarce skills that the dataset does not capture. The actual-vs-predicted chart confirms this: most points cluster tightly around the 45° line, with a fanning-out at the high-salary end where the model tends to under-predict.

The recommendation is therefore to use the model as **decision support, not decision authority**. It is fit for shortlisting, budgeting and outlier-flagging, but any individual pay decision should still go through a human reviewer who can weigh the residual-driving factors the model cannot see — internal equity, retention risk, market premium for niche skills, and negotiated benefits. If the business wants to narrow the error further, the obvious next steps are a richer feature set (location granularity, performance ratings, market benchmark data) and a non-linear model such as a gradient-boosted tree.

## Governance caveat — fairness, representativeness, and deployment risk

Salary is a high-stakes, legally sensitive outcome, and this model is trained on a small synthetic classroom dataset (720 rows) that was not audited for demographic representativeness. Even though protected characteristics such as gender, ethnicity and age are not in the feature set, several included features — `region`, `education_level`, `seniority_level` and `people_management` — can act as **proxies for protected attributes** and therefore reproduce or amplify historical pay inequities. Under the UK GDPR / Equality Act and the ICO's guidance on AI and data protection, this model must not be used to make or materially influence individual pay decisions without (a) a Data Protection Impact Assessment, (b) a documented fairness audit comparing error rates across demographic groups, (c) a meaningful human-in-the-loop review for every consequential decision, and (d) a clear retraining schedule once it is connected to real organisational data. Until those controls are in place, the appropriate use is **internal planning and benchmarking only**.
