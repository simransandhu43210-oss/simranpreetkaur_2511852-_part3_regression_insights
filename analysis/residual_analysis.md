# Residual Analysis

## Model Used for Residual Analysis

**Final Model: Multiple Regression**

**Equation:**
```
monthly_sales = 91,266.06 + 28.94×footfall + 1.1626×marketing_spend + 2,636.17×staff_count + 3,100.12×inventory_availability_pct + 39,962.03×store_Airport + 17,557.64×store_High Street + 28,984.87×store_Mall
```

**Residual = Actual monthly_sales − Predicted monthly_sales**

---

## Top 5 Stores with Largest POSITIVE Residuals
*(Model under-predicted — store performed better than expected)*

| Store ID | Store Type | Region | Actual Sales (₹) | Predicted Sales (₹) | Residual (₹) |
|----------|-----------|--------|-------------------|----------------------|--------------|
| STR-1030 | Residential | West | 820,519.04 | 712,863.12 | **+107,655.92** |
| STR-1073 | Residential | East | 813,316.71 | 710,743.06 | **+102,573.65** |
| STR-1028 | Mall | East | 713,611.16 | 615,096.53 | **+98,514.63** |
| STR-1032 | High Street | South | 914,544.17 | 820,285.03 | **+94,259.14** |
| STR-1026 | Mall | East | 625,514.04 | 531,605.80 | **+93,908.24** |

---

## Top 5 Stores with Largest NEGATIVE Residuals
*(Model over-predicted — store performed worse than expected)*

| Store ID | Store Type | Region | Actual Sales (₹) | Predicted Sales (₹) | Residual (₹) |
|----------|-----------|--------|-------------------|----------------------|--------------|
| STR-1017 | High Street | West | 685,379.08 | 839,367.38 | **−153,988.30** |
| STR-1012 | Residential | West | 595,467.60 | 719,855.23 | **−124,387.63** |
| STR-1023 | Mall | South | 627,171.90 | 742,440.87 | **−115,268.97** |
| STR-1007 | Mall | West | 800,451.94 | 904,299.21 | **−103,847.27** |
| STR-1001 | Residential | East | 658,920.30 | 760,358.83 | **−101,438.53** |

---

## Business Interpretation of Residuals

### Positive Residuals (Under-predicted stores)
Stores like STR-1030 (Residential, West) and STR-1073 (Residential, East) are outperforming what the model predicts based on their footfall, marketing spend, staff, and inventory levels. This could indicate:
- **Local competitive advantage** — fewer nearby competitors not fully captured by the model
- **Exceptional store management** or customer service quality beyond what ratings capture
- **Catchment area strength** — higher disposable income neighbourhoods
- **Unmeasured promotions or local events** driving extra traffic

These stores are potential **best-practice candidates** — leadership should study what they are doing differently.

### Negative Residuals (Over-predicted stores)
Stores like STR-1017 (High Street, West) and STR-1012 (Residential, West) are underperforming despite having favourable input levels. Possible causes:
- **Execution issues** — poor in-store experience, long queues, or product mix mismatch
- **Local market challenges** — declining neighbourhood footfall or strong competition nearby
- **Structural issues** — store layout, accessibility, or parking problems
- **West region underperformance** — 3 of the 5 worst stores are in the West region, suggesting a possible regional issue not captured by the model

---

## Is the Model Under-predicting or Over-predicting Certain Store Types?

| Store Type | Pattern Observed |
|------------|-----------------|
| Residential (West) | Consistently over-predicted — actual sales fall below model expectations |
| Mall (West/South) | Tends to be over-predicted — model may overestimate mall store premium in these regions |
| Residential (East) | Mixed — some under-predicted (STR-1030, STR-1073 outperform), some over-predicted |
| High Street | Mixed — STR-1032 outperforms significantly, STR-1017 underperforms significantly |

**Key finding:** The **West region** appears to underperform relative to model predictions across multiple store types. The model does not include a region variable, which may be causing systematic over-prediction for West region stores. Adding region dummy variables could improve model accuracy for these stores.

---

## Conclusion

The multiple regression model performs well overall (R² = 0.8224), but residuals reveal that some stores have characteristics not captured by the current predictors. The largest residuals are concentrated in West region stores and suggest that **regional effects** may be an important missing variable. Leadership should investigate West region stores specifically to understand the structural barriers to sales performance.
