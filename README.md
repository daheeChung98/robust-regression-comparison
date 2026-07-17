# Robust Regression Comparison

## Overview

## Research Question

## Motivation

## Dataset

### California Housing Dataset

This project uses the **California Housing Dataset**, which is a widely used benchmark dataset for regression tasks. It contains housing information collected from districs in California and is available through `scikit-learn`.

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

## Regression Models

- Ordinary Least Squares (OLS)
- Ridge Regression
- LASSO Regression
- Huber Regression

## Evaluation Metrics

- RMSE
- MAE
- R<sup>2</sup>
## Repository Structure

## Future Work

The current comparison was performed on the original California Housing Dataset,

Future work will investigate the robustness of these regression models under synthetic outlier contamination (5%, 10%, and 20%) to better understand the advantages of Huber Regression in challenging settings.
