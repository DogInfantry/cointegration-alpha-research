# cointegration-alpha-research
This repository contains a comprehensive Jupyter Notebook (DE.ipynb) that explores various quantitative finance techniques, ranging from macroeconomic sector analysis to machine learning-enhanced statistical arbitrage. The project demonstrates the use of Python for financial data ingestion, risk analysis, distributed computing with Dask, and algorithmic trading strategy backtesting.
Features
1. Market Breadth & Sector Analysis
• Data Ingestion: Fetches 5 years of historical data for 11 major US Economy sectors (e.g., Technology XLK, Financials XLF, Energy XLE) and the S&P 500 benchmark (SPY) using yfinance.
• Correlation Mapping: Generates a cross-asset correlation heatmap to identify systemic risk and diversification opportunities.
• Relative Strength (Alpha) Map: Visualizes sector performance relative to the S&P 500 to identify outperforming industries.
2. Trend Following Strategy (SMA Crossover)
• Logic: Implements a classic Moving Average Crossover strategy on NVDA.
• Parameters: Buys when the Short-Term MA (20-day) crosses above the Long-Term MA (50-day).
• Backtesting: Simulates trade execution and compares strategy returns against a "Buy & Hold" benchmark, visualizing the growth of a $1 investment.
3. Distributed Risk Analysis with Dask
• Scalability: Utilizes dask to handle parallel processing for large-scale data operations.
• Volatility Analysis: Calculates 30-day rolling volatility for major tech stocks (NVDA, AAPL, MSFT, etc.) to assess risk relative to the sector average.
4. Statistical Arbitrage & Pairs Trading
• Cointegration Testing: Scans semiconductor stocks (NVDA, AMD, INTC, TSM, etc.) for cointegrated pairs using the Augmented Dickey-Fuller (ADF) test.
• Heatmap Visualization: Plots p-values to identify statistically significant mean-reverting relationships.
5. ML-Enhanced Pairs Trading Strategy
• Hedge Ratio: Calculates the optimal hedge ratio for the NVDA/AMD pair using OLS regression (Formula: Y=βX+α).
• Feature Engineering: Generates signals based on Spread Volatility, Market Volatility, Momentum, and Z-Scores.
• Machine Learning Model: Trains a Random Forest Classifier (sklearn) to filter false trading signals by predicting the probability of Z-Score mean reversion.
• Performance Metrics: Generates a professional "Tearsheet" analyzing Total Return, Annualized Return, Sharpe Ratio, and Maximum Drawdown.
Tech Stack
• Core: Python, Pandas, NumPy
• Data Source: yfinance
• Visualization: Matplotlib, Seaborn
• Big Data/Parallel Computing: Dask
• Statistics & ML: Statsmodels, Scikit-learn
Installation
1. Clone the repository:
2. Install the required dependencies:
3. Launch Jupyter Lab or Notebook:
Usage
Open DE.ipynb and run the cells sequentially. The notebook is structured in steps:
1. Define Horizontal Depth: Set up sector tickers.
2. Get Data: Ingest historical prices.
3. Analyze & Visualize: Run correlation matrices and backtests.
4. ML Layer: Train the Random Forest model and view the strategy tearsheet.
Disclaimer
This project is for educational and research purposes only. The strategies and code provided are not financial advice, and past performance is not indicative of future results.
