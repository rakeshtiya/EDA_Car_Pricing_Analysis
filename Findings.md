# 📄 BMW Car Pricing — EDA Findings

## 1) Executive Summary
- 50,000-row BMW dataset; **no missing values, no duplicates, no outliers** detected by IQR.
- Numeric features (Year, Engine_Size_L, Mileage_KM, Sales_Volume) show **near-zero correlation** with Price.
- **Regression (Price ~ Engine_Size_L)**: R² ≈ 0 → engine size does **not** explain price in this dataset.
- Implication: **Categorical factors** (Model, Region, Fuel_Type, Transmission) likely drive pricing differences.

## 2) Data Snapshot
- Rows: **50,000** | Columns: **11**  
- Categorical: Model, Region, Color, Fuel_Type, Transmission, Sales_Classification  
- Numeric: Year, Engine_Size_L, Mileage_KM, Price_USD, Sales_Volume  
- Sample ranges: Year **2010–2024**, Price **$30k–$120k**, Mileage **3–199,996 km**, Engine **1.5–5.0 L**.

## 3) Data Quality
- Missing values: **0**  
- Duplicates: **0**  
- Outliers (IQR ± 1.5×): **0 across numeric columns**  
- Interpretation: Pre-validated/synthetic-like dataset; analysis focuses on pattern discovery rather than cleaning.

## 4) Univariate Highlights
- **Price** centered ~ **$75,000** (balanced spread).  
- **Engine Size** between **1.5–5.0 L**.  
- **Mileage** spans near-uniformly, enabling fair comparisons of used vs newer vehicles.

**Visuals:**  
![Price Histogram](images/price_hist.png)  
![Correlation Heatmap](images/corr_heatmap.png)

## 5) Bivariate Highlights
- **Mileage ↔ Price**: No visible downward trend.  
- **Engine Size ↔ Price**: No clear upward trend.  
- **Category comparisons** (from grouped means):
  - Regions show modest price differences (NA typically higher).
  - Automatic transmission has slightly higher mean price than Manual.

## 6) Correlation & Regression
| Pair | Correlation | Note |
|------|-------------|------|
| Engine_Size_L ↔ Price | ~0.0001 | None |
| Mileage_KM ↔ Price | ~-0.004 | None |
| Year ↔ Price | ~0.0035 | None |
| Sales_Volume ↔ Price | ~0.00008 | None |

**Simple Linear Regression (Price ~ Engine_Size_L)**  
- Intercept (β₀): **≈ 75,022**  
- Slope (β₁): **≈ 3.76** (≈ $3.76 per 1L; negligible)  
- R²: **≈ 0.0** → No explanatory power.

**Interpretation:** Numeric specs don’t drive price in this dataset; **brand/market attributes** likely do.

## 7) Business Insights
1. **Pricing is not spec-driven** here → positioning and market segment likely dominate.
2. **Region & Transmission** show practical differences → use for portfolio/product packaging.
3. **Clean dataset** enables rapid modeling/dashboards without heavy prep.

## 8) Limitations
- Likely standardized/synthetic generation → real-world noise is muted.
- No cost, incentive, dealer, or trim-level detail → limits granular pricing drivers.

## 9) Next Steps
- Encode categorical features (one-hot) and run **multivariate regression** to quantify drivers.
- **Feature importance** (tree-based models) to rank Model / Region / Fuel_Type effects.
- Build a small **dashboard**: average price by model/region; filter by transmission/fuel.
- Perform **time-based analysis** if true dates are available.

---

### 10) Reproducibility
- Notebook: `analysis.ipynb`  
- Plots used: `images/price_hist.png`, `images/corr_heatmap.png`, `images/mileage_vs_price.png`  
- Python 3.13; Libraries: pandas, matplotlib, scikit-learn, numpy
