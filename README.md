
# 🛒 Walmart Sales Forecasting

## 📌 Overview

Retail sales are highly seasonal, and missing peak or low-demand periods can cost millions. In this project, we forecast **Walmart’s weekly sales** using historical data from multiple sources (sales, stores, features).

By building **time-aware regression models** with **calendar, lag, and rolling features**, and applying advanced **boosting algorithms (XGBoost & LightGBM)**, we achieved highly accurate forecasts. These insights help Walmart improve **inventory management, revenue planning, promotions, and investor confidence**.

---

## 📂 Dataset

Source: [Kaggle – Walmart Sales Forecasting](https://www.kaggle.com/c/walmart-recruiting-store-sales-forecasting)

- **train.csv** → `Store`, `Dept`, `Date`, `Weekly_Sales`, `IsHoliday`
- **test.csv** → same as train but without `Weekly_Sales`
- **stores.csv** → store `Type` (A/B/C), `Size`
- **features.csv** → `Temperature`, `Fuel_Price`, `CPI`, `Unemployment`, `MarkDowns`, `IsHoliday`

---

## ⚙️ Workflow

### 1. Data Preparation

- Converted `Date` → datetime, sorted by `Store–Dept–Date`
- Merged `stores.csv` & `features.csv` into train/test
- Handled missing values:
  - `MarkDowns` → filled with 0
  - `Temperature`, `Fuel_Price`, `CPI`, `Unemployment` → forward/back fill per store, then median
- Added calendar features: `Year`, `Month`, `Week`, `DayOfWeek`, `MonthStart`, `MonthEnd`

### 2. Exploratory Data Analysis (EDA)

- **Total Weekly Sales** → yearly spikes in December & holiday weeks
- **Holiday vs Non-Holiday** → clear positive outliers during holidays
- **Store Types** → Type A stores (largest) consistently sell more
- **Correlation Heatmap** → store `Size` matters more than macro variables
- **Monthly Trends** → December peak, January slump

### 3. Feature Engineering

- Lag features: `Weekly_Sales_lag1`, `lag2`, `lag52`
- Rolling averages: `roll4`, `roll12`, `roll52`
- One-hot encoding: store `Type` (A/B/C)

### 4. Time-Aware Validation

- Train: first 90% of timeline
- Validation: last 10% (future simulation)

### 5. Modeling

- **Baseline:** Linear Regression (underfit, missed holiday spikes)
- **Advanced:**
  - XGBoost → RMSE: **2710.62**, MAE: **1290.72**, R²: **0.985**
  - LightGBM → RMSE: **2719.74**, MAE: **1281.75**, R²: **0.985**
- **Ensemble (weighted average)** → most stable predictions

### 6. Visualization & Diagnostics

- Actual vs Predicted (aggregate + Store–Dept level)
- Residual distributions centered near 0
- Seasonal decomposition → trend growth + annual holiday peaks

---

## 📊 Results

- **R² ≈ 0.985** → models explain ~98.5% of variance
- Captured **holiday/seasonal spikes** and **store differences**
- Boosting models far outperformed linear baseline
- **Business Benefits:**
  - Accurate demand forecasting → **better inventory planning**
  - Predictable revenue → **improved financial projections**
  - Anticipating peaks/slumps → **optimized promotions & campaigns**
  - Confidence in hitting sales targets → **positive investor sentiment**

## 📌 Conclusion

Our advanced models (XGBoost & LightGBM) achieved **highly accurate forecasts (R² ≈ 0.985)**, far surpassing simple baselines. They successfully captured **seasonality, holiday spikes, and store heterogeneity**, providing Walmart with actionable insights to:

- **Manage inventory more effectively**
- **Improve revenue forecasting**
- **Plan promotions & campaigns around demand peaks**
- **Boost investor confidence through reliable target achievement**

This approach demonstrates how **data-driven forecasting** can directly enhance retail decision-making and financial outcomes.
