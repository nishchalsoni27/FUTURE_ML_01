# 📈 Sales & Demand Forecasting for Businesses
### Task 01 — Machine Learning Project
**Author:** Nishchal Soni | **Theme:** Into the Wild (Dark) | **Type:** Offline-Ready HTML

---

## 🗺️ Overview

A fully self-contained, single-file web application for **Sales & Demand Forecasting** built as a Machine Learning project showcase. No internet connection required — open the HTML file directly in any modern browser and everything works.

The project demonstrates a complete ML forecasting pipeline with a **live interactive demo** that runs three real forecasting algorithms in the browser using vanilla JavaScript.

---

## 📂 Project Files

```
📁 project/
├── sales_forecasting_nishchal.html   ← Main project page (open this)
├── DEMO_TEST.html                    ← Demo & algorithm test suite
└── README.md                         ← This file
```

---

## 🚀 Quick Start

### Run Locally (Offline)
```bash
# No installation needed — just double-click the file, or:
open sales_forecasting_nishchal.html          # macOS
start sales_forecasting_nishchal.html         # Windows
xdg-open sales_forecasting_nishchal.html      # Linux
```

### Run via Local Server (optional, for development)
```bash
# Python 3
python -m http.server 8080
# then visit http://localhost:8080/sales_forecasting_nishchal.html

# Node.js
npx serve .
```

> ✅ No Node.js, Python, or any dependency required for normal use.  
> ✅ No CDN, no Google Fonts, no external scripts — 100% offline.

---

## 🤖 ML Algorithms Implemented

All three algorithms are implemented from scratch in vanilla JavaScript:

### 1. Simple Moving Average (SMA)
Averages the last `w` observations to predict the next value.

```
Forecast(t+1) = (y(t) + y(t-1) + ... + y(t-w+1)) / w
```
- **Best for:** Stable markets, short-term forecasting
- **Window:** Last 6 months by default

### 2. Exponential Smoothing (ETS)
Assigns exponentially decreasing weights to older observations.

```
S(t) = α × y(t) + (1 - α) × S(t-1)     [α = 0.3]
```
- **Best for:** Smooth demand with gradual trends
- **Parameter:** Smoothing factor α (0 = slow adaptation, 1 = fast)

### 3. Linear Regression
Fits a least-squares line through historical data and extrapolates.

```
ŷ = β₀ + β₁ × t
β₁ = Σ(t - t̄)(y - ȳ) / Σ(t - t̄)²
```
- **Best for:** Data with a strong consistent upward/downward trend

---

## 📊 Dataset Patterns (Demo Modes)

| Pattern | Description | Use Case |
|---------|-------------|----------|
| **Seasonal Business** | Trend + sinusoidal seasonality | Retail, e-commerce |
| **Upward Trend** | Linear growth with noise | Startups, SaaS growth |
| **Volatile Demand** | High variance, irregular spikes | FMCG, perishables |
| **Stable Market** | Near-flat with minor fluctuation | B2B SaaS, utilities |

---

## 📐 Evaluation Metrics

| Metric | Formula | Interpretation |
|--------|---------|----------------|
| **MAE** | mean(\|actual - predicted\|) | Average error in original units |
| **RMSE** | √mean((actual - predicted)²) | Penalises large errors more |
| **MAPE** | mean(\|error/actual\|) × 100 | % error — scale independent |
| **R²** | 1 - SS_res / SS_tot | 1.0 = perfect fit; >0.85 = excellent |

> 💡 **Industry benchmark:** MAPE < 10% is considered excellent for demand forecasting.

Metrics are computed on a **held-out validation set** (last 6 months of historical data not seen during fitting).

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Structure | HTML5 |
| Styling | CSS3 (custom properties, grid, animations) |
| Charts | HTML5 Canvas API (vanilla JS) |
| ML Engine | Vanilla JavaScript |
| Fonts | System fonts (Palatino, Georgia, Courier New) |
| Dependencies | **None** |

---

## 🌿 Features

- **Live Forecasting Demo** — run any of 3 algorithms on 4 dataset types
- **Interactive Canvas Chart** — historical line, dashed forecast, 90% confidence bands
- **Compare All Models** — overlay SMA, ETS, and Linear Regression on one chart
- **Real Metrics** — MAE, RMSE, MAPE, R² computed on validation split
- **Adjustable Parameters** — forecast horizon (3–12 months), noise level (Low/Med/High)
- **ML Pipeline Diagram** — 6-step animated pipeline visual
- **How to Explain Section** — structured talking points for viva, interviews, presentations
- **Scroll animations** — intersection-observer-driven reveal effects
- **Progress bar + nav dots** — compass-themed navigation
- **Into the Wild dark theme** — forest silhouette, starfield, grain overlay, amber palette
- **Fully offline** — zero network requests after file load

