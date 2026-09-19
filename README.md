# Biomedical Linear Modeling  
Regression, Collinearity & Missing Data Imputation (R)

---

## Overview

This repository contains two applied biomedical statistics projects focused on:

- Multivariate linear regression
- Collinearity diagnostics (VIF)
- Model selection (AIC / BIC)
- Polynomial terms
- Outlier & influence analysis
- Missing data mechanisms (MCAR, MAR, MNAR)
- Multiple imputation using `mice`
- Cross-validation and predictive performance assessment

---

# Project 1: Body Fat Index Modeling

Source: Body fat dataset (252 men, 19 anthropometric measurements)

Goal:
Predict percentage body fat (PerBFat1) using technical body measurements.

Key components:

- Stepwise selection (BIC criterion)
- Collinearity reduction via VIF
- Polynomial transformations
- Influence diagnostics
- Model validation
- Cross-validation (10-fold, repeated CV)
- Train/test split performance comparison

Key findings:

- Final reduced model retained:
  - Height
  - FatFreeW
  - Chest
  - Thigh
  - Wrist
- R² ≈ 0.87 (see the limitation below)
- No significant influential observations after validation

### Known limitation: target leakage via FatFreeW

The model above retains `FatFreeW` (fat-free mass). That is a mistake, and it is
documented here rather than quietly deleted.

`FatFreeW` is not an independent body measurement. It is computed from the outcome:

    FatFreeW = Weight x (1 - PerBFat1/100)

Given `Weight`, which is also in the dataset, the outcome is recoverable almost
exactly: `100 x (1 - FatFreeW/Weight)` correlates with `PerBFat1` at r = 0.996, with a
mean absolute difference under 0.1 percentage points. Those two variables alone give
R2 = 0.96, which is arithmetic rather than prediction.

`Density` and `PerBFat2` were excluded at the start of this analysis for the same
reason. `FatFreeW` belongs in that exclusion list and was missed, because the course
exercise this analysis follows uses it as a predictor.

Corrected results, with `FatFreeW` removed from the candidate set before selection
rather than dropped afterwards:

| Model | R2 | 10-fold CV RMSE |
|---|---|---|
| As reported above: poly(FatFreeW,2) + Height + Chest + Thigh + Wrist | 0.87 | 3.82 |
| Backward BIC without FatFreeW: Weight, Abdomen, Forearm, Wrist | 0.74 | 4.10 |
| Abdomen circumference alone | 0.66 | 4.58 |
| FatFreeW + Weight only, the leak in isolation | 0.96 | 1.68 |

Standard deviation of `PerBFat1` is 7.75.

The clean model is the one that answers the question the study actually asks: predict
body fat from simple technical measurements. `R/Target-leakage-check.qmd` reproduces
every figure in this table from the raw data.

---

# Project 2: Missing Data & Multiple Imputation

Goal:
Investigate inference under missing data mechanisms and apply multiple imputation.

Topics covered:

- MCAR, MAR, MNAR simulation
- Complete case analysis comparison
- Multiple imputation using `mice`
- Pooling estimates across imputations
- Bias comparison between approaches

Key results:

- MCAR: minimal bias
- MAR: requires imputation for unbiased estimates
- MNAR: imputation insufficient
- Pooled estimates closely matched full-data model

---

## Methods Used

- Linear regression (lm)
- VIF diagnostics
- Stepwise selection (AIC, BIC)
- Polynomial regression
- Cook's distance
- Studentized residuals
- Multiple imputation (mice)
- Cross-validation (caret)
- RMSE, MSE comparison

---

## Reproducing this analysis

Install the dependencies with `setup.R` (R)

---

## Skills Demonstrated

- Advanced regression modeling
- Missing data theory & implementation
- Statistical inference under uncertainty
- Model diagnostics & assumption testing
- Predictive vs explanatory modeling
- Reproducible statistical workflow

---

## Note

These projects focus on statistical methodology and interpretation in biomedical contexts.
