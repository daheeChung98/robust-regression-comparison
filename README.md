# Robust Regression Comparison

## Overview

This project compares four widely used linear regression models:

- Ordinary Least Squares (OLS)
- Ridge Regression
- LASSO Regression
- Huber Regression

using the California Housing Dataset.

The primary objective is to investigate how regularization and robust loss functions influence model performance, coefficient estimation, and sensitivity to influential observations.

---

## Research Question

This project addresses the following questions:

- How do OLS, Ridge, LASSO, and Huber Regression differ in predictive performance?
- How does regularization affect estimated regression coefficients?
- Does Huber regression produce more stable estimates when influential observations exist?
- Which regression model provides the best trade-off between prediction accuracy and robustness?

---

## Motivation

Ordinary Least Squares (OLS) is one of the mose widely used regression methods, but it is highly sensitive to outliers because it minimizes squared residuals.

Regularized regression methods such as Ridge, and LASSO improve coefficient stability and reduce overfitting, yet they are still based on squared-error loss.

Hubere regression replaces the squared loss with the Huber loss, reducing the influence of large residuals while maintaining good statistical efficiency.

This project aims to compare these approaches under the same experimental setting and build intuition about when robust regression becomes advantageous.

---

## Dataset

### California Housing Dataset

This project uses the **California Housing Dataset**, a standard benchmark dataset for regression probelms available through `scikit-learn`.

**Dataset Summary**

- **Samples:** 20,640
- **Features:** 8 unmerical features
- **Target:** Median house value (in units of \$100,000)

**Features**

| Feature | Description |
|---------|-------------|
| MedInc| Median income in the district |
| HouseAge | Median house age |
| AveRooms | Average number of rooms per household |
| AveBedrms | Average number of bedrooms per household |
| Population | District population |
| AveOccup | Average number of household members |
| Latitude | Geographic latitude |
| Longitude | Geographic longitude |

### Why this dataset?

The California Housing Dataset was selected for the following reasons:

- It is a standard benchmark dataset for regression problems.
- It contains multiple numerical predictors, making it suitable for comparing different regression methods.
- Some predictors exhibit correlations, allowing investigation of multicollinearity.
- Artificial ouliers and noise can be introduced easily to evaluate the robustness of different regression models.
- The dataset is readily availbale through `scikit-learn`, ensuring reproducibility and ease of use.
- In later experiments, synthetic outliers and additional noise will be introduced to evaluate how OLS, Ridge, LASSO, and Huber Regression perform under challenging data conditions.

## Methods

### Regression Models

- Ordinary Least Squares (OLS)
- Ridge Regression
- LASSO Regression
- Huber Regression

### Data Processing

- Train/Test Split
- Feature Standardization
- Model Training
- Prediction

### Evaluation Metrics

- RMSE
- MAE
- R<sup>2</sup>

---

## Results

### Model Performance

Evaluation results are available in
```
results/metrics.csv
```

### Estimated Coefficients

Estimated regression coefficients are available in

```
results/coefficients.csv
```

### Interpretation

Model interpretation and discussion are provided in

```
results/discussion.md
```

### Key Findings

- All four models achieved comparable predictive performance on the original dataset.
- Ridge and LASSO shrank regression coefficients compared with OLS.
- Huber regression produced similar prediction accuracy while reducing the influence of observations with unusually large residuals.
- The largest coefficient changes were observed for **AveOccup**, suggesting sensitivity to influential observations.

---

## Representative Figures

The repository includes visualizations comparing the regression models, including:

- Regression coefficient comparison
- Residual distribution
- Actual vs OLS Predicted values
- Residual vs Huber Predicted values

Figures are stored in:

```
figures/
```

---

## Project Structure

```
robust-regression-comparison/
│
├── data/
├── notebooks/
├── src/
├── figures/
├── results/
│   ├── metrics.csv
│   ├── coefficients.csv
│   └── discussion.md
├── README.md
└── requirements.txt
```

---

## Future Work

The current analysis evaluates regression models on the original California Housing Dataset.

Future work will extend this project by:

- Injecting synthetic outliers (5%, 10%, and 20%)
- Comparing robustness under heavy-tailed noise
- Evaluating coefficient stability under contamination
- Investigating adversarial covariate contamination

---

## References

- Scikit-learn Developers. *California Housing Dataset.*
- Huber, P. J. (1964). Robust Estimation of a Location Parameter.
- Hastie, Tibshirani, & Friedman. *The Elements of Statistical Learning.*
