# Insurance Pricing Platform - Technical Report

## 1. Introduction

Insurance pricing requires accurate estimation of expected claim costs for policyholders.

This project develops an end-to-end motor insurance pricing framework using actuarial statistical models and machine learning approaches.

The pricing framework follows the pure premium methodology:

Pure Premium = Claim Frequency × Claim Severity

The objective is to compare different modeling techniques and identify the best-performing pricing approach.

---

# 2. Dataset Description

The project uses the French Motor Third-Party Liability (MTPL) datasets:

- freMTPL2freq
- freMTPL2sev

The datasets contain information about:

- Policy exposure
- Claim frequency
- Claim severity
- Driver characteristics
- Vehicle characteristics
- Geographic information

The frequency dataset was used to model the number of claims, while the severity dataset was used to model claim costs.

---

# 3. Exploratory Data Analysis

Initial analysis was performed to understand:

- Claim frequency distribution
- Percentage of zero claims
- Claim severity distribution
- Feature relationships

Key observations:

- Insurance claims are highly skewed.
- Most policyholders have zero claims.
- Claim severity contains extreme values.
- Exposure strongly influences observed claim frequency.

---

# 4. Frequency Modeling

The following models were developed:

## Poisson GLM

Used as a traditional actuarial baseline model for claim frequency prediction.

## Negative Binomial GLM

Developed to handle overdispersion where claim variance exceeds the mean.

## XGBoost Frequency Model

A machine learning approach was developed to capture nonlinear relationships between risk factors and claim frequency.

---

# 5. Severity Modeling

Severity modeling was performed on policies with positive claims.

The following models were evaluated:

## Gamma GLM

A classical actuarial model suitable for positive continuous claim amounts.

## Tweedie GLM

Used because Tweedie distributions are commonly applied to insurance loss modeling.

## XGBoost Severity Model

A machine learning approach used to capture complex claim cost patterns.

---

# 6. Pure Premium Framework

The final pricing models were created by combining frequency and severity predictions:

Pure Premium = Predicted Frequency × Predicted Severity

Multiple combinations were evaluated:

- Poisson + Gamma
- Poisson + Tweedie
- Poisson + XGBoost
- Negative Binomial + Gamma
- Negative Binomial + Tweedie
- Negative Binomial + XGBoost
- XGBoost Frequency + Gamma
- XGBoost Frequency + Tweedie
- XGBoost Frequency + XGBoost Severity
---

# 7. Model Performance Evaluation

The developed pricing models were evaluated using prediction error metrics:

- Root Mean Squared Error (RMSE)
- Mean Absolute Error (MAE)

The final pure premium models were created by combining different frequency and severity model combinations.

## Model Comparison Results

| Rank | Model Combination | RMSE | MAE |
|---|---|---|---|
| 1 | XGBoost Frequency + Tweedie Severity | 14249.12 | 2174.84 |
| 2 | XGBoost Frequency + Gamma Severity | 14249.16 | 2174.94 |
| 3 | XGBoost Frequency + XGBoost Severity | 14250.10 | 2177.42 |
| 4 | Poisson Frequency + Tweedie Severity | 14251.46 | 2175.87 |
| 5 | Poisson Frequency + Gamma Severity | 14251.49 | 2176.12 |
| 6 | Negative Binomial Frequency + Tweedie Severity | 14251.49 | 2175.33 |
| 7 | Negative Binomial Frequency + Gamma Severity | 14251.52 | 2175.59 |
| 8 | Negative Binomial Frequency + XGBoost Severity | 14252.07 | 2181.04 |
| 9 | Poisson Frequency + XGBoost Severity | 14252.09 | 2181.45 |

---

# 8. Final Model Selection

The best-performing pricing framework was:

## XGBoost Frequency + Tweedie Severity

The model achieved:

- RMSE: 14,249.12
- MAE: 2,174.84

This combination provided the lowest prediction error among all tested approaches.

The results demonstrate that machine learning methods can capture complex relationships in insurance pricing while maintaining the ability to explain important risk factors.

---

# 9. Model Explainability Using SHAP

SHAP (SHapley Additive exPlanations) was used to interpret the XGBoost model predictions.

The analysis identified the variables that contributed most strongly to predicted insurance risk.

## Top Feature Contributions

| Feature | Mean SHAP Value |
|---|---|
| Exposure | 0.457 |
| IDpol | 0.405 |
| BonusMalus | 0.274 |
| Driver Age | 0.108 |
| Density | 0.093 |
| Vehicle Age | 0.076 |
| Vehicle Brand | 0.054 |
| Vehicle Gas Type | 0.038 |
| Region | 0.022 |
| Vehicle Power | 0.018 |

## Business Interpretation

The most influential genuine risk factors were:

- Exposure: represents the amount of time a policy is observed and directly affects expected claims.
- BonusMalus: captures previous driving risk and claim history.
- Driver Age: reflects differences in driving behavior and risk.
- Density: represents geographical risk differences.
- Vehicle Age: contributes to differences in vehicle-related claim patterns.

Note: Identifier variables such as IDpol should be removed from production models because they do not represent actual risk characteristics.

---

# 10. Conclusion and Recommendation

This project developed a complete insurance pricing pipeline using actuarial and machine learning methods.

The recommended pricing framework is:

**XGBoost Frequency + Tweedie Severity**

because it achieved the best predictive performance while providing interpretable risk drivers through SHAP analysis.

The developed framework demonstrates how statistical models and machine learning techniques can be combined to improve insurance pricing accuracy and risk segmentation.

Future improvements could include:

- Hyperparameter optimization
- Cross-validation
- Additional machine learning algorithms
- Automated deployment pipeline
- Model monitoring
  ---

# 11. Final Conclusion

This project developed a complete motor insurance pricing framework using actuarial and machine learning techniques.

The approach separated the pricing problem into claim frequency and claim severity components and combined them to estimate pure premium.

Among all tested combinations, XGBoost Frequency combined with Tweedie Severity achieved the best predictive performance.

The final model provides both:
- strong predictive accuracy
- interpretable risk drivers through SHAP analysis

The framework demonstrates how modern machine learning techniques can complement traditional actuarial methods for insurance pricing.