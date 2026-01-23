# FX Expense Timing – ML Decision Support System (EUR → INR)

## Overview
This project builds a machine learning–based decision-support system to help determine the optimal timing for euro-denominated expenses when payments are ultimately debited from an Indian (INR) account.

Using historical EUR → INR exchange rates, the system forecasts short-term currency movements and provides a simple, interpretable recommendation:
**“Spend now” or “Wait 7 days.”**

The goal is not currency trading, but practical expense timing for everyday and planned expenditures.

---

## Problem Statement
Individuals paying in foreign currencies often face uncertainty due to exchange rate fluctuations and hidden charges such as:
- Forex markup fees
- GST on forex transactions

This project addresses the question:
> *Is it better to spend today or wait a few days to reduce total INR outflow?*

---

## Data Source
- **Frankfurter Exchange Rate API**
- Daily EUR → INR exchange rates
- Time range used: **Jan 2023 – Present**

---

## Methodology

### 1. Data Collection
- Historical exchange rates fetched via public API
- Stored and processed as a daily time series

### 2. Preprocessing
- Missing dates handled using forward-fill
- Continuous daily index created
- Train/test split respecting time order

### 3. Forecasting Model
- **Facebook Prophet** for time-series forecasting
- Yearly seasonality enabled
- Short-term trend flexibility tuned via `changepoint_prior_scale`
- Model optimized for short-horizon stability rather than long-term prediction

### 4. Model Evaluation
- Metrics used:
  - Mean Absolute Error (MAE)
  - Root Mean Squared Error (RMSE)
- Final performance:
  - **MAE ≈ 0.9 INR**
  - **RMSE ≈ 1.1 INR**

### 5. Recommendation Logic - Aids decision-making
- Forecasted rates combined with:
  - Forex markup fees
  - GST
- Noise-aware decision thresholds applied
- Output reduced to a clear recommendation:
  - *Spend now*
  - *Wait 7 days*
- Example output:
  > “I think you should spend now — the euro is likely to strengthen.”

---

## Key Design Decisions
- Focused on **decision quality**, not trading accuracy
- Limited training data to recent years to avoid regime shifts
- Prioritized interpretability and robustness over model complexity

---

## Tools & Technologies
- Python
- Pandas, NumPy
- Prophet
- Matplotlib
- Google Colab

---

## Limitations
- Exchange rates are inherently noisy and influenced by external macroeconomic events
- The model is intended as a decision-support tool, not a trading system

---

## Future Enhancements
- Streamlit web app
- Automated daily retraining
- Notifications for favorable spending windows
- Support for additional currencies

---

## Author
Nitin Umesh
