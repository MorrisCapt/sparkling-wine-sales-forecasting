# sparkling-wine-sales-forecasting

Time series analysis and forecasting of monthly Sparkling wine sales for ABC Estate Wines (1980–1995). Built as a full-code data science project covering EDA, decomposition, 8 forecasting models, model comparison, and a 12-month forward forecast.

---

## Overview

ABC Estate Wines needed to understand its historical Sparkling wine sales patterns and produce reliable short-term demand forecasts. This project delivers both — using classical time series methods to extract trend and seasonality signals, then evaluating a comprehensive model suite to select the best-performing approach for operational planning.

**Dataset:** 187 monthly observations | January 1980 – July 1995  
**Target variable:** `Sparkling` — monthly unit sales  
**Forecast horizon:** 12 months forward with 95% confidence intervals

---

## Key Findings

- Sparkling wine sales have grown ~2× over 15 years, driven by a structural upward trend of ~8–10 units per month.
- December consistently generates ~3× the sales of an average month — a textbook multiplicative seasonal pattern tied to Christmas and New Year celebrations.
- The seasonal amplitude grows proportionally with the trend level, confirming a **multiplicative** (not additive) seasonal structure.
- **Holt-Winters Triple Exponential Smoothing** (additive trend + multiplicative seasonality) delivers the best test-set RMSE among all models evaluated.

---

## Models Evaluated

| Model | Type |
|---|---|
| Linear Regression on Time | Trend baseline |
| Naïve Forecast | Benchmark |
| Simple Average | Benchmark |
| Simple Exponential Smoothing (SES) | Level only |
| Double Exponential Smoothing / Holt's | Level + Trend |
| Triple Exponential Smoothing / Holt-Winters | Level + Trend + Seasonality |
| Auto ARIMA (lowest AIC) | Statistically driven |
| Auto SARIMA (lowest AIC) | Seasonal ARIMA |

---

## Repository Structure

```
sparkling-wine-sales-forecasting/
│
├── data/
│   └── Sparkling.csv                  # Raw monthly sales data
│
├── notebooks/
│   └── ABC_Estate_Wines_Sparkling_TSF.ipynb   # Main analysis notebook
│
├── requirements.txt                   # Python dependencies
├── .gitignore                         # Files excluded from version control
└── README.md                          # This file
```

---

## Quickstart

### 1. Clone the repository

```bash
git clone https://github.com/<your-username>/sparkling-wine-sales-forecasting.git
cd sparkling-wine-sales-forecasting
```

### 2. Set up the environment

```bash
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

### 3. Launch the notebook

```bash
jupyter notebook notebooks/ABC_Estate_Wines_Sparkling_TSF.ipynb
```

Run all cells top to bottom. The notebook is fully self-contained.

---

## Notebook Structure

| Section | Contents |
|---|---|
| Problem Statement | Business context and analytical objectives |
| Data Overview | Shape, dtypes, and initial inspection |
| Data Pre-Processing | Datetime indexing, column cleanup |
| Missing Value Check | Completeness verification |
| EDA | Time series plot, year-on-year boxplot, month-of-year seasonality |
| Decomposition | Additive and multiplicative decomposition with Shapiro-Wilk residual tests |
| Data Preparation | Train / test split (1980–1991 train, 1992–1995 test) |
| Model Building | All 8 models with parameter sweeps and RMSE evaluation |
| Stationarity | ADF test, first differencing, ACF / PACF plots |
| Model Comparison | Ranked RMSE table and bar chart |
| Final Forecast | Holt-Winters retrained on full data, 12-month forecast with 95% CI |
| Business Insights | Consultant-level recommendations for procurement, inventory, and strategy |

---

## Requirements

- Python 3.8+
- See `requirements.txt` for the full dependency list

---

## Business Recommendations Summary

1. Adopt Holt-Winters TES as the operational demand planning model, retrained quarterly.
2. Implement a two-tier procurement calendar — ramp up inventory in Sep–Nov, run lean in Apr–Aug.
3. Use the 95% confidence interval upper bound to set safety stock levels for December.
4. Investigate the drivers behind the long-term trend to assess sustainability and growth levers.
5. Monitor model performance monthly (MAPE threshold alert) to detect structural breaks early.

---

## License

MIT License. See `LICENSE` for details.
