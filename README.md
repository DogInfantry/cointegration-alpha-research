# cointegration-alpha-research
# 🦅 Beta-Neutral Statistical Arbitrage Engine

![Python](https://img.shields.io/badge/Python-3.10-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Strategy](https://img.shields.io/badge/Strategy-Pairs%20Trading-006400?style=for-the-badge&logo=finance)
![Math](https://img.shields.io/badge/Math-Cointegration%20(ADF)-orange?style=for-the-badge)
![ML](https://img.shields.io/badge/AI-Random%20Forest-blueviolet?style=for-the-badge&logo=scikitlearn&logoColor=white)
![Scale](https://img.shields.io/badge/Scale-Dask%20Parallelism-blue?style=for-the-badge&logo=dask&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-lightgrey?style=for-the-badge)

---

## 📊 Executive Summary
This repository contains an institutional-grade **Quantitative Research Framework** designed to identify, test, and execute **Statistical Arbitrage (StatArb)** strategies. 

Unlike standard correlation-based pairs trading, this engine utilizes **Cointegration (Engle-Granger Two-Step Method)** to identify stationary time-series relationships. It implements **Dynamic Beta Hedging** using OLS Regression to neutralize market risk and integrates a **Machine Learning (Random Forest)** layer to filter signal noise, ensuring trade execution occurs only during high-probability mean-reversion regimes.

> **Key Edge:** Isolates idiosyncratic alpha from broad market volatility (Beta $\approx$ 0), creating a return stream uncorrelated with the S&P 500.

---

## 🏗️ Technical Architecture

### 1. Data Pipeline & Scalability
* **Ingestion:** Fetches high-frequency (Hourly) OHLCV data via `yfinance`.
* **Microstructure Handling:** Implements `ffill`/`bfill` imputation to handle missing ticks and execution gaps.
* **Parallel Computing:** Built on **Dask** to demonstrate horizontal scalability, allowing the engine to process broad-market universes (Russell 3000) without memory bottlenecks.

### 2. The Alpha Engine (Math & Stats)
* **Stationarity Testing:** Utilizes the **Augmented Dickey-Fuller (ADF)** test from `statsmodels` to validate the cointegration vector ($p < 0.05$).
* **Hedge Ratio Optimization:** Calculates the rolling Ordinary Least Squares (OLS) beta to dynamically adjust position sizing.
    * *Formula:* $Spread_t = Price^A_t - (\beta \times Price^B_t)$
* **Signal Generation:** Computes rolling Z-Scores to normalize spread divergence, entering trades at $\pm 2.0\sigma$ (Bollinger Band logic).

### 3. Machine Learning Risk Filter
* **Model:** Random Forest Classifier (`scikit-learn`).
* **Feature Engineering:**
    * *Spread Volatility (10-period rolling std)*
    * *Market Velocity (Momentum)*
    * *Z-Score Extremes*
* **Function:** Acts as a "Regime Filter" to reject mean-reversion signals during momentum breakouts, significantly reducing Max Drawdown.

---

## 📈 Performance & Tearsheet
The strategy performance is evaluated using institutional risk metrics, accounting for **10bps transaction costs** to simulate real-world execution friction.

| Metric | Value | Description |
| :--- | :--- | :--- |
| **Strategy Type** | Mean Reversion | High-frequency StatArb |
| **Hedge Ratio** | **1.60** | Dynamic OLS Beta (Long AMD / Short NVDA) |
| **Sharpe Ratio** | *Dynamic* | Risk-adjusted return unit |
| **Max Drawdown** | *Dynamic* | Peak-to-valley loss intensity |
| **Signal Precision** | **> 60%** | ML-filtered entry accuracy |

*(Note: Detailed performance graphs and equity curves can be found in the `outputs/` directory.)*

---

## 📂 Repository Structure

```bash
├── 📁 src/                # Source code for the engine
│   ├── data_loader.py     # Dask/Pandas ingestion pipelines
│   ├── statarb_core.py    # ADF tests and Cointegration logic
│   └── ml_filter.py       # Scikit-Learn Random Forest implementation
├── 📁 notebooks/          # Jupyter Notebooks for research & visualization
│   └── Strategy_Walkthrough.ipynb
├── 📁 outputs/            # Generated Tearsheets, Equity Curves, and Z-Score Plots
├── .gitignore             # Financial data exclusion rules
├── requirements.txt       # Production dependencies
└── README.md              # Documentation
