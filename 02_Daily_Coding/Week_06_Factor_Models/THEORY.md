# Week 6: Factor Models in Finance

## Table of Contents
1. [Introduction to Factor Models](#1-introduction-to-factor-models)
2. [Capital Asset Pricing Model (CAPM)](#2-capital-asset-pricing-model-capm)
3. [Fama-French Three-Factor Model](#3-fama-french-three-factor-model)
4. [Fama-French Five-Factor Model](#4-fama-french-five-factor-model)
5. [Arbitrage Pricing Theory (APT)](#5-arbitrage-pricing-theory-apt)
6. [Factor Exposure Analysis](#6-factor-exposure-analysis)
7. [Building Factor Portfolios](#7-building-factor-portfolios)

---

## 1. Introduction to Factor Models

### What is a Factor Model?

A factor model explains asset returns through exposure to common risk factors:

$$R_i = \alpha_i + \sum_{k=1}^{K} \beta_{ik} F_k + \epsilon_i$$

Where:
- $R_i$ = Return of asset i
- $\alpha_i$ = Alpha (unexplained return)
- $\beta_{ik}$ = Exposure (loading) to factor k
- $F_k$ = Return of factor k
- $\epsilon_i$ = Idiosyncratic (asset-specific) return

### Why Factor Models?

1. **Dimensionality Reduction:** N assets → K factors (K << N)
2. **Risk Attribution:** Understand sources of risk
3. **Alpha Generation:** Identify mispriced assets
4. **Portfolio Construction:** Control factor exposures

### Types of Factors

| Category | Examples |
|----------|----------|
| **Macroeconomic** | GDP, Inflation, Interest rates |
| **Statistical** | PCA factors, Independent components |
| **Fundamental** | Value, Size, Momentum, Quality |
| **Technical** | Volatility, Trend, Mean-reversion |

---

## 2. Capital Asset Pricing Model (CAPM)

### The Single-Factor Model

CAPM states that a stock's expected return depends only on its exposure to market risk:

$$E[R_i] - R_f = \beta_i (E[R_m] - R_f)$$

Or equivalently:
$$E[R_i] = R_f + \beta_i (E[R_m] - R_f)$$

Where:
- $R_f$ = Risk-free rate
- $R_m$ = Market return
- $\beta_i$ = Stock's sensitivity to market
- $E[R_m] - R_f$ = Market risk premium

### Beta: Systematic Risk

$$\beta_i = \frac{\text{Cov}(R_i, R_m)}{\text{Var}(R_m)} = \frac{\sigma_{im}}{\sigma_m^2}$$

**Interpretation:**
| Beta | Meaning |
|------|---------|
| β = 1 | Moves with market |
| β > 1 | More volatile than market |
| β < 1 | Less volatile than market |
| β = 0 | Uncorrelated with market |
| β < 0 | Moves opposite to market |

### Step-by-Step Beta Calculation

**Example:** Calculate beta from 5 observations

| Period | Stock Return | Market Return |
|--------|-------------|---------------|
| 1 | 8% | 5% |
| 2 | -2% | -3% |
| 3 | 12% | 7% |
| 4 | -5% | -4% |
| 5 | 6% | 4% |

**Step 1: Calculate means**
$$\bar{R}_i = \frac{8-2+12-5+6}{5} = 3.8\%$$
$$\bar{R}_m = \frac{5-3+7-4+4}{5} = 1.8\%$$

**Step 2: Calculate deviations and products**

| Period | $R_i - \bar{R}_i$ | $R_m - \bar{R}_m$ | Product | $(R_m - \bar{R}_m)^2$ |
|--------|-------------------|-------------------|---------|----------------------|
| 1 | 4.2% | 3.2% | 0.1344% | 0.1024% |
| 2 | -5.8% | -4.8% | 0.2784% | 0.2304% |
| 3 | 8.2% | 5.2% | 0.4264% | 0.2704% |
| 4 | -8.8% | -5.8% | 0.5104% | 0.3364% |
| 5 | 2.2% | 2.2% | 0.0484% | 0.0484% |
| **Sum** | | | **1.398%** | **0.988%** |

**Step 3: Calculate covariance and variance**
$$\text{Cov}(R_i, R_m) = \frac{1.398\%}{4} = 0.3495\%$$
$$\text{Var}(R_m) = \frac{0.988\%}{4} = 0.247\%$$

**Step 4: Calculate beta**
$$\beta = \frac{0.3495\%}{0.247\%} = 1.41$$

**Interpretation:** Stock is 41% more volatile than market.

### Security Market Line (SML)

The SML plots expected return vs. beta:

$$E[R_i] = R_f + \beta_i [E[R_m] - R_f]$$

**Alpha:** Distance from SML
- Positive alpha: Undervalued (above SML)
- Negative alpha: Overvalued (below SML)

### CAPM Assumptions and Limitations

**Assumptions:**
1. Investors are mean-variance optimizers
2. Single period, same expectations
3. No taxes, transaction costs
4. Unlimited borrowing at risk-free rate

**Limitations:**
- Empirical evidence shows other factors matter
- Beta doesn't fully explain cross-sectional returns
- Low-beta anomaly: Low-beta stocks outperform

---

## 3. Fama-French Three-Factor Model

### Beyond CAPM

Fama and French (1993) found two additional factors explain returns:

$$R_i - R_f = \alpha_i + \beta_i^{MKT}(R_m - R_f) + \beta_i^{SMB} \cdot SMB + \beta_i^{HML} \cdot HML + \epsilon_i$$

### The Three Factors

**1. Market (MKT):** Same as CAPM
$$MKT = R_m - R_f$$

**2. Size (SMB - Small Minus Big):**
$$SMB = R_{small} - R_{big}$$

Small stocks historically outperform large stocks.

**3. Value (HML - High Minus Low):**
$$HML = R_{high B/M} - R_{low B/M}$$

Value stocks (high book-to-market) outperform growth stocks.

### Factor Construction

**SMB Construction:**
1. Rank stocks by market cap
2. Top 50% = Big, Bottom 50% = Small
3. $SMB = \bar{R}_{small} - \bar{R}_{big}$

**HML Construction:**
1. Rank stocks by Book-to-Market ratio
2. Top 30% = Value, Bottom 30% = Growth
3. $HML = \bar{R}_{value} - \bar{R}_{growth}$

### Example: FF3 Regression

**Model:** $R_i - R_f = \alpha + \beta_1 MKT + \beta_2 SMB + \beta_3 HML + \epsilon$

**Results for a fund:**
- $\alpha = 0.002$ (0.2% monthly alpha)
- $\beta_{MKT} = 1.1$
- $\beta_{SMB} = 0.5$
- $\beta_{HML} = -0.3$

**Interpretation:**
- Fund has positive alpha (skill or luck)
- 10% more market exposure than market
- Tilted toward small caps
- Tilted toward growth stocks

### Expected Return Calculation

Given factor risk premiums:
- $E[MKT] = 6\%$
- $E[SMB] = 2\%$
- $E[HML] = 3\%$
- $R_f = 2\%$

**Expected return:**
$$E[R_i] = 2\% + 1.1(6\%) + 0.5(2\%) + (-0.3)(3\%)$$
$$= 2\% + 6.6\% + 1\% - 0.9\% = 8.7\%$$

---

## 4. Fama-French Five-Factor Model

### Two Additional Factors

Fama and French (2015) added profitability and investment:

$$R_i - R_f = \alpha + \beta_{MKT} MKT + \beta_{SMB} SMB + \beta_{HML} HML + \beta_{RMW} RMW + \beta_{CMA} CMA + \epsilon$$

### The Five Factors

| Factor | Name | Description | Long | Short |
|--------|------|-------------|------|-------|
| MKT | Market | Market excess return | Market | Risk-free |
| SMB | Size | Small minus Big | Small caps | Large caps |
| HML | Value | High minus Low B/M | Value | Growth |
| RMW | Profitability | Robust minus Weak | High profit | Low profit |
| CMA | Investment | Conservative minus Aggressive | Low invest | High invest |

### RMW (Profitability Factor)

$$RMW = R_{robust} - R_{weak}$$

- Robust: High operating profitability
- Weak: Low operating profitability

**Metric:** Operating Profit / Book Equity

### CMA (Investment Factor)

$$CMA = R_{conservative} - R_{aggressive}$$

- Conservative: Low asset growth
- Aggressive: High asset growth

**Rationale:** Companies that invest less tend to have higher returns.

### Interpretation Example

**Fund factor loadings:**
| Factor | Loading | Premium | Contribution |
|--------|---------|---------|--------------|
| MKT | 0.95 | 6% | 5.7% |
| SMB | 0.2 | 2% | 0.4% |
| HML | 0.3 | 3% | 0.9% |
| RMW | 0.4 | 3% | 1.2% |
| CMA | -0.1 | 2% | -0.2% |
| **Total** | | | **8.0%** |

Expected excess return = 8.0%

---

## 5. Arbitrage Pricing Theory (APT)

### The APT Framework

Ross (1976) proposed a more general factor model:

$$E[R_i] = R_f + \sum_{k=1}^{K} \beta_{ik} \lambda_k$$

Where:
- $\beta_{ik}$ = Sensitivity to factor k
- $\lambda_k$ = Risk premium for factor k

### Key Differences from CAPM

| Aspect | CAPM | APT |
|--------|------|-----|
| Factors | One (market) | Multiple |
| Derivation | Equilibrium | No-arbitrage |
| Factor identity | Market specified | Unspecified |
| Assumptions | Stricter | Fewer |

### Statistical Factor Models (PCA)

**Principal Component Analysis** extracts factors from returns:

$$\mathbf{R} = \mathbf{F}\mathbf{B}^T + \mathbf{E}$$

Where:
- $\mathbf{R}$ = Returns matrix (T × N)
- $\mathbf{F}$ = Factors (T × K)
- $\mathbf{B}$ = Loadings (N × K)
- $\mathbf{E}$ = Residuals

### PCA Step-by-Step

**Step 1:** Standardize returns

**Step 2:** Compute covariance matrix $\Sigma$

**Step 3:** Find eigenvalues $\lambda_1 > \lambda_2 > ... > \lambda_N$ and eigenvectors $\mathbf{v}_1, \mathbf{v}_2, ...$

**Step 4:** Variance explained by factor k:
$$\frac{\lambda_k}{\sum_i \lambda_i}$$

**Step 5:** Select K factors explaining desired variance (e.g., 90%)

### Example: PCA Results

| PC | Eigenvalue | Variance Explained | Cumulative |
|----|------------|-------------------|------------|
| 1 | 8.5 | 42.5% | 42.5% |
| 2 | 2.1 | 10.5% | 53.0% |
| 3 | 1.3 | 6.5% | 59.5% |
| 4 | 0.9 | 4.5% | 64.0% |

**Interpretation:** First PC (often market) explains 42.5% of variance.

---

## 6. Factor Exposure Analysis

### Calculating Factor Exposures

**Time-Series Regression:**
$$R_{i,t} - R_f = \alpha_i + \sum_k \beta_{ik} F_{k,t} + \epsilon_{i,t}$$

Run OLS regression to estimate betas.

### Rolling Factor Exposures

Factor exposures change over time. Use rolling windows:

```
Window 1: Days 1-252 → β₁
Window 2: Days 2-253 → β₂
...
```

### Portfolio Factor Exposure

Portfolio exposure = weighted average of asset exposures:

$$\beta_p^k = \sum_{i=1}^{N} w_i \beta_i^k$$

### Factor Attribution

Decompose portfolio return:

$$R_p - R_f = \alpha_p + \sum_k \beta_p^k F_k + \epsilon_p$$

| Component | Formula | Interpretation |
|-----------|---------|----------------|
| Alpha | $\alpha_p$ | Skill |
| Factor | $\beta_p^k F_k$ | Systematic risk |
| Residual | $\epsilon_p$ | Idiosyncratic |

### Example: Return Attribution

**Portfolio return:** 15%
**Factor decomposition:**
- Risk-free: 2%
- Market contribution: 1.1 × 8% = 8.8%
- SMB contribution: 0.3 × 3% = 0.9%
- HML contribution: 0.5 × 4% = 2.0%
- Alpha: 15% - 2% - 8.8% - 0.9% - 2.0% = 1.3%

---

## 7. Building Factor Portfolios

### Long-Short Factor Portfolios

**Construction:**
1. Rank stocks by factor characteristic
2. Long top decile/quartile
3. Short bottom decile/quartile
4. Equal or value weight within

### Momentum Factor Example

$$MOM = R_{winners} - R_{losers}$$

**Construction:**
1. Calculate 12-1 month return (skip most recent month)
2. Rank stocks
3. Long top 30%, Short bottom 30%

### Factor Timing

Some factors are cyclical:
- Value: Performs in recoveries
- Momentum: Performs in trends
- Quality: Performs in downturns

### Multi-Factor Portfolio Construction

**Goal:** Capture multiple premiums simultaneously

**Approach 1: Factor Integration**
Combine factor scores into single signal:
$$Score_i = w_1 \cdot Value_i + w_2 \cdot Mom_i + w_3 \cdot Quality_i$$

**Approach 2: Factor Sleeves**
Allocate separately to each factor portfolio.

### Factor Neutralization

Remove unwanted factor exposures:

$$\beta_{target}^{unwanted} = 0$$

**Example:** Market-neutral long-short
- Long portfolio: $1M in high-value stocks
- Short portfolio: $1M in low-value stocks
- Net market exposure ≈ 0

### Information Ratio

$$IR = \frac{\alpha}{\sigma_{residual}} = \frac{E[R_p - R_b]}{\sigma(R_p - R_b)}$$

**Interpretation:**
- IR > 0.5: Good
- IR > 1.0: Excellent
- IR > 1.5: Exceptional

---

## Key Formulas Summary

| Model/Concept | Formula |
|---------------|---------|
| CAPM | $E[R_i] = R_f + \beta_i(E[R_m] - R_f)$ |
| Beta | $\beta = \frac{\text{Cov}(R_i, R_m)}{\text{Var}(R_m)}$ |
| FF3 | $R - R_f = \alpha + \beta_{MKT}MKT + \beta_{SMB}SMB + \beta_{HML}HML$ |
| SMB | $R_{small} - R_{big}$ |
| HML | $R_{value} - R_{growth}$ |
| APT | $E[R_i] = R_f + \sum_k \beta_k \lambda_k$ |
| Portfolio Beta | $\beta_p = \sum_i w_i \beta_i$ |
| Information Ratio | $\frac{\alpha}{\sigma_{residual}}$ |

---

## Practice Problems

1. **Beta calculation:** Given Cov(stock, market) = 0.0024 and Var(market) = 0.0016, calculate beta.

2. **CAPM expected return:** β = 1.3, Rf = 3%, E[Rm] = 9%. What's expected return?

3. **FF3 interpretation:** A fund has loadings: MKT=0.9, SMB=-0.2, HML=0.4. Describe the fund's style.

4. **Factor contribution:** Calculate expected return contribution from each factor given loadings and premiums.

5. **PCA variance:** First 3 eigenvalues are 5, 2, 1 out of total 10. What % variance do they explain?

---

*Next Week: Advanced Volatility Models*
