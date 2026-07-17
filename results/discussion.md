# Discussion

## Key Findings

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

## Overall Interpretation

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



