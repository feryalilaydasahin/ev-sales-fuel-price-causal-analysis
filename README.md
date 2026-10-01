# Does Gasoline Price Drive EV Sales?
### ML forecasting, explainable AI (SHAP) and causal inference

**Question:** Do higher gasoline prices increase electric vehicle sales, and under which conditions?

**Data:** [EV Market Master Dataset](https://www.kaggle.com/) (Kaggle, CC BY 4.0) — 8 countries, 9 country–brand series, monthly, 2019–2023, 420 observations.

## Approach
1. **Forecasting:** Random Forest, XGBoost and LightGBM vs. a naive "last month" baseline, with a time-based split (train 2019–2022, test 2023)
2. **Explainability:** SHAP summary, dependence and waterfall plots
3. **Causal inference:** Double Machine Learning (LinearDML) and Causal Forest DML (EconML), with a log-scale robustness check

## Key findings
- Random Forest reached R² = 0.966 on 2023, but the naive baseline did as well (R² = 0.968): sales in this dataset are quarterly figures split into months, so past sales dominate.
- Raw data shows a **negative** correlation between gasoline price and EV sales, driven by cross-country differences.
- After controlling for confounders, **no statistically significant causal effect** was found (LinearDML ATE CI and Causal Forest ATE CI both include zero; log model: +0.10 USD/L → +1.5%, 95% CI −3.5% to +6.7%).

## What I learned
The first version of this project reported much stronger results. A review revealed **data leakage** (a rolling average that included the current month), a train/test split that was not chronological, and a misreported causal coefficient. Fixing these changed the conclusion — a good reminder that correlation and a high R² are not evidence of causation.

## Files
| File | Description |
|---|---|
| `EV_sales_fuel_prices_duzeltilmis.ipynb` | Full analysis with outputs |
| `Rapor_duzeltilmis.pdf` | Detailed report (Turkish) |
| `ev_market_master.csv` | Dataset |

**Tools:** Python, pandas, scikit-learn, XGBoost, LightGBM, SHAP, EconML, matplotlib, seaborn

*Feryal İlayda Şahin — Industrial Engineering, İstanbul University-Cerrahpaşa*
