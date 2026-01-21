# Week 3: Time Series Analysis for Finance

## Overview
Time series analysis is fundamental to quantitative finance. This week covers stationarity, autocorrelation, ARMA/ARIMA models, volatility modeling (GARCH), and cointegration.

---

## Day 1: Stationarity and Unit Root Tests
- **Stationarity**: Mean, variance, autocorrelation constant over time
- **Types**: Strict vs Weak (covariance) stationarity
- **Unit Root Tests**: ADF, KPSS, Phillips-Perron
- **Transformations**: Differencing, log returns

## Day 2: Autocorrelation and Partial Autocorrelation
- **ACF**: Correlation at different lags
- **PACF**: Direct correlation controlling for intermediate lags
- **Ljung-Box Test**: Testing for significant autocorrelation
- **Applications**: Return predictability, mean reversion signals

## Day 3: ARMA Models
- **AR(p)**: Autoregressive models
- **MA(q)**: Moving average models
- **ARMA(p,q)**: Combined models
- **Model Selection**: AIC, BIC criteria

## Day 4: ARIMA and Forecasting
- **ARIMA(p,d,q)**: Integrated models for non-stationary data
- **Forecasting**: Point forecasts and confidence intervals
- **Walk-Forward Validation**: Out-of-sample testing
- **Applications**: Price/spread forecasting

## Day 5: Volatility Modeling (ARCH/GARCH)
- **Volatility Clustering**: Why constant variance fails
- **ARCH(q)**: Autoregressive Conditional Heteroskedasticity
- **GARCH(p,q)**: Generalized ARCH
- **Extensions**: EGARCH, GJR-GARCH

## Day 6: Cointegration
- **Spurious Regression**: Why levels correlations can mislead
- **Cointegration**: Long-run equilibrium relationships
- **Engle-Granger**: Two-step method
- **Johansen Test**: Multivariate cointegration
- **Pairs Trading**: Statistical arbitrage application

## Day 7: Interview Questions & Review
- Common time series interview problems
- Practical coding challenges
- Week 3 concept review

---

## Key Formulas

### Stationarity Conditions
**Weak Stationarity:**
- E[Xₜ] = μ (constant mean)
- Var(Xₜ) = σ² (constant variance)
- Cov(Xₜ, Xₜ₊ₖ) = γₖ (depends only on lag k)

### ARMA Models
**AR(1):** Xₜ = φXₜ₋₁ + εₜ
**MA(1):** Xₜ = εₜ + θεₜ₋₁
**ARMA(1,1):** Xₜ = φXₜ₋₁ + εₜ + θεₜ₋₁

### GARCH(1,1)
σₜ² = ω + αεₜ₋₁² + βσₜ₋₁²

### Cointegration
If X ~ I(1) and Y ~ I(1), but Y - βX ~ I(0), then X and Y are cointegrated.

---

## Python Libraries
- `statsmodels`: ARIMA, GARCH, unit root tests
- `arch`: Advanced GARCH models
- `pandas`: Time series manipulation
- `scipy`: Statistical tests
