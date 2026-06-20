# Model Comparison: Simple vs Multiple Regression

## Overview

This document compares all regression models run to predict `monthly_sales` for the retail chain.

---

## Model Summary Table

| Item | Model 1 — Simple (footfall) | Model 2 — Simple (marketing_spend) | Model 3 — Multiple Regression |
|------|-----------------------------|------------------------------------|-------------------------------|
| **Model Name** | Simple Regression 1 | Simple Regression 2 | Multiple Regression (Final) |
| **Dependent Variable** | monthly_sales | monthly_sales | monthly_sales |
| **Independent Variables** | footfall | marketing_spend | footfall, marketing_spend, staff_count, inventory_availability_pct, store_Airport, store_High Street, store_Mall |
| **R-squared** | 0.7363 | 0.1672 | **0.8224** |
| **Adjusted R-squared** | — | — | 0.8184 |
| **Significant Variables** | footfall (p < 0.001) | marketing_spend (p < 0.001) | All (p < 0.05) |
| **Business Usefulness** | Moderate — single factor only | Low — explains only 16.7% of variation | **High — explains 82.2% of variation** |
| **Limitations** | Ignores all other factors | Very weak predictive power | Assumes linearity; excludes region |

---

## Detailed Model Outputs

### Model 1: Simple Regression — footfall

**Equation:** `monthly_sales = 446,410.58 + 35.68 × footfall`

| Metric | Value |
|--------|-------|
| Intercept | 446,410.58 |
| Coefficient (footfall) | 35.68 |
| R-squared | 0.7363 |
| P-value | < 0.001 |

**Interpretation:** Footfall alone explains 73.6% of monthly sales variation. For every additional customer visit, monthly sales increase by approximately ₹35.68. This is statistically strong and practically meaningful. However, the model ignores marketing, staffing, inventory, and store type — all of which also matter.

**Business usefulness:** Useful as a quick indicator. If leadership wants one metric to track, footfall is the strongest single signal.

---

### Model 2: Simple Regression — marketing_spend

**Equation:** `monthly_sales = 560,777.35 + 2.13 × marketing_spend`

| Metric | Value |
|--------|-------|
| Intercept | 560,777.35 |
| Coefficient (marketing_spend) | 2.13 |
| R-squared | 0.1672 |
| P-value | < 0.001 |

**Interpretation:** Marketing spend explains only 16.7% of monthly sales variation. While statistically significant, it is a **weak standalone predictor**. The coefficient of 2.13 means every ₹1 increase in marketing spend is associated with ₹2.13 in additional sales — a positive ROI signal, but marketing alone does not drive sales strongly.

**Business usefulness:** Limited when used alone. Marketing spend works better as part of a multi-factor model.

---

### Model 3: Multiple Regression (Final Model)

**Equation:**
```
monthly_sales = 91,266.06
              + 28.94 × footfall
              + 1.1626 × marketing_spend
              + 2,636.17 × staff_count
              + 3,100.12 × inventory_availability_pct
              + 39,962.03 × store_Airport
              + 17,557.64 × store_High Street
              + 28,984.87 × store_Mall
```

| Variable | Coefficient | P-value | Significant? |
|----------|-------------|---------|--------------|
| Intercept | 91,266.06 | 0.036 | YES * |
| footfall | 28.94 | < 0.001 | YES *** |
| marketing_spend | 1.1626 | < 0.001 | YES *** |
| staff_count | 2,636.17 | 0.039 | YES * |
| inventory_availability_pct | 3,100.12 | < 0.001 | YES *** |
| store_Airport | 39,962.03 | < 0.001 | YES *** |
| store_High Street | 17,557.64 | 0.004 | YES ** |
| store_Mall | 28,984.87 | < 0.001 | YES *** |

**R-squared = 0.8224 | Adjusted R-squared = 0.8184**

**Business usefulness:** This is the best model. It explains 82.2% of monthly sales variation using actionable business variables. All predictors are statistically significant.

**Limitations:** Does not include region-level effects; assumes a linear relationship; based on only 4 months of data.

---

## Why Multiple Regression is Superior

The multiple regression model adds 8.6 percentage points of explanatory power over the best simple model (footfall alone: R² = 0.7363 vs combined: R² = 0.8224). Crucially, it isolates the independent contribution of each factor, allowing leadership to make targeted decisions — for example, increasing inventory availability or deploying more staff — rather than relying on a single metric.

---

## Winner: Model 3 — Multiple Regression

Selected as the final model due to highest R-squared (0.8224), all significant predictors, and the most actionable business insights.
