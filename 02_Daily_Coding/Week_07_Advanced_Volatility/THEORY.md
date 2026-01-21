# Week 7: Advanced Volatility Modeling

## Table of Contents
1. [Volatility Fundamentals](#1-volatility-fundamentals)
2. [GARCH(1,1) Model](#2-garch11-model)
3. [EGARCH Model](#3-egarch-model)
4. [GJR-GARCH Model](#4-gjr-garch-model)
5. [Multivariate GARCH (DCC)](#5-multivariate-garch-dcc)
6. [Volatility Forecasting](#6-volatility-forecasting)
7. [Volatility Trading Strategies](#7-volatility-trading-strategies)

---

## 1. Volatility Fundamentals

### Types of Volatility

| Type | Definition | Calculation |
|------|------------|-------------|
| **Historical** | Past realized volatility | $\sqrt{\frac{252}{n}\sum r_t^2}$ |
| **Implied** | Market's expectation (from options) | From Black-Scholes inversion |
| **Realized** | Actual volatility over period | High-frequency data |
| **Conditional** | Model-based forecast | GARCH, etc. |

### Stylized Facts of Volatility

1. **Volatility Clustering:** High vol followed by high vol
2. **Mean Reversion:** Volatility returns to long-run average
3. **Asymmetry (Leverage Effect):** Negative returns → Higher vol
4. **Fat Tails:** Returns have excess kurtosis
5. **Long Memory:** Autocorrelation decays slowly

### Why Model Volatility?

- **Risk Management:** VaR, Expected Shortfall
- **Option Pricing:** Volatility is key input
- **Portfolio Allocation:** Dynamic risk budgeting
- **Trading:** Volatility arbitrage

---

## 2. GARCH(1,1) Model

### Model Specification

**Return equation:**
$$r_t = \mu + \epsilon_t$$

**Error term:**
$$\epsilon_t = \sigma_t z_t, \quad z_t \sim N(0,1)$$

**Variance equation:**
$$\sigma_t^2 = \omega + \alpha \epsilon_{t-1}^2 + \beta \sigma_{t-1}^2$$

### Parameter Interpretation

| Parameter | Range | Interpretation |
|-----------|-------|----------------|
| $\omega$ | > 0 | Base/unconditional variance component |
| $\alpha$ | ≥ 0 | News coefficient (shock impact) |
| $\beta$ | ≥ 0 | Persistence coefficient |
| $\alpha + \beta$ | < 1 | Stationarity condition |

### Unconditional (Long-Run) Variance

$$\bar{\sigma}^2 = \frac{\omega}{1 - \alpha - \beta}$$

**Example:**
```
ω = 0.00001, α = 0.10, β = 0.85

Long-run variance = 0.00001 / (1 - 0.10 - 0.85)
                  = 0.00001 / 0.05
                  = 0.0002

Long-run volatility (daily) = √0.0002 = 1.41%
Annualized = 1.41% × √252 = 22.4%
```

### Persistence and Half-Life

**Persistence:** $P = \alpha + \beta$

Higher persistence = slower mean reversion

**Half-Life:** Time for shock to decay by 50%
$$HL = \frac{\ln(0.5)}{\ln(\alpha + \beta)}$$

**Example:**
```
α + β = 0.95

Half-life = ln(0.5) / ln(0.95) = -0.693 / -0.051 = 13.5 days

A volatility shock takes ~14 days to decay by half.
```

### Step-by-Step GARCH Estimation

**Given:** Returns $r_1, r_2, ..., r_T$ and initial variance $\sigma_0^2$

**Step 1:** Set initial values
- $\sigma_0^2 = \text{sample variance}$

**Step 2:** Recursively calculate conditional variances
$$\sigma_t^2 = \omega + \alpha r_{t-1}^2 + \beta \sigma_{t-1}^2$$

**Step 3:** Calculate log-likelihood
$$\ell = -\frac{1}{2}\sum_{t=1}^{T}\left[\ln(2\pi) + \ln(\sigma_t^2) + \frac{r_t^2}{\sigma_t^2}\right]$$

**Step 4:** Maximize likelihood using optimization

### Numerical Example

**Given:** $\omega = 0.00001$, $\alpha = 0.1$, $\beta = 0.85$, $\sigma_0^2 = 0.0002$

| Day | Return | $\epsilon_{t-1}^2$ | $\sigma_{t-1}^2$ | $\sigma_t^2$ |
|-----|--------|-------------------|-----------------|--------------|
| 0 | - | - | - | 0.0002 |
| 1 | 2% | - | 0.0002 | 0.00018 |
| 2 | -3% | 0.0004 | 0.00018 | 0.000203 |
| 3 | 1% | 0.0009 | 0.000203 | 0.000263 |

**Day 2 calculation:**
$$\sigma_2^2 = 0.00001 + 0.1(0.02)^2 + 0.85(0.0002) = 0.00001 + 0.00004 + 0.00017 = 0.00022$$

---

## 3. EGARCH Model

### Motivation

GARCH limitations:
1. Symmetric response to positive/negative shocks
2. Non-negativity constraints on parameters

### EGARCH Specification

$$\ln(\sigma_t^2) = \omega + \alpha\left(\frac{|\epsilon_{t-1}|}{\sigma_{t-1}} - \sqrt{\frac{2}{\pi}}\right) + \gamma\frac{\epsilon_{t-1}}{\sigma_{t-1}} + \beta\ln(\sigma_{t-1}^2)$$

Or simplified:
$$\ln(\sigma_t^2) = \omega + \alpha |z_{t-1}| + \gamma z_{t-1} + \beta\ln(\sigma_{t-1}^2)$$

Where $z_t = \epsilon_t / \sigma_t$

### Parameter Interpretation

| Parameter | Interpretation |
|-----------|----------------|
| $\omega$ | Constant term |
| $\alpha$ | Magnitude effect (size of shock) |
| $\gamma$ | Asymmetry effect (sign of shock) |
| $\beta$ | Persistence |

**Leverage Effect:**
- $\gamma < 0$: Negative returns increase volatility more
- $\gamma = 0$: Symmetric
- $\gamma > 0$: Positive returns increase volatility more

### Advantages of EGARCH

1. **No positivity constraints:** Log ensures $\sigma_t^2 > 0$
2. **Captures asymmetry:** $\gamma$ parameter
3. **Multiplicative shocks:** More realistic

### Example: EGARCH Response

**Parameters:** $\alpha = 0.15$, $\gamma = -0.08$, $\beta = 0.95$

**Positive shock ($z_{t-1} = 2$):**
$$\Delta\ln(\sigma_t^2) = 0.15(2) + (-0.08)(2) = 0.30 - 0.16 = 0.14$$

**Negative shock ($z_{t-1} = -2$):**
$$\Delta\ln(\sigma_t^2) = 0.15(2) + (-0.08)(-2) = 0.30 + 0.16 = 0.46$$

**Result:** Negative shock has 3.3× larger impact on variance.

---

## 4. GJR-GARCH Model

### Model Specification

$$\sigma_t^2 = \omega + \alpha\epsilon_{t-1}^2 + \gamma\epsilon_{t-1}^2 I_{[\epsilon_{t-1}<0]} + \beta\sigma_{t-1}^2$$

Where:
$$I_{[\epsilon_{t-1}<0]} = \begin{cases} 1 & \text{if } \epsilon_{t-1} < 0 \\ 0 & \text{if } \epsilon_{t-1} \geq 0 \end{cases}$$

### Interpretation

- **Positive shock:** Coefficient = $\alpha$
- **Negative shock:** Coefficient = $\alpha + \gamma$

If $\gamma > 0$: Negative shocks have larger impact (leverage effect)

### News Impact Curve

The relationship between past shocks and current variance:

**For GARCH:**
$$\sigma_t^2 = \omega + \beta\bar{\sigma}^2 + \alpha\epsilon_{t-1}^2$$
(Symmetric parabola)

**For GJR-GARCH:**
$$\sigma_t^2 = \begin{cases} \omega + \beta\bar{\sigma}^2 + \alpha\epsilon_{t-1}^2 & \text{if } \epsilon_{t-1} \geq 0 \\ \omega + \beta\bar{\sigma}^2 + (\alpha+\gamma)\epsilon_{t-1}^2 & \text{if } \epsilon_{t-1} < 0 \end{cases}$$
(Asymmetric - steeper for negative)

### Example: GJR-GARCH Calculation

**Parameters:** $\omega = 0.00001$, $\alpha = 0.05$, $\gamma = 0.10$, $\beta = 0.85$, $\sigma_0^2 = 0.0002$

**Case 1: Positive return of 2%**
$$\sigma_1^2 = 0.00001 + 0.05(0.02)^2 + 0.10(0.02)^2(0) + 0.85(0.0002)$$
$$= 0.00001 + 0.00002 + 0 + 0.00017 = 0.0002$$

**Case 2: Negative return of -2%**
$$\sigma_1^2 = 0.00001 + 0.05(-0.02)^2 + 0.10(-0.02)^2(1) + 0.85(0.0002)$$
$$= 0.00001 + 0.00002 + 0.00004 + 0.00017 = 0.00024$$

**Result:** Negative shock produces 20% higher variance.

### Unconditional Variance (GJR-GARCH)

$$\bar{\sigma}^2 = \frac{\omega}{1 - \alpha - \gamma/2 - \beta}$$

The $\gamma/2$ accounts for 50% probability of negative shocks.

---

## 5. Multivariate GARCH (DCC)

### Why Multivariate?

- Correlations change over time
- Joint risk measurement
- Portfolio optimization

### DCC Model Structure

**Step 1: Univariate GARCH** for each asset
$$\sigma_{i,t}^2 = \omega_i + \alpha_i\epsilon_{i,t-1}^2 + \beta_i\sigma_{i,t-1}^2$$

**Step 2: Standardize returns**
$$z_{i,t} = \frac{r_{i,t}}{\sigma_{i,t}}$$

**Step 3: Dynamic Correlation**
$$Q_t = (1 - a - b)\bar{Q} + a(z_{t-1}z_{t-1}') + bQ_{t-1}$$

**Step 4: Correlation Matrix**
$$R_t = \text{diag}(Q_t)^{-1/2} Q_t \text{diag}(Q_t)^{-1/2}$$

### DCC Parameters

| Parameter | Interpretation |
|-----------|----------------|
| $\bar{Q}$ | Unconditional correlation matrix |
| $a$ | News impact on correlation |
| $b$ | Persistence of correlation |
| $a + b$ | Total persistence |

### Covariance Matrix

$$H_t = D_t R_t D_t$$

Where:
- $D_t = \text{diag}(\sigma_{1,t}, \sigma_{2,t}, ..., \sigma_{N,t})$
- $R_t$ = Dynamic correlation matrix

### Example: Two-Asset DCC

**Given:**
- Asset 1: $\sigma_1 = 2\%$
- Asset 2: $\sigma_2 = 3\%$
- Dynamic correlation: $\rho_{12,t} = 0.6$

**Covariance:**
$$\sigma_{12,t} = \rho_{12,t} \times \sigma_{1,t} \times \sigma_{2,t} = 0.6 \times 0.02 \times 0.03 = 0.00036$$

**Covariance Matrix:**
$$H_t = \begin{bmatrix} 0.0004 & 0.00036 \\ 0.00036 & 0.0009 \end{bmatrix}$$

---

## 6. Volatility Forecasting

### One-Step Ahead Forecast

**GARCH(1,1):**
$$\hat{\sigma}_{T+1}^2 = \omega + \alpha\epsilon_T^2 + \beta\sigma_T^2$$

### Multi-Step Ahead Forecast

**h-step forecast:**
$$\hat{\sigma}_{T+h}^2 = \bar{\sigma}^2 + (\alpha + \beta)^{h-1}(\hat{\sigma}_{T+1}^2 - \bar{\sigma}^2)$$

As $h \to \infty$, forecast converges to unconditional variance $\bar{\sigma}^2$.

### Example: Multi-Step Forecast

**Given:** $\bar{\sigma}^2 = 0.0002$, $\alpha + \beta = 0.95$, $\hat{\sigma}_{T+1}^2 = 0.0004$

| Horizon | Formula | Forecast |
|---------|---------|----------|
| h=1 | Given | 0.0004 |
| h=2 | $0.0002 + 0.95(0.0004-0.0002)$ | 0.00039 |
| h=5 | $0.0002 + 0.95^4(0.0004-0.0002)$ | 0.000363 |
| h=10 | $0.0002 + 0.95^9(0.0004-0.0002)$ | 0.000326 |
| h=∞ | $\bar{\sigma}^2$ | 0.0002 |

### Forecast Evaluation

**Mean Squared Error:**
$$MSE = \frac{1}{T}\sum_{t=1}^{T}(\sigma_t^2 - \hat{\sigma}_t^2)^2$$

**Quasi-Likelihood (QLIKE):**
$$QLIKE = \frac{1}{T}\sum_{t=1}^{T}\left(\ln(\hat{\sigma}_t^2) + \frac{r_t^2}{\hat{\sigma}_t^2}\right)$$

**Mincer-Zarnowitz Regression:**
$$\sigma_t^2 = a + b\hat{\sigma}_t^2 + \epsilon_t$$

Good forecast: $a = 0$, $b = 1$, high $R^2$

---

## 7. Volatility Trading Strategies

### Volatility Risk Premium

**Implied vs. Realized:**
$$VRP = IV - RV$$

Historically: $IV > RV$ (volatility risk premium is positive)

### Strategy 1: Sell Volatility

**Concept:** Systematically sell options when IV > expected RV

**Implementation:**
- Sell straddles/strangles
- Delta hedge to isolate volatility exposure
- Profit if realized vol < implied vol

**Risk:** Large losses during volatility spikes

### Strategy 2: Variance Swaps

$$\text{Payoff} = N_{var}(\sigma_{realized}^2 - K_{var})$$

Where:
- $K_{var}$ = Strike (agreed variance)
- $\sigma_{realized}^2$ = Realized variance over period
- $N_{var}$ = Notional

**Example:**
```
Strike variance: 0.04 (20% vol)
Realized variance: 0.0625 (25% vol)
Notional: $100,000 per variance point

Payoff = 100,000 × (0.0625 - 0.04) = $2,250
```

### Strategy 3: Volatility Mean Reversion

**Signal:**
$$z_t = \frac{\sigma_t - \bar{\sigma}}{std(\sigma)}$$

**Rules:**
- $z > 2$: Short volatility (expect reversion down)
- $z < -2$: Long volatility (expect reversion up)

### Strategy 4: Volatility Breakout

**Concept:** Buy volatility when it breaks above recent range

**Implementation:**
```
If σ_t > max(σ_{t-20:t-1}):
    Buy straddle
    Hold for N days
```

### Risk Metrics Using GARCH

**Value at Risk (VaR):**
$$VaR_{1-\alpha} = -\mu + \sigma_t \times z_\alpha$$

**Example (95% VaR):**
```
μ = 0.05% (daily)
σ_t = 1.5% (from GARCH)
z_0.95 = 1.645

VaR_95 = -0.05% + 1.5% × 1.645 = 2.42%

With $1M position: VaR = $24,200
```

**Expected Shortfall:**
$$ES_{1-\alpha} = E[L | L > VaR_{1-\alpha}]$$

For normal:
$$ES = \mu + \sigma \times \frac{\phi(z_\alpha)}{1-\alpha}$$

---

## Key Formulas Summary

| Model | Variance Equation |
|-------|-------------------|
| GARCH(1,1) | $\sigma_t^2 = \omega + \alpha\epsilon_{t-1}^2 + \beta\sigma_{t-1}^2$ |
| EGARCH | $\ln\sigma_t^2 = \omega + \alpha|z_{t-1}| + \gamma z_{t-1} + \beta\ln\sigma_{t-1}^2$ |
| GJR-GARCH | $\sigma_t^2 = \omega + \alpha\epsilon_{t-1}^2 + \gamma\epsilon_{t-1}^2 I_{<0} + \beta\sigma_{t-1}^2$ |

| Concept | Formula |
|---------|---------|
| Long-run variance | $\bar{\sigma}^2 = \frac{\omega}{1-\alpha-\beta}$ |
| Half-life | $\frac{\ln(0.5)}{\ln(\alpha+\beta)}$ |
| h-step forecast | $\bar{\sigma}^2 + (\alpha+\beta)^{h-1}(\sigma_{T+1}^2 - \bar{\sigma}^2)$ |
| VaR | $-\mu + \sigma_t z_\alpha$ |

---

## Practice Problems

1. **GARCH(1,1):** Given ω=0.000005, α=0.08, β=0.90:
   - Calculate long-run volatility (daily and annual)
   - Calculate half-life of shocks
   - Is the model stationary?

2. **GJR-GARCH:** Given ω=0.00001, α=0.04, γ=0.08, β=0.87, σ²=0.0003:
   - Calculate variance after +3% shock
   - Calculate variance after -3% shock
   - What's the ratio of negative to positive impact?

3. **Forecasting:** Current σ²=0.0005, long-run σ²=0.0002, α+β=0.94:
   - Forecast variance for horizons 1, 5, 10, 20 days
   - At what horizon does forecast reach 95% of long-run level?

4. **VaR:** GARCH forecasts σ_tomorrow = 2.5%. Portfolio = $5M.
   - Calculate 99% 1-day VaR
   - Calculate 99% 10-day VaR (assume scaling)

---

*Next Week: Machine Learning for Trading*
