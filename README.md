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
- R² ≈ 0.90
- Cross-validated RMSE ≈ 1.4
- No significant influential observations after validation

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
