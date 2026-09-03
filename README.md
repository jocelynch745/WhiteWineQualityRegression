# White Wine Quality Regression Analysis

## Overview

This project investigates how physicochemical properties of white wine are associated with perceived wine quality.

Using the White Wine Quality dataset from the UCI Machine Learning Repository, I analyzed 4,898 wine samples with 11 physicochemical features and a sensory quality score.

The analysis focuses on identifying the most important chemical characteristics associated with wine quality and evaluating whether a simplified regression model can maintain similar explanatory power to a full model.

The project was completed in R using multiple linear regression, AIC-based model selection, regression diagnostics, and bootstrap confidence intervals.

---

## Research Questions

This analysis focuses on the following questions:

1. Which physicochemical characteristics are most strongly associated with white wine quality?
2. Can an AIC-based reduced regression model provide similar or better model performance than a full model?
3. Are the estimated effects of the key predictors stable under bootstrap resampling?

---

## Dataset

The dataset contains 4,898 observations of Portuguese white Vinho Verde wines.

Each observation contains 11 physicochemical measurements:

- Fixed acidity
- Volatile acidity
- Citric acid
- Residual sugar
- Chlorides
- Free sulfur dioxide
- Total sulfur dioxide
- Density
- pH
- Sulphates
- Alcohol

The response variable is:

- `quality`: sensory quality score assigned by wine experts

Source: Cortez et al. (2009), UCI Machine Learning Repository.

---

## Methods

The analysis was performed in R and included:

- Exploratory data analysis
- Correlation analysis
- Multiple linear regression
- AIC-based stepwise model selection
- Adjusted R-squared model comparison
- Residual diagnostics
- Normal Q-Q analysis
- Bootstrap confidence intervals with 1,000 resamples

Two regression models were compared:

### Full Model

The full model included all 11 physicochemical predictors.

### AIC-Reduced Model

Stepwise AIC selection was applied starting from the full model.

The final reduced model retained eight predictors:

- Fixed acidity
- Volatile acidity
- Residual sugar
- Free sulfur dioxide
- Density
- pH
- Sulphates
- Alcohol

---

## Model Comparison

| Model | Number of Predictors | AIC | Adjusted R² |
|------|------:|------:|------:|
| Full Model | 11 | 11113.48 | 0.2803 |
| AIC-Reduced Model | 8 | 11108.29 | 0.2806 |

The reduced model achieved a lower AIC while maintaining approximately the same adjusted R².

Therefore, the AIC-reduced model was selected as the primary model for further interpretation and diagnostics.

---

## Key Findings

Three variables showed particularly strong relationships with wine quality.

### Volatile Acidity

Volatile acidity had a strong negative association with predicted wine quality.

The estimated coefficient was approximately:

`β = -1.89`

Holding the other predictors constant, higher volatile acidity was associated with lower predicted wine quality.

### Alcohol

Alcohol showed a positive association with wine quality.

The estimated coefficient was approximately:

`β = 0.19`

A one-percentage-point increase in alcohol content was associated with approximately a 0.19-point increase in predicted wine quality, holding the other predictors constant.

### Density

Density had a negative coefficient of approximately:

`β = -154`

Because density varies over a very small numerical range around 1.0, the coefficient should be interpreted relative to realistic changes in density.

For example, a 0.001 increase in density corresponds to approximately a 0.15-point decrease in predicted quality.

---

## Model Diagnostics

Regression assumptions were evaluated using:

- Residuals vs. Fitted plot
- Normal Q-Q plot

The residual plot did not show a strong nonlinear pattern or a major change in residual variance.

The diagonal bands visible in the residual plot are expected because wine quality is recorded as discrete integer scores.

The Q-Q plot showed that most residuals followed the theoretical normal line, with some deviations in the tails.

Overall, the diagnostic plots did not indicate major violations of the linear regression assumptions.

---

## Bootstrap Analysis

To evaluate the stability of the key coefficient estimates, I generated 1,000 bootstrap samples and compared bootstrap confidence intervals with conventional normal confidence intervals.

| Predictor | Normal 95% CI | Bootstrap 95% CI |
|------|------|------|
| Volatile Acidity | [-2.10, -1.67] | [-2.12, -1.67] |
| Alcohol | [0.15, 0.24] | [0.08, 0.27] |
| Density | [-190, -118] | [-248, -93] |

None of the confidence intervals contained zero.

The bootstrap results were generally consistent with the conventional regression intervals, suggesting that the main coefficient conclusions were reasonably stable.

---

## Conclusion

The analysis suggests that alcohol, volatile acidity, and density are among the most important physicochemical variables associated with white wine quality.

Higher alcohol content was associated with higher quality ratings, while higher volatile acidity and density were associated with lower predicted quality.

The AIC-reduced model used fewer predictors than the full model while achieving a slightly lower AIC and similar adjusted R².

However, the model explains only about 28% of the variation in wine quality, indicating that physicochemical measurements alone cannot fully explain sensory quality ratings.

Future work could explore nonlinear relationships and interactions using methods such as generalized additive models, random forests, or boosting.

---

## Tools & Skills

- R
- R Markdown
- Exploratory Data Analysis
- Multiple Linear Regression
- Model Selection
- AIC
- Regression Diagnostics
- Bootstrap Inference
- Statistical Interpretation

---

## Repository Structure

```text
.
├── README.md
├── 5030_Project.Rmd
├── 5030_Project.html
├── 5030_Project_Report.pdf
├── data/
│   └── winequality-white.csv
└── figures/
    ├── residuals_vs_fitted.png
    └── qq_plot.png
