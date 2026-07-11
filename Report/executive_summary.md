# Executive Summary

## Insurance Pricing Platform

## Business Objective

Insurance companies need accurate pricing models to estimate expected claim costs and set fair premiums.

This project develops an end-to-end motor insurance pricing framework using actuarial statistical models and machine learning techniques.

The project follows the pure premium approach:

**Pure Premium = Claim Frequency × Claim Severity**

The objective was to compare different modeling approaches and identify the best-performing pricing framework.

---

## Dataset

This project uses the French Motor Third-Party Liability (MTPL) insurance datasets:

- freMTPL2freq
- freMTPL2sev

The datasets contain information about:

- Policy exposure
- Claim frequency
- Claim amounts
- Driver characteristics
- Vehicle characteristics
- Geographic variables

The frequency dataset was used to predict the number of claims, while the severity dataset was used to predict claim costs.

---

## Modeling Approach

Multiple actuarial and machine learning models were developed.

### Frequency Models

- Poisson GLM
- Negative Binomial GLM
- XGBoost

### Severity Models

- Gamma GLM
- Tweedie GLM
- XGBoost

Different frequency and severity combinations were evaluated to create the final pure premium prediction framework.

---

## Key Results

The best-performing pricing model was:

**XGBoost Frequency + Tweedie Severity**

Performance:

- RMSE: 14,249.12
- MAE: 2,174.84

This model achieved the lowest prediction error among all tested combinations.

---

## Model Explainability

SHAP analysis was used to understand the main factors influencing predictions.

The most important risk drivers were:

1. Exposure
2. BonusMalus
3. Driver Age
4. Density
5. Vehicle Age

These variables provide meaningful explanations for differences in predicted insurance risk.

---

## Recommendation

The recommended pricing framework is:

**XGBoost Frequency + Tweedie Severity**

The model provides:

- Strong predictive performance
- Ability to capture complex risk patterns
- Improved customer risk segmentation
- Explainable predictions

For production use, identifier variables such as IDpol should be removed because they do not represent actual risk characteristics.

---

## Future Improvements

Possible future improvements include:

- Hyperparameter optimization
- Cross-validation
- Additional machine learning models
- Automated deployment pipeline
- Continuous model monitoring