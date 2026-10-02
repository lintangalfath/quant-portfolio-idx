# Quantitative Finance Portfolio: Indonesian Equity Market (IDX)

An end-to-end quantitative workflow built on Indonesia Stock Exchange (IDX) data, across five connected projects. Each project answers one question in the investment process, moving from **static to dynamic** and from **descriptive to predictive** analysis.

```
 Screening  →  Allocation  →  Risk Measurement  →  Strategy Testing  →  Forecasting
  (IDX30)     (IDXBUMN20)         (LQ45)               (LQ45)              (JII)
```

| # | Project | Question | Core methods | Headline result |
|---|---|---|---|---|
| 1 | [IDX30 Momentum & Risk Screener](01-idx30-momentum-risk-screener/) | Which stocks deserve attention? | Multi-factor composite score, percentile ranking, sensitivity analysis | AADI, INDF, ADRO stay in the top 5 under all 4 weighting schemes |
| 2 | [IDXBUMN20 Portfolio Optimizer](02-idxbumn20-portfolio-optimizer/) | How should capital be allocated? | Markowitz MPT, Monte Carlo (10,000 portfolios), SLSQP optimization | Optimizer Sharpe 1.14 vs 0.20 from random sampling |
| 3 | [LQ45 Risk Management Dashboard](03-lq45-risk-management-dashboard/) | How much can the portfolio lose? | CAPM beta, Monte Carlo VaR/CVaR, Kupiec backtest, beta-neutral hedging | Hedging cut simulated VaR 95% by ~61% |
| 4 | [LQ45 Systematic Backtesting Engine](04-lq45-systematic-backtesting-engine/) | Does an active trading rule hold up out-of-sample? | MA crossover, walk-forward validation, grid search, transaction costs | Train Sharpe 2.32 → test Sharpe −1.05: overfitting detected |
| 5 | [JII Time Series Forecasting](05-jii-time-series-forecasting/) | Can return and volatility be predicted? | ARIMA, GARCH / GJR-GARCH-t, Random Forest, QLIKE, Diebold-Mariano, dynamic VaR | Returns unpredictable; GJR-GARCH-t VaR is the only method passing all backtests |

## How the projects connect

- **1 → 2**: the screener narrows the universe; the optimizer decides the weights.
- **2 → 3**: once weights exist, the next question is tail risk (VaR/CVaR) and how to hedge market exposure.
- **3 → 4**: Project 4 reuses the same 44-stock LQ45 universe and data window as Project 3.
- **4 → 5**: Project 5 applies the same walk-forward framework from Project 4 to every forecast.
- **5 → 3**: the GARCH-based dynamic VaR in Project 5 fixes the clustered VaR breaches found in Project 3.

## Tech stack

Python · pandas · NumPy · SciPy · statsmodels · arch · scikit-learn · matplotlib · seaborn · yfinance

## Repository structure

```
quant-portfolio-idx/
├── README.md
├── requirements.txt
├── 01-idx30-momentum-risk-screener/
├── 02-idxbumn20-portfolio-optimizer/
├── 03-lq45-risk-management-dashboard/
├── 04-lq45-systematic-backtesting-engine/
└── 05-jii-time-series-forecasting/
```

Each folder contains one self-contained notebook, a README with the key findings, and the charts used in it.

## Running the notebooks

```bash
git clone https://github.com/lintangalfath/quant-portfolio-idx.git
cd quant-portfolio-idx
pip install -r requirements.txt
jupyter notebook
```

Data is downloaded live from Yahoo Finance through `yfinance`, so re-running a notebook on a later date can give slightly different numbers than the saved outputs.

## Notes

- Notebook explanations are written in Bahasa Indonesia; the READMEs are in English.
- All analysis is for educational and research purposes and is not investment advice.

## Author

**Lintang Gilardino Alfathoni** · Data Science undergraduate, Universitas Airlangga