---

## 📋 ML Pipeline (As Implemented)

```
Raw Data  →  Clean & Preprocess  →  Feature Engineering
    →  Train Model  →  Evaluate & Tune  →  Forecast & Deploy
```

### Step-by-step (real Python equivalent):
```python
# 1. Load & Clean
import pandas as pd
df = pd.read_csv('sales_data.csv', parse_dates=['date'])
df = df.dropna().sort_values('date')

# 2. Feature Engineering
df['lag_1']  = df['sales'].shift(1)
df['lag_3']  = df['sales'].shift(3)
df['lag_12'] = df['sales'].shift(12)
df['roll_3'] = df['sales'].rolling(3).mean()
df['month']  = df['date'].dt.month
df['quarter']= df['date'].dt.quarter

# 3. Train/Test Split (time-aware — never shuffle!)
train = df.iloc[:-6]
test  = df.iloc[-6:]

# 4. Model (XGBoost example)
from xgboost import XGBRegressor
features = ['lag_1','lag_3','lag_12','roll_3','month','quarter']
model = XGBRegressor(n_estimators=200, learning_rate=0.05)
model.fit(train[features], train['sales'])

# 5. Evaluate
from sklearn.metrics import mean_absolute_error, mean_squared_error
import numpy as np
pred = model.predict(test[features])
mae  = mean_absolute_error(test['sales'], pred)
rmse = np.sqrt(mean_squared_error(test['sales'], pred))
mape = np.mean(np.abs((test['sales'] - pred) / test['sales'])) * 100

# 6. Forecast future
future_pred = model.predict(future_features)
```

---

## 🎯 How to Present This Project

### 30-Second Elevator Pitch
> *"I built a Machine Learning model that forecasts future sales or demand for a business from its historical data. The core problem is that businesses can't see ahead — they over-stock or under-stock. My model learns seasonal patterns, trends, and cycles from past data and projects 3–12 months forward with confidence intervals. I evaluated it using MAPE, achieving under 10% error on validation data."*

### Key Talking Points
1. **Problem** — inventory waste, stockouts, poor planning from manual guesswork
2. **Data** — historical monthly/weekly sales, feature-engineered with lags and seasonality
3. **Model** — chose [your model] because [1 sentence reason]
4. **Results** — MAPE of X%, R² of Y, outperformed baseline by Z%
5. **Business Value** — 20–30% inventory cost reduction, better cash flow forecasting

### Likely Interview Questions
| Question | Key Answer |
|----------|-----------|
| Why time-series, not regular regression? | Temporal dependency — past values influence future |
| How did you handle seasonality? | STL decomposition / SARIMA seasonal term / month dummies |
| How did you validate? | Walk-forward cross-validation — never shuffle split |
| What's MAPE vs RMSE? | MAPE is %-based (scale-free); RMSE penalises large errors |
| How would you improve this? | LSTM for long-range, add external regressors (weather, promotions) |

---

## 📸 Sections in the HTML

| Section | What It Shows |
|---------|--------------|
| Hero | Into the Wild title screen with stars + forest silhouette |
| Mission | Task overview, metadata, 4 key feature cards |
| ML Pipeline | 6-step animated pipeline + skills bars + tools badges |
| Live ML Demo | Interactive canvas chart + 3 algorithms + real metrics |
| How to Explain | 6 accordion cards for presentation prep |
| Deliverable | Summary of project outputs |

---

## 🌲 Design Credits

- **Theme:** Into the Wild (2007 film by Sean Penn) — wilderness, navigation, raw beauty
- **Palette:** Ink black `#0d0b08` · Forest green `#a8c89a` · Sunray amber `#e8b84b` · Cream `#f2ead8`
- **Typography:** Palatino Linotype (display) · Courier New (body) · Georgia (labels)
- **Effects:** CSS grain overlay · SVG starfield · Forest silhouette · Compass rose · Scroll animations

---

## 📄 License

This project was created for educational purposes as part of a Data Science / ML coursework assignment.

**Made with 🌿 by Nishchal Soni**

---

*"Into the wilderness of data we go, armed only with curiosity and code."*
