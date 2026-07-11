# Insurance-pricing-platform-GLM-VS-Xgboost-
End-to-end motor insurance pricing platform using actuarial models and machine learning
# Insurance Pricing Platform

## Project Overview

This project develops an end-to-end insurance pricing framework using the French Motor Third-Party Liability (MTPL) datasets. The objective is to estimate the expected insurance premium by separately modeling claim frequency and claim severity and combining them into a pure premium estimate.

Both traditional actuarial techniques and machine learning models are evaluated and compared to identify the most suitable pricing model.

---

## Objectives

- Perform exploratory data analysis on insurance policy data.
- Build claim frequency models.
- Build claim severity models.
- Calculate pure premium.
- Compare statistical and machine learning models.
- Interpret model predictions using SHAP.

---

## Dataset

This project uses the **French Motor Third-Party Liability (MTPL) Insurance** datasets:

- **freMTPL2freq** – Claim frequency data
- **freMTPL2sev** – Claim severity data

The datasets contain policyholder, vehicle, exposure, and claims information used to develop motor insurance pricing models.

Key variables include:

- Policy exposure
- Claim count
- Claim amount
- Driver age
- Vehicle age
- Vehicle power
- Vehicle brand
- Region
- Fuel type
- Bonus-Malus score

---

## Models Developed

### Frequency Models

- Poisson GLM
- Negative Binomial GLM
- XGBoost

### Severity Models

- Gamma GLM
- Tweedie GLM
- XGBoost

---

## Project Workflow

1. Data Understanding
2. Exploratory Data Analysis
3. Frequency Modeling
4. Severity Modeling
5. Pure Premium Calculation
6. Calibration
7. SHAP Explainability

---

## Repository Structure

insurance-pricing-platform/

- notebooks/
- data/
- models/
- results/
- figures/
- reports/

---

## Technologies Used

- Python
- Pandas
- NumPy
- Statsmodels
- Scikit-learn
- XGBoost
- SHAP
- Matplotlib
- Seaborn
- ---

## Results

The project compares classical actuarial models and machine learning approaches for both claim frequency and claim severity prediction.

### Frequency Models
- Poisson GLM
- Negative Binomial GLM
- XGBoost

### Severity Models
- Gamma GLM
- Tweedie GLM
- XGBoost

Model performance was evaluated using:

- RMSE
- MAE
- Deviance
- Calibration Analysis

The final pure premium was calculated by combining the predicted claim frequency and predicted claim severity.

SHAP analysis was used to interpret the machine learning models and identify the key variables influencing insurance risk.
---

## How to Run

1. Clone the repository.
2. Install the required Python packages listed in `requirements.txt`.
3. Open the notebooks in the `notebooks/` directory.
4. Run the notebooks in numerical order:
   - 01 Data Understanding
   - 02 Exploratory Data Analysis
   - 03 Poisson GLM
   - 04 Negative Binomial GLM
   - 05 XGBoost Frequency
   - 06 Gamma & Tweedie Severity
   - 07 XGBoost Severity
   - 08 Pure Premium Framework
   - 09 Calibration & SHAP
   ---

## Model Performance Results

The final pricing framework was evaluated by combining different frequency and severity model combinations.

Performance was measured using:

- Root Mean Squared Error (RMSE)
- Mean Absolute Error (MAE)

### Pure Premium Model Comparison

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

### Final Model Recommendation

The best-performing pricing model was:

**XGBoost Frequency + Tweedie Severity**

This combination achieved the lowest RMSE and MAE, indicating the strongest predictive performance for estimating insurance pure premiums.

The model combines the flexibility of gradient boosting for claim frequency prediction with the Tweedie distribution's ability to model insurance claim severity and zero-inflated loss distributions.
---

## Model Explainability (SHAP)

SHAP (SHapley Additive exPlanations) was used to interpret the XGBoost pricing model and identify the main variables influencing insurance risk predictions.

### Top Risk Drivers

| Rank | Feature | Mean SHAP Value |
|---|---|---|
| 1 | Exposure | 0.457 |
| 2 | IDpol | 0.405 |
| 3 | BonusMalus | 0.274 |
| 4 | Driver Age | 0.108 |
| 5 | Density | 0.093 |
| 6 | Vehicle Age | 0.076 |
| 7 | Vehicle Brand | 0.054 |
| 8 | Vehicle Gas Type | 0.038 |
| 9 | Region | 0.022 |
| 10 | Vehicle Power | 0.018 |

### Business Interpretation

The SHAP analysis shows that exposure, driver characteristics, vehicle characteristics, and geographical factors are important contributors to insurance risk.

The BonusMalus variable is one of the strongest behavioural risk indicators, showing the importance of previous driving history in premium calculation.

Driver age, vehicle age, and regional density also influence expected claim risk and help explain differences between policyholders.

Note: Identifier variables such as IDpol should generally be excluded from production pricing models because they do not represent genuine risk characteristics.
