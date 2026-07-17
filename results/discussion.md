# Discussion

## 1. Summary of Results

| Model | RMSE | MAE | R<sup>2</sup> |
|------|------|------|------|
| OLS | 0.7456 | 0.5332 | 0.5758 |
| Ridge | 0.7456 | 0.5332 | 0.5758 |
| LASSO | 0.7404 | 0.5353 | 0.5816 |
| Huber | 0.7584 | 0.5158 | 0.5610 |

Although all four models achieved similar predictive performance on the original dataset,
their coefficient estimates revealed meaningful differences.

OLS and Ridge behaved similarly because the dataset contains relatively mild multicollinearity.

LASSO demonstrated automatic feature selection.

Huber Regression produced the largest coefficient changes, indicatin greater robustness against influential observations.

---

## 2. Interpretation by Model

### Ordinary Least Squares (OLS)

OLS serves as the baseline regression model without regularization.
It provides interpretable coefficients but is sensitive to multicollinearity and outliers.

### Ridge Regression

Ridge Regression produced coefficients very similar to OLS while reducing coefficient variance through L2 regularization.
Since the California Housing Dataset does not exhibit severe multicollinearity, the predictive performance remained close to OLS.

### LASSO Regression

LASSO performed implicit feature selection by shrinking some coefficients toward zero.
For example, the coefficient of **Population** became nearly zero, suggesting that this variable contributes relatively little once other predictors are considered.

### Huber Regression

Huber Regression assigned noticeably different coefficients, especially for **AveOccup**.
This indicates that Huber Loss reduced the influence of observations with unusally large occupancy values, resulting in a model that is more robust to potential outliers.

---

## 3. Statistical Insights

### Why did Ridge perform similarly to OLS?

The predictive performance of Ridge Regression was almost identical to that of OLS.
This is expected because the California Housing Dataset does not contain severe multicollinearity.
The L2 penalty therefore had only a limited effect on the estimated coefficients.

### Why did LASSO remove Population?

LASSO shrinks less informative coefficients toward zero.
The Population variable received a coeeficient close to zero, suggesting that it provides limited additional predictive information after accounting for the remaining features.

### Why did Huber change AveOccup?

The coefficient associsted with AveOccup changed substantially under Huber Regression. 
This suggests that observations with unsually high occupancy values may have influenced the OLS etimates.
Huber Loss reduced their impact by down-weighting large residuals.

### Why does this imply?

Although all models achieved similar predictive accuracy,
their parameter estimates differed considerably.

This highlights that rousstness is not only about predictive performance, 
but also about obtaining reliable coefficient estimates under challenging data conditions.

---

## 4. Limitations

The current comparison was conducted using the original California Housing Dataset.
The dataset contains relatively few extreme outliers, which may limit the observed advantages of Huber Regression.

---

## 5. Future Work

Introduce synthetic outliers (5%, 10%, and 20%) and compare the robustness of the four regression models.
