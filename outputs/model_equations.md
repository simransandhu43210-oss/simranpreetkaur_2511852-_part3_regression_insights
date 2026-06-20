# Model Equations & Dummy Variable Explanation

## Simple Regression Equations

### Model 1: footfall → monthly_sales

```
monthly_sales = 446,410.58 + 35.68 × footfall
```

| Term | Value | Meaning |
|------|-------|---------|
| Intercept (b0) | 446,410.58 | Baseline monthly sales when footfall = 0 (theoretical starting point) |
| Coefficient b1 (footfall) | 35.68 | For every 1 additional customer visit, monthly sales increase by ₹35.68 |
| R-squared | 0.7363 | Footfall alone explains 73.6% of variation in monthly sales |
| P-value | < 0.001 | Highly statistically significant |

---

### Model 2: marketing_spend → monthly_sales

```
monthly_sales = 560,777.35 + 2.13 × marketing_spend
```

| Term | Value | Meaning |
|------|-------|---------|
| Intercept (b0) | 560,777.35 | Baseline monthly sales when marketing spend = ₹0 |
| Coefficient b1 (marketing_spend) | 2.13 | For every ₹1 increase in marketing spend, monthly sales increase by ₹2.13 |
| R-squared | 0.1672 | Marketing spend alone explains only 16.7% of variation in monthly sales |
| P-value | < 0.001 | Statistically significant but weak standalone predictor |

---

## Multiple Regression Equation (Final Model)

```
monthly_sales = 91,266.06
              + 28.94    × footfall
              + 1.1626   × marketing_spend
              + 2,636.17 × staff_count
              + 3,100.12 × inventory_availability_pct
              + 39,962.03 × store_Airport
              + 17,557.64 × store_High Street
              + 28,984.87 × store_Mall
```

**R-squared = 0.8224 | Adjusted R-squared = 0.8184**

---

## Explanation of Each Coefficient

| Variable | Coefficient | Business Meaning |
|----------|-------------|-----------------|
| Intercept | 91,266.06 | Baseline monthly sales for a Residential store with all other predictors at zero |
| footfall | 28.94 | Each additional customer visit adds ₹28.94 to monthly sales, holding all else constant |
| marketing_spend | 1.1626 | Each additional ₹1 spent on marketing adds ₹1.16 to monthly sales, holding all else constant |
| staff_count | 2,636.17 | Each additional staff member deployed adds ₹2,636 to monthly sales, holding all else constant |
| inventory_availability_pct | 3,100.12 | Each 1 percentage point increase in inventory availability adds ₹3,100 to monthly sales |
| store_Airport | 39,962.03 | Airport stores earn ₹39,962 more per month than Residential stores (all else equal) |
| store_High Street | 17,557.64 | High Street stores earn ₹17,558 more per month than Residential stores (all else equal) |
| store_Mall | 28,984.87 | Mall stores earn ₹28,985 more per month than Residential stores (all else equal) |

---

## Dummy Variable Explanation

### Why dummy variables are needed
The variable `store_type` has 4 categories: **Residential, High Street, Airport, Mall**. Regression requires numerical inputs. We convert each category into a binary (0 or 1) column.

### Reference Category: Residential
To avoid the **dummy variable trap** (perfect multicollinearity), one category must be dropped. We drop **Residential** as the reference category. All store_type coefficients are interpreted *relative to a Residential store*.

### Dummy variable encoding

| Store Type | store_Airport | store_High Street | store_Mall | Interpretation |
|-----------|--------------|-------------------|------------|----------------|
| Residential | 0 | 0 | 0 | **Reference category** |
| Airport | 1 | 0 | 0 | Adds ₹39,962 vs Residential |
| High Street | 0 | 1 | 0 | Adds ₹17,558 vs Residential |
| Mall | 0 | 0 | 1 | Adds ₹28,985 vs Residential |

---

## Final Model Selected: Multiple Regression

**Reason for selection:**
1. Highest R-squared (0.8224) — explains 82.2% of monthly sales variation
2. All 7 predictors are statistically significant (p < 0.05)
3. Includes both numerical drivers (footfall, inventory, staff) and store type context
4. Enables actionable decisions across multiple levers simultaneously
5. Adjusted R-squared (0.8184) confirms the model is not over-fitted

The simple regression models are useful for understanding individual variable effects but lack the explanatory power and practical completeness of the multiple regression model. The final model allows leadership to evaluate trade-offs — e.g., is it better to invest ₹1 more in marketing or hire one additional staff member? The coefficients directly answer this.
