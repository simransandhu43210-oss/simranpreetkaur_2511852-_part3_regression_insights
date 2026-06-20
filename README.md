# simranpreetkaur_2511852-_part3_regression_insights
# Part 3: Regression-Based Business Insights & Model Interpretation

## Business Problem Summary

You are a business analyst for a retail chain. The leadership team wants to understand what factors are driving monthly sales performance across stores. They are considering business actions such as increasing marketing spend, improving inventory availability, changing discounting strategy, reallocating staff, and prioritising certain store types or regions. The goal of this analysis is to use regression to identify which factors are most strongly associated with monthly sales and provide an evidence-based recommendation.

---

## Dataset Description

- **File:** `business_regression_data.xlsx`
- **Sheet:** `store_performance`
- **Rows:** 320 (80 stores × 4 months)
- **Columns:** 14

| Column | Type | Description |
|--------|------|-------------|
| store_id | Categorical (ID) | Unique store identifier |
| month | Date | Month of observation |
| region | Categorical | Store region: East, North, South, West |
| store_type | Categorical | Store type: Residential, High Street, Airport, Mall |
| marketing_spend | Numerical | Monthly marketing expenditure (₹) |
| footfall | Numerical | Number of customers visiting the store |
| avg_discount_pct | Numerical | Average discount offered (as decimal, e.g. 0.15 = 15%) |
| staff_count | Numerical | Number of staff deployed |
| inventory_availability_pct | Numerical | % of inventory available on shelves |
| competitor_distance_km | Numerical | Distance to nearest competitor (km) |
| holiday_flag | Binary (0/1) | 1 if month contains a major holiday |
| customer_rating | Numerical | Average customer rating (1–5) |
| monthly_sales | Numerical | **DEPENDENT VARIABLE** — Total monthly sales (₹) |
| monthly_profit | Numerical | Monthly profit (₹) — excluded to avoid data leakage |

---

## Dependent and Independent Variables

**Dependent Variable:** `monthly_sales`

**Independent Variables used in regression:**
- `footfall` (numerical)
- `marketing_spend` (numerical)
- `staff_count` (numerical)
- `inventory_availability_pct` (numerical)
- `store_type` (categorical → converted to dummy variables)

**Variables excluded and reasons:**
- `store_id` — Identifier only, no predictive meaning
- `month` — Time index, not a business driver
- `monthly_profit` — Derived from sales; using it would cause data leakage
- `avg_discount_pct` — Correlation r = -0.09, p = 0.10 (not statistically significant)
- `customer_rating` — Correlation r = -0.03, p = 0.64 (not statistically significant)
- `competitor_distance_km` — Correlation r = -0.11, p = 0.056 (borderline, excluded for model clarity)
- `holiday_flag` — Weak correlation r = 0.20 (not included in final model to keep model interpretable)
- `region` — store_type already captures location-level differences; region not added to avoid multicollinearity

---

## Data Cleaning Steps

| Issue | Column | Action Taken |
|-------|--------|--------------|
| 8 missing values | `customer_rating` | Filled with column median (3.9) |
| 6 missing values | `competitor_distance_km` | Filled with column median (3.365 km) |

---

## Dummy Variable Approach

Categorical variable `store_type` was converted into dummy (binary) variables.

**Reference Category: Residential** (dropped to avoid the dummy variable trap / perfect multicollinearity)

| Dummy Variable | Meaning |
|----------------|---------|
| `store_Airport` | 1 if Airport store, else 0 |
| `store_High Street` | 1 if High Street store, else 0 |
| `store_Mall` | 1 if Mall store, else 0 |

When all three dummies = 0, the store is a **Residential** store (the reference category).

---

## Model Comparison Summary

| Model | Variables | R-squared | Verdict |
|-------|-----------|-----------|---------|
| Simple Regression 1 | footfall | 0.7363 | Strong single predictor |
| Simple Regression 2 | marketing_spend | 0.1672 | Weak standalone predictor |
| Multiple Regression (Final) | footfall + marketing_spend + staff_count + inventory_availability_pct + store_type dummies | **0.8224** | **Best model — selected as final** |

---

## Final Model Selected

**Multiple Regression Model (Model 3)**

**Equation:**
```
monthly_sales = 91,266.06 + 28.94×footfall + 1.1626×marketing_spend + 2,636.17×staff_count + 3,100.12×inventory_availability_pct + 39,962.03×store_Airport + 17,557.64×store_High Street + 28,984.87×store_Mall
```

**R-squared = 0.8224** — The model explains 82.2% of the variation in monthly sales. All predictors are statistically significant (p < 0.05).

---

## Business Recommendation

The strongest driver of monthly sales is **footfall** (customer visits). Leadership should focus on driving foot traffic through promotional events, loyalty programs, and location-based marketing. **Inventory availability** and **staff count** are also significant — ensuring shelves are stocked and adequate staff are deployed directly translates to higher sales. **Airport stores** generate the highest sales premium (≈₹39,962 more than Residential stores on average), making them a priority for investment.

**Marketing spend** has a statistically significant but modest effect — each additional ₹1 in marketing generates approximately ₹1.16 in sales. It should be maintained but not over-relied upon as the primary growth lever.

---

## Assumptions and Limitations

- Regression shows **association, not causation** — higher footfall may be caused by other factors not in the dataset
- The model assumes a **linear relationship** between predictors and sales
- `region` was not included; there may be unmeasured regional effects
- The dataset covers only **4 months** — seasonal effects cannot be fully captured
- Outlier stores (large residuals) suggest the model may under-predict high-performing stores and over-predict underperformers

---

## Screenshots Included

- `screenshots/simple_regression_output.png` — Simple regression output (footfall model)
- `screenshots/multiple_regression_output.png` — Multiple regression coefficients table
- `screenshots/residuals_preview.png` — Predicted values and residuals table
- `screenshots/model_comparison_preview.png` — Model comparison table
