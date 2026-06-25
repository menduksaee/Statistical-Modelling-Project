A rigorous econometric regression analysis estimating continuous scalar residential property valuations ($y\in\mathbb{R}^{n}$) from the Ames Housing dataset within the General Linear Model framework.
---

```markdown
# Statistical Modelling of Residential Property Valuation 🏡📈

> A rigorous econometric linear regression pipeline estimating continuous residential property valuations from the Ames Housing dataset.

---

## 📌 Executive Summary
Predicting residential property transaction prices serves as a foundational benchmark for evaluating classic linear econometric estimation methodologies. This project implements an end-to-end econometric pipeline covering missing value imputation, quantile-stratified partitioning, logarithmic target compression, geometric multicollinearity pruning via Variance Inflation Factors (VIF), and Ordinary Least Squares (OLS) estimation. 

The underlying model is built upon the classical Gauss-Markov linear specification:

y = X * beta + error

```

Where **y** represents the observed transaction response vector, **X** is the regressor design matrix, **beta** is the vector of unknown population parameters, and **error** represents spherical random disturbances with zero conditional mean and constant variance.

---

## 🚀 Key Performance & Diagnostic Results

| Metric / Diagnostic | Comprehensive OLS Model | Pruned Significant Model (p < 0.05) | Statistical Takeaway |
| --- | --- | --- | --- |
| **Degrees of Freedom** | 152 | 45 | Aggressive noise and dimension reduction |
| **R-squared** | 0.920 | 0.902 | Minimal explanatory penalty after pruning |
| **Joint F-Statistic** | 65.47 | 200.5 (p = 0.00) | Massive surge in overall model significance |
| **Condition Number** | 2.42 * 10^7 | 2.83 * 10^5 | Vastly superior matrix algebraic stability |

### Top Discovered Economic Drivers

* **Value Surges (+):** `OverallQual` (t = 13.48) and `GarageCars` (t = 9.35) act as the primary positive price drivers. `TotalBsmtSF` (t = 4.70) also provides a consistent linear valuation lift.
* **Value Discounts (-):** Townhouse building typologies (`BldgType_Twnhs`) and above-ground kitchen counts (`KitchenAbvGr`) firmly impose negative constraints on property transaction prices.

---

## 🛠️ Systematic Methodology Pipeline

1. **Data Ingestion & L1 Imputation:** Loaded 1460 raw observations via OpenML spanning 24 numerical and 43 categorical features. Severe numerical gaps (e.g., LotFrontage) were resolved using sample median imputation. This median substitution minimizes L1 absolute error loss and protects against extreme outliers. Categorical missing data was mapped to a dedicated `"Missing"` level to preserve structural information.
2. **Quantile Stratification:** Discretized the continuous target variable into 10 equal-probability quantiles. Proportional stratified sampling was executed to lock in a stable **70% training (n = 1022)**, **15% validation (n = 219)**, and **15% test (n = 219)** partition without data distribution shifts.
3. **Distributional Tail Compression:** Empirical analysis flagged severe right-skewness in raw sale prices (skewness = 1.965). Applying a natural logarithmic transformation (`log1p`) compressed target skewness to a stable **0.254**, aligning the target variable with OLS normality assumptions.
4. **Geometric VIF Pruning:** Transformed categorical columns into orthogonal binary indicators via dummy encoding, expanding the feature space to 262 columns. An iterative Variance Inflation Factor (**VIF**) routine recursively eliminated predictors scoring >= 10 to eliminate severe multicollinearity and guarantee a full-rank design matrix.
5. **OLS Optimization:** Solved the closed-form normal equations using `statsmodels.api`. Model interpretability was maximized by extracting t-test p-values and strictly filtering out regressors failing the significance threshold of p > 0.05.

---

## 🔬 Gauss-Markov Residual Diagnostics

* **Heteroscedasticity Analysis:** Plotted residuals against fitted values revealed a slight non-constant funneling spread. Formal execution of the Breusch-Pagan Lagrange Multiplier test rejected homoscedasticity (p approximately 0). While OLS estimators remain unbiased, standard errors lose efficiency, pointing toward regularized methods (Ridge/LASSO) or robust standard errors for future iterations.
* **Cross-Sectional Stationarity:** Autocorrelation Function (ACF) plots exhibited immediate drop-offs beyond lag 0. This confirmed the complete absence of sequential lag dependence, verifying that time-series architectures (like ARIMA) are unneeded for this cross-sectional dataset.

---

## 📁 Repository Structure

```text
├── dataset/
│   └── ames_housing.csv          # Raw data ingestion pool
├── notebooks/
│   └── RTSM_Project.ipynb        # Core executable pipeline & EDA
├── reports/
│   ├── RTSM_Project_Report.pdf   # Complete academic econometric derivations
│   └── Solution_Description.pdf  # Executive architecture overview
└── README.md                     # Project documentation

```

---

## 💻 Quickstart (Local Execution)

```bash
# Clone the repository
git clone [https://github.com/yourusername/residential-property-valuation.git](https://github.com/yourusername/residential-property-valuation.git)
cd residential-property-valuation

# Install required statistical dependencies
pip install numpy pandas scipy statsmodels scikit-learn matplotlib seaborn

# Launch the interactive analysis notebook
jupyter notebook notebooks/RTSM_Project.ipynb

```

```

```
