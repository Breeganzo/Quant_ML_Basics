# Week 3: Time Series Analysis for Finance

## Table of Contents
1. [Time Series Fundamentals](#1-time-series-fundamentals)
2. [Stationarity](#2-stationarity)
3. [Autoregressive (AR) Models](#3-autoregressive-ar-models)
4. [Moving Average (MA) Models](#4-moving-average-ma-models)
5. [ARIMA Models](#5-arima-models)
6. [GARCH Models](#6-garch-models)
7. [Cointegration](#7-cointegration)

---

## 1. Time Series Fundamentals

### What is a Time Series?

A time series is a sequence of data points indexed by time:
$$\{X_t\}_{t=1}^{T} = X_1, X_2, ..., X_T$$

**Examples in Finance:**
- Stock prices: $P_1, P_2, ..., P_T$
- Returns: $r_1, r_2, ..., r_T$
- Volatility: $\sigma_1, \sigma_2, ..., \sigma_T$

### Components of Time Series

1. **Trend ($T_t$):** Long-term direction
2. **Seasonality ($S_t$):** Regular periodic patterns
3. **Cycle ($C_t$):** Non-fixed periodic fluctuations
4. **Noise ($\epsilon_t$):** Random variation

$$X_t = T_t + S_t + C_t + \epsilon_t$$ (Additive)

$$X_t = T_t \times S_t \times C_t \times \epsilon_t$$ (Multiplicative)

### Autocorrelation Function (ACF)

Measures correlation between a series and its lagged values.

$$\rho_k = \text{Corr}(X_t, X_{t-k}) = \frac{\text{Cov}(X_t, X_{t-k})}{\text{Var}(X_t)}$$

Where $k$ = number of lags

**Example Calculation:**

For lag-1 autocorrelation:
$$\rho_1 = \frac{\sum_{t=2}^{T}(X_t - \bar{X})(X_{t-1} - \bar{X})}{\sum_{t=1}^{T}(X_t - \bar{X})^2}$$

### Partial Autocorrelation Function (PACF)

Measures correlation between $X_t$ and $X_{t-k}$ after removing the effect of intermediate lags.

**Use:** 
- ACF decays slowly → AR process
- PACF cuts off → AR order

---

## 2. Stationarity

### Why Stationarity Matters

Most time series models assume stationarity. Non-stationary data can lead to:
- Spurious regressions
- Invalid statistical tests
- Poor forecasts

### Strict Stationarity

The joint distribution of $(X_{t_1}, X_{t_2}, ..., X_{t_k})$ is the same as $(X_{t_1+h}, X_{t_2+h}, ..., X_{t_k+h})$ for all time shifts $h$.

### Weak (Covariance) Stationarity

A process is weakly stationary if:

1. **Constant Mean:** $E[X_t] = \mu$ for all $t$
2. **Constant Variance:** $\text{Var}(X_t) = \sigma^2$ for all $t$
3. **Covariance depends only on lag:** $\text{Cov}(X_t, X_{t-k}) = \gamma_k$ for all $t$

### Testing for Stationarity

#### Augmented Dickey-Fuller (ADF) Test

Tests for unit root (non-stationarity).

**Hypotheses:**
- $H_0$: Series has unit root (non-stationary)
- $H_1$: Series is stationary

**Test Equation:**
$$\Delta X_t = \alpha + \beta t + \gamma X_{t-1} + \sum_{i=1}^{p} \delta_i \Delta X_{t-i} + \epsilon_t$$

**Test Statistic:**
$$\text{ADF} = \frac{\hat{\gamma}}{SE(\hat{\gamma})}$$

**Decision:** Reject $H_0$ (series is stationary) if ADF statistic < critical value

**Example:**
```
ADF Statistic: -3.45
Critical Values: 1%: -3.43, 5%: -2.86, 10%: -2.57

Since -3.45 < -3.43, reject H₀ at 1% level.
Conclusion: Series is stationary.
```

### Making Series Stationary

1. **Differencing:** $\Delta X_t = X_t - X_{t-1}$
2. **Log Transform:** $\ln(X_t)$
3. **Detrending:** Remove linear trend
4. **Seasonal Differencing:** $X_t - X_{t-s}$

**Example:**
```
Prices: [100, 102, 105, 103, 107]
First Difference: [2, 3, -2, 4]

Prices are non-stationary (trend)
Differences (returns) are stationary
```

---

## 3. Autoregressive (AR) Models

### AR(1) Model

Current value depends on previous value plus noise:

$$X_t = c + \phi X_{t-1} + \epsilon_t$$

Where:
- $c$ = constant
- $\phi$ = autoregressive coefficient
- $\epsilon_t \sim N(0, \sigma^2)$ = white noise

### Stationarity Condition

AR(1) is stationary if $|\phi| < 1$

### AR(1) Properties

**Mean:**
$$E[X_t] = \frac{c}{1 - \phi}$$

**Variance:**
$$\text{Var}(X_t) = \frac{\sigma^2}{1 - \phi^2}$$

**Autocorrelation:**
$$\rho_k = \phi^k$$

### AR(p) Model

$$X_t = c + \phi_1 X_{t-1} + \phi_2 X_{t-2} + ... + \phi_p X_{t-p} + \epsilon_t$$

Or using lag operator $L$ (where $LX_t = X_{t-1}$):

$$\Phi(L)X_t = c + \epsilon_t$$

Where $\Phi(L) = 1 - \phi_1 L - \phi_2 L^2 - ... - \phi_p L^p$

### Example: AR(1) Simulation and Estimation

**Given:** $X_t = 0.5 + 0.7 X_{t-1} + \epsilon_t$ where $\epsilon_t \sim N(0, 1)$

**Properties:**
- Mean: $\mu = 0.5 / (1 - 0.7) = 1.67$
- Lag-1 autocorrelation: $\rho_1 = 0.7$
- Lag-2 autocorrelation: $\rho_2 = 0.7^2 = 0.49$

**To Estimate:** Use OLS regression of $X_t$ on $X_{t-1}$

---

## 4. Moving Average (MA) Models

### MA(1) Model

Current value depends on current and past noise:

$$X_t = \mu + \epsilon_t + \theta \epsilon_{t-1}$$

Where:
- $\mu$ = mean
- $\theta$ = MA coefficient
- $\epsilon_t \sim N(0, \sigma^2)$

### MA(1) Properties

**Mean:**
$$E[X_t] = \mu$$

**Variance:**
$$\text{Var}(X_t) = \sigma^2(1 + \theta^2)$$

**Autocorrelation:**
$$\rho_1 = \frac{\theta}{1 + \theta^2}, \quad \rho_k = 0 \text{ for } k > 1$$

**Key Feature:** MA(q) has ACF that cuts off after lag q.

### MA(q) Model

$$X_t = \mu + \epsilon_t + \theta_1 \epsilon_{t-1} + \theta_2 \epsilon_{t-2} + ... + \theta_q \epsilon_{t-q}$$

Using lag operator:
$$X_t = \mu + \Theta(L)\epsilon_t$$

Where $\Theta(L) = 1 + \theta_1 L + \theta_2 L^2 + ... + \theta_q L^q$

### Invertibility Condition

MA(1) is invertible if $|\theta| < 1$

---

## 5. ARIMA Models

### ARMA(p,q) Model

Combines AR and MA:

$$X_t = c + \sum_{i=1}^{p} \phi_i X_{t-i} + \epsilon_t + \sum_{j=1}^{q} \theta_j \epsilon_{t-j}$$

Or:
$$\Phi(L)X_t = c + \Theta(L)\epsilon_t$$

### ARIMA(p,d,q) Model

ARMA applied to differenced series:

- **p** = AR order
- **d** = Differencing order
- **q** = MA order

$$\Phi(L)(1-L)^d X_t = c + \Theta(L)\epsilon_t$$

### Model Selection: Box-Jenkins Method

**Step 1: Identify**
- Plot ACF and PACF
- Determine stationarity
- Choose p, d, q

**Step 2: Estimate**
- Use MLE or OLS
- Estimate parameters

**Step 3: Diagnose**
- Check residuals (should be white noise)
- ACF of residuals should be insignificant

**Step 4: Forecast**
- Use fitted model for predictions

### ACF/PACF Patterns

| Model | ACF Pattern | PACF Pattern |
|-------|-------------|--------------|
| AR(p) | Decays exponentially | Cuts off after lag p |
| MA(q) | Cuts off after lag q | Decays exponentially |
| ARMA | Decays | Decays |

### Information Criteria

**AIC (Akaike Information Criterion):**
$$AIC = 2k - 2\ln(\hat{L})$$

**BIC (Bayesian Information Criterion):**
$$BIC = k\ln(n) - 2\ln(\hat{L})$$

Where:
- $k$ = number of parameters
- $n$ = sample size
- $\hat{L}$ = maximized likelihood

**Rule:** Lower is better. BIC penalizes complexity more.

### Example: ARIMA(1,1,1) Forecast

**Model:** $(1 - \phi L)(1-L)X_t = (1 + \theta L)\epsilon_t$

**Expanded:** $\Delta X_t = \phi \Delta X_{t-1} + \epsilon_t + \theta \epsilon_{t-1}$

**1-Step Forecast:**
$$\hat{X}_{T+1} = X_T + \hat{\phi}(\Delta X_T) + \hat{\theta}\hat{\epsilon}_T$$

---

## 6. GARCH Models

### Motivation

Stock returns show:
- **Volatility Clustering:** High volatility followed by high volatility
- **Fat Tails:** More extreme returns than normal predicts
- **Mean Reversion:** Volatility returns to long-run average

ARIMA can't capture these. GARCH models conditional variance.

### ARCH(1) Model

$$r_t = \mu + \epsilon_t$$
$$\epsilon_t = \sigma_t z_t, \quad z_t \sim N(0,1)$$
$$\sigma_t^2 = \omega + \alpha \epsilon_{t-1}^2$$

Where:
- $\sigma_t^2$ = conditional variance at time t
- $\omega > 0$ = base variance
- $\alpha \geq 0$ = ARCH coefficient

### GARCH(1,1) Model

Adds lagged variance:

$$\sigma_t^2 = \omega + \alpha \epsilon_{t-1}^2 + \beta \sigma_{t-1}^2$$

Where:
- $\alpha$ = impact of past shocks
- $\beta$ = persistence of variance
- $\alpha + \beta$ = persistence (< 1 for stationarity)

### GARCH Properties

**Unconditional Variance:**
$$E[\sigma_t^2] = \frac{\omega}{1 - \alpha - \beta}$$

**Example:**
```
ω = 0.00001, α = 0.1, β = 0.85

Long-run variance = 0.00001 / (1 - 0.1 - 0.85)
                  = 0.00001 / 0.05
                  = 0.0002

Long-run volatility = √0.0002 = 1.41% (daily)
Annualized = 1.41% × √252 = 22.4%
```

### Volatility Forecasting

**1-Step Ahead:**
$$\hat{\sigma}_{T+1}^2 = \omega + \alpha \epsilon_T^2 + \beta \sigma_T^2$$

**Multi-Step:**
$$\hat{\sigma}_{T+h}^2 = \bar{\sigma}^2 + (\alpha + \beta)^{h-1}(\sigma_{T+1}^2 - \bar{\sigma}^2)$$

Converges to unconditional variance as $h \to \infty$.

### GARCH Extensions

| Model | Feature | Equation Component |
|-------|---------|-------------------|
| **EGARCH** | Asymmetric, no positivity constraint | $\ln(\sigma_t^2)$ |
| **GJR-GARCH** | Leverage effect | $+ \gamma \epsilon_{t-1}^2 I_{[\epsilon_{t-1}<0]}$ |
| **TGARCH** | Threshold effects | Different regimes |

---

## 7. Cointegration

### What is Cointegration?

Two non-stationary series are cointegrated if a linear combination is stationary.

If $X_t \sim I(1)$ and $Y_t \sim I(1)$, they are cointegrated if:
$$Z_t = Y_t - \beta X_t \sim I(0)$$

### Intuition

- Individual series wander (random walk)
- But they move together (common trend)
- Spread between them is stationary

### Example: Pairs Trading

```
Stock A and Stock B are cointegrated with β = 1.2

Spread = Price_A - 1.2 × Price_B

When spread deviates from mean:
- Spread too high → Short A, Long 1.2×B
- Spread too low → Long A, Short 1.2×B

Expect spread to revert to mean.
```

### Testing for Cointegration

#### Engle-Granger Two-Step Method

**Step 1:** Regress Y on X
$$Y_t = \alpha + \beta X_t + \epsilon_t$$

**Step 2:** Test residuals for stationarity (ADF test)

If residuals are stationary → cointegrated

#### Johansen Test

For multiple series, tests number of cointegrating relationships.

### Error Correction Model (ECM)

For cointegrated series, short-run dynamics:

$$\Delta Y_t = \alpha + \gamma(Y_{t-1} - \beta X_{t-1}) + \sum \delta_i \Delta Y_{t-i} + \sum \phi_j \Delta X_{t-j} + \epsilon_t$$

Where:
- $\gamma$ = speed of adjustment (< 0)
- $(Y_{t-1} - \beta X_{t-1})$ = error correction term

---

## Key Formulas Summary

| Concept | Formula |
|---------|---------|
| AR(1) | $X_t = c + \phi X_{t-1} + \epsilon_t$ |
| MA(1) | $X_t = \mu + \epsilon_t + \theta\epsilon_{t-1}$ |
| GARCH(1,1) | $\sigma_t^2 = \omega + \alpha\epsilon_{t-1}^2 + \beta\sigma_{t-1}^2$ |
| Long-run Variance | $\bar{\sigma}^2 = \frac{\omega}{1-\alpha-\beta}$ |
| ACF at lag k | $\rho_k = \frac{\gamma_k}{\gamma_0}$ |
| ADF Test | $\Delta X_t = \alpha + \gamma X_{t-1} + \epsilon_t$ |
| Cointegration | $Y_t - \beta X_t \sim I(0)$ |

---

## Practice Problems

1. Given AR(1) with φ = 0.8, c = 2, σ² = 1:
   - Calculate mean, variance, and ρ₁, ρ₂, ρ₃
   
2. Identify the model from ACF/PACF:
   - ACF: significant at lags 1,2,3... (decaying)
   - PACF: significant only at lag 1, then cuts off

3. A GARCH(1,1) has ω = 0.00002, α = 0.15, β = 0.80:
   - Is it stationary?
   - What is the long-run daily volatility?
   - If today's σ² = 0.0004, forecast tomorrow's variance

4. Two stocks have spread with half-life of 10 days. What is the mean reversion speed?

---

*Next Week: Machine Learning Foundations*
