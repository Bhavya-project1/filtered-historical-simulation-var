# Filtered Historical Simulation for Portfolio Value at Risk

A quantitative risk-modelling notebook that combines conditional-volatility models with historical standardised shocks to estimate portfolio Value at Risk (VaR).

The workflow models the conditional variance of a three-stock financial-sector portfolio, standardises historical residuals, rescales those shocks using the forecast volatility, and calculates loss quantiles at multiple confidence levels.

## Portfolio and Data

- Constituents: Goldman Sachs (GS), JPMorgan Chase (JPM), Morgan Stanley (MS)
- Weights: 40%, 30%, 30%, respectively
- Initial portfolio value: $1,000,000
- Historical sample used in the first model comparisons: 2020-01-01 to 2026-08-10 (end date exclusive)
- Observations in the cached output: 1,657 daily return observations

The notebook downloads auto-adjusted closing prices using yfinance.

## Models Compared

- GARCH(1,1) with normal innovations
- GARCH(1,1) with Student's t innovations
- GJR-GARCH(1,1) with Student's t innovations
- EGARCH with Student's t innovations
- EWMA-based historical VaR

The FHS-style scenario construction is based on:

~~~text
r_(t+1) = μ + σ_(t+1) z_t
~~~

where z_t denotes a historical standardised residual and σ_(t+1) is the one-step-ahead conditional-volatility forecast.

## Cached Example Results

The notebook retains the following VaR outputs for the first three GARCH specifications. Amounts are dollar losses on the assumed $1,000,000 portfolio.

| Specification | 90% VaR | 95% VaR | 99% VaR |
|---|---:|---:|---:|
| GARCH(1,1), normal | $18,965.22 | $25,639.89 | $41,972.32 |
| GARCH(1,1), Student's t | $19,653.65 | $26,314.20 | $43,442.72 |
| GJR-GARCH(1,1), Student's t | $21,503.60 | $29,173.07 | $45,617.40 |

These are cached notebook outputs, not current risk estimates. They correspond to the historical data and assumptions recorded in the notebook. Re-running the notebook may produce different values as Yahoo Finance data and model fits change.

## Repository Contents

- GARCH • GJR-GARCH • EGARCH • EWMA.ipynb — volatility estimation and VaR scenarios.
- Results of VaR + GARCH Models.xlsx — supporting spreadsheet of results.

## Technology

Python · NumPy · pandas · yfinance · arch · Jupyter Notebook · Excel

## Run

~~~bash
pip install -r requirements.txt
jupyter notebook
~~~

Open the notebook and execute cells in order. The Excel workbook can be opened separately in Microsoft Excel.

## Risk Evaluation and Limitations

The model should be extended with formal VaR backtesting (for example, unconditional-coverage and independence tests), Expected Shortfall, stress scenarios, parameter stability checks, and rolling out-of-sample evaluation. The current FHS implementation uses empirical standardised shocks and is sensitive to the sample window and volatility specification. The exact forecast horizon is one trading day.

## Disclaimer

Educational quantitative-risk research only. VaR is model-dependent and does not bound the worst possible loss. Not investment advice.
