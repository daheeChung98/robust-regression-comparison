# Baseline Results

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

---

# Response Contamination

Artificial response contamination was introduced to investigate the robustness of different regression methods under abnormal observations.

For each contamination level (0%, 5%, 10%, 20%), the experiment was repeated 30 times using different random seeds.

Average performance metrics were computed across repeated simulations.

## 1. Main Findings

The baseline comparison showed relatively small differences among the four regression models.

However, introducing synthetic contamination substantially changed the conclusions.

As contamination increased,

- OLS exhibited rapidly increasing RMSE and MAE.
- Ridge and LASSO remained sensitive because they still optimize squared-error loss.
- Huber Regression consistently produced lower prediction errors and more stable coefficients.

## 2. Coefficient Stability

Regression coefficients estimated by OLS became increasingly unstable as contamination increased.

Huber Regression maintained considerably more stable coefficient estimates across repeated experiments.

The larges differences were observed for variables that were strongly affected by contaminated observations, indicating that robust estimation can improve model interpretability in addition to prediction accuracy.

## 3. Practical Implications

The experiments demonstrate that evaluating regression models only on clean benchmark datasets may underestimate the practical value of robust regression.

Real-world datasets frequently contain

- recording errors
- abormal observations
- heavy-tailed noise

Undeer these conditions, robust regression methods can substantially improve both predictive performance and parameter stability.

## 4. Limitaions

The current contamination mechanism only modifies the response vaiable.

Although this experiment illustrates the robustness of Huber Regression, it does not fully capture more realistic data-quality issues such as leverage points or heavy-tailed covariates.

These scenarios will be investigated in subsequent experiments.

## 5. Future Work

Future experiments will extend this benchmark by introducing

- Feature contamination
- Heavy-tailed noise

The objective is to investigate how different types of abnormal observations influence both prediction accuracy and coefficient stability.

# Feature Contamination

Artificial outliers were introduced into selected explanatory variables (AveOccup and MedInc) to investigate the robustness of regression models against abnormal predictor values.

Unlike the previous experiment, the response variable remained unchanged while only the explanatory variables were contaminated.

This setting evaluates model sensitivity to leverage points rather than response outliers.

## 1. Main Findings

The feature contamination experiment produced several important observations.

- OLS coefficients changed noticeably after contamination.
- Ridge Regression reduced coefficient fluctuations through L2 regularization but remained influenced by contaminated predictors.
- LASSO continued to shrink less informative variables but was not immune to leverage points.
- Huber Regression generally produced more stable coefficient estimates, although its improvement was smaller than in the response contamination experiment.

Overall, predictor contamination affected parameter estimation more strongly than prediction accuracy.

## 2. Interpretation

### Why was Feature Contamination different?

Huber Regression is designed to reduce the influence of large residuals.

However, feature contamination introduces high-leverage observations that can influence the fitted regression function before residuals become large.

Consequently, Huber Regression remains more robust than ordinary least squares but cannot completely eliminate the influence of contaminated predictors.

This experiment demonstrates that robust loss functions alone may not fully address leverage-point problems.

## 3. Statistical Insight

The comparison between response contamination and feature contamination highlights an important distinction.

Response contamination primarily creates large residuals.

Feature contamination creates influential observations in the predictor space.

Although both scenarios involve abnormal observations, they affect regression estimation through different mechanisms.

Consequently, robustness against response outliers does not necessarily imply robustness against leverage points.

## 4. Practical Implications

Many real-world datasets contain abnormal predictor values arising from

- recording errors
- sensor failures
- data integration issues
- extreme population subgroups

The experiment demonstrates that evaluating predictive performance alone may overlook substantial instability in regression coefficients.

Therefore, coefficient stability should be considered alongside predictive accuracy when comparing regression methods.

## 5. Limitations

Only two explanatory variables were contaminated in this experiment.

Furthermore, contamination was generated through simple multiplicative perturbations rather than realistic adversarial mechanisms.

Additional studies are required to evaluate more complex contamination patterns.

## 6. Future Work

Future experiments will investigate

- heavy-tailed predictor distributions

These experiments will further clarify the strengths and limitations of different robust regression techniques under realistic data-quality challenges.

# Heavy-tailed Noise

Heavy-tailed noise was introduced into the response variable by adding random errors sampled from a Student's t distribution (df = 3).

Unlike the response contamination experiment, which injected a small number of extreme outliers, heavy-tailed noise affected the entire training dataset by increasing the probability of large residuals.

This setting evaluates model robustness when the Gaussian error assumption is violated.

## 1. Main Findings

The heavy-tailed noise experiment revealed several important observations.

- OLS exhibited increased prediction errors because squared-error loss is highly sensitive to frequent large residuals.
- Ridge Regression reduced coefficient variance through L2 regularization but remained sensitive to heavy-tailed errors.
- LASSO continued to perform feature selection but showed similar sensitivity to non-Gaussian residuals.
- Huber Regression maintained comparatively stable prediction performance and coefficient estimates by reducing the influence of large residuals.

Overall, heavy-tailed noise affected both predictive performance and coefficient stability, with Huber Regression showing the greatest robustness.

## 2. Interpretation

### Why was Heavy-tailed Noise different?

Unlike isolated response contamination, heavy-tailed noise changes the entire error distribution.

Instead of a few abnormal observations, moderately large residuals occur much more frequently throughout the dataset.

Because OLS, Ridge, and LASSO all minimize squared-error loss, they assign disproportionately large weight to these residuals.

Huber Regression limits the influence of large residuals through the Huber loss function, allowing parameter estimation to remain more stable under non-Gaussian error distributions.

This experiment demonstrates that robust loss functions remain beneficial even when abnormal observations arise naturally rather than through explicit contamination.

## 3. Statistical Insight

The comparison between response contamination and heavy-tailed noise highlights another important distinction.

Response contamination introduces a relatively small number of extreme observations.

Heavy-tailed noise changes the probability distribution of the residuals, increasing the likelihood of moderate and large errors across the entire dataset.

Although both violate the Gaussian assumption, they represent different sources of model uncertainty.

The experiment illustrates that robustness should be evaluated under both isolated outliers and distributional misspecification.

## 4. Practical Implications

Heavy-tailed error distributions are common in many real-world applications, including

- financial returns
- insurance claims
- biomedical measurements
- environmental observations

In these settings, assuming normally distributed errors may underestimate the frequency of extreme observations.

The results suggest that robust regression methods such as Huber Regression can improve both prediction reliability and coefficient stability when the underlying error distribution deviates from normality.

## 5. Limitations

The experiment considered only one heavy-tailed distribution generated from a Student's t distribution with three degrees of freedom.

In addition, noise was added only to the response variable while the explanatory variables remained unchanged.

Further investigation is required to evaluate different tail heaviness and more complex non-Gaussian data-generating processes.

## 6. Conclusion

The heavy-tailed noise experiment complements the previous contamination studies by examining robustness under distributional misspecification rather than isolated outliers.

Across all experiments, Huber Regression consistently demonstrated greater robustness than classical least-squares methods while maintaining competitive predictive performance.

These findings suggest that robust regression methods provide practical advantages whenever real-world data deviate from ideal Gaussian assumptions, whether through response outliers, contaminated predictors, or heavy-tailed error distributions.
