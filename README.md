# Filtered Historical Simulation for Value at Risk

A quantitative risk-modelling project combining conditional-volatility estimation with a historical simulation approach to estimate portfolio tail risk.

## Repository Contents

- `GARCH • GJR-GARCH • EGARCH • EWMA.ipynb` — volatility modelling notebook.
- `Results of VaR + GARCH Models.xlsx` — spreadsheet of results.

## Methodological Overview

Filtered Historical Simulation (FHS) separates return shocks from time-varying volatility. A typical workflow is:

1. Fit a conditional-volatility model to returns.
2. Standardise historical residuals using estimated conditional volatility.
3. Resample or replay the standardised shocks.
4. Scale shocks by current or forecast conditional volatility.
5. Reconstruct scenario returns and calculate the relevant loss quantile.

The notebook examines GARCH-family and EWMA volatility approaches.

### Volatility Models

- **GARCH:** models conditional variance using past squared shocks and past conditional variance.
- **GJR-GARCH:** introduces an asymmetric response to negative and positive shocks.
- **EGARCH:** models log conditional variance and can capture asymmetric effects.
- **EWMA:** updates variance using exponentially decaying weights on past squared returns.

## Run

```bash
pip install numpy pandas scipy matplotlib statsmodels arch openpyxl jupyter
jupyter notebook
```

Open the notebook and execute the cells in order. Open the Excel workbook separately to inspect reported outputs and calculations.

## Risk Evaluation

FHS can incorporate volatility clustering while retaining an empirical distribution of standardised shocks. Performance depends on the volatility specification, residual quality, sample window, tail observations, and scenario assumptions.

A robust assessment should include VaR backtesting, exception analysis, Expected Shortfall, stress scenarios, and comparison with alternative VaR methods.

## Limitations

The exact portfolio, return frequency, forecast horizon, confidence levels, and implementation choices are defined by the notebook and workbook. Confirm these before interpreting or comparing results.

## Disclaimer

Educational quantitative-risk research only. VaR is a model-based estimate, not a maximum-loss guarantee or investment advice.
