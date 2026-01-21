# Week 5: Portfolio Optimization Theory

## Table of Contents
1. [Modern Portfolio Theory](#1-modern-portfolio-theory)
2. [Mean-Variance Optimization](#2-mean-variance-optimization)
3. [Efficient Frontier](#3-efficient-frontier)
4. [Capital Market Line](#4-capital-market-line)
5. [Portfolio Risk Decomposition](#5-portfolio-risk-decomposition)
6. [Advanced Optimization Techniques](#6-advanced-optimization-techniques)
7. [Practical Considerations](#7-practical-considerations)

---

## 1. Modern Portfolio Theory

### The Foundation

Harry Markowitz (1952) revolutionized finance with one key insight:

> **Diversification reduces risk without necessarily reducing return.**

### Key Assumptions

1. Investors are risk-averse
2. Returns are normally distributed
3. Investors maximize expected utility
4. Single-period investment horizon
5. No transaction costs or taxes

### Risk and Return

For a portfolio of N assets with weights $w_1, w_2, ..., w_N$:

**Portfolio Return:**
$$R_p = \sum_{i=1}^{N} w_i R_i$$

**Expected Portfolio Return:**
$$E[R_p] = \sum_{i=1}^{N} w_i E[R_i] = \mathbf{w}^T \boldsymbol{\mu}$$

Where $\boldsymbol{\mu}$ = vector of expected returns

### Portfolio Variance

**Two-Asset Case:**
$$\sigma_p^2 = w_1^2\sigma_1^2 + w_2^2\sigma_2^2 + 2w_1w_2\sigma_{12}$$

**General N-Asset Case:**
$$\sigma_p^2 = \sum_{i=1}^{N}\sum_{j=1}^{N} w_i w_j \sigma_{ij} = \mathbf{w}^T \boldsymbol{\Sigma} \mathbf{w}$$

Where $\boldsymbol{\Sigma}$ = covariance matrix

---

## 2. Mean-Variance Optimization

### The Optimization Problem

**Minimize variance for a target return:**

$$\min_{\mathbf{w}} \quad \mathbf{w}^T \boldsymbol{\Sigma} \mathbf{w}$$

Subject to:
- $\mathbf{w}^T \boldsymbol{\mu} = \mu_p$ (target return)
- $\mathbf{w}^T \mathbf{1} = 1$ (weights sum to 1)
- $w_i \geq 0$ (optional: no short selling)

### Analytical Solution (No Constraints on Shorting)

Using Lagrangian:

$$L = \mathbf{w}^T \boldsymbol{\Sigma} \mathbf{w} - \lambda_1(\mathbf{w}^T \boldsymbol{\mu} - \mu_p) - \lambda_2(\mathbf{w}^T \mathbf{1} - 1)$$

**Solution:**
$$\mathbf{w}^* = \boldsymbol{\Sigma}^{-1}(\lambda_1 \boldsymbol{\mu} + \lambda_2 \mathbf{1})$$

Where $\lambda_1, \lambda_2$ are determined by constraints.

### Step-by-Step Example: Two Assets

**Given:**
- Stock A: $E[R_A] = 12\%$, $\sigma_A = 20\%$
- Stock B: $E[R_B] = 8\%$, $\sigma_B = 15\%$
- Correlation: $\rho_{AB} = 0.3$

**Find:** Optimal portfolio for $E[R_p] = 10\%$

**Step 1: Set up weight equation**
$$0.10 = w_A(0.12) + (1-w_A)(0.08)$$
$$0.10 = 0.12w_A + 0.08 - 0.08w_A$$
$$0.02 = 0.04w_A$$
$$w_A = 0.5, \quad w_B = 0.5$$

**Step 2: Calculate covariance**
$$\sigma_{AB} = \rho_{AB}\sigma_A\sigma_B = 0.3 \times 0.20 \times 0.15 = 0.009$$

**Step 3: Calculate portfolio variance**
$$\sigma_p^2 = (0.5)^2(0.20)^2 + (0.5)^2(0.15)^2 + 2(0.5)(0.5)(0.009)$$
$$= 0.01 + 0.005625 + 0.0045 = 0.020125$$

**Step 4: Portfolio volatility**
$$\sigma_p = \sqrt{0.020125} = 14.19\%$$

**Result:** 50/50 portfolio achieves 10% return with 14.19% volatility.

---

## 3. Efficient Frontier

### What is the Efficient Frontier?

The set of portfolios that:
- Maximize return for a given level of risk, OR
- Minimize risk for a given level of return

### Mathematical Characterization

The efficient frontier is a hyperbola in mean-variance space:

$$\sigma_p^2 = \frac{1}{D}\left[A\mu_p^2 - 2B\mu_p + C\right]$$

Where:
- $A = \mathbf{1}^T\boldsymbol{\Sigma}^{-1}\mathbf{1}$
- $B = \mathbf{1}^T\boldsymbol{\Sigma}^{-1}\boldsymbol{\mu}$
- $C = \boldsymbol{\mu}^T\boldsymbol{\Sigma}^{-1}\boldsymbol{\mu}$
- $D = AC - B^2$

### Global Minimum Variance Portfolio (GMVP)

The portfolio with lowest possible risk:

$$\mathbf{w}_{gmv} = \frac{\boldsymbol{\Sigma}^{-1}\mathbf{1}}{\mathbf{1}^T\boldsymbol{\Sigma}^{-1}\mathbf{1}}$$

**Return:** $\mu_{gmv} = \frac{B}{A}$

**Variance:** $\sigma_{gmv}^2 = \frac{1}{A}$

### Example: GMVP Calculation

**Given 2 assets:**
$$\boldsymbol{\Sigma} = \begin{bmatrix} 0.04 & 0.006 \\ 0.006 & 0.0225 \end{bmatrix}$$

**Step 1: Calculate inverse**
$$\boldsymbol{\Sigma}^{-1} = \frac{1}{\det(\Sigma)}\begin{bmatrix} 0.0225 & -0.006 \\ -0.006 & 0.04 \end{bmatrix}$$

$$\det(\Sigma) = 0.04 \times 0.0225 - 0.006^2 = 0.000864$$

$$\boldsymbol{\Sigma}^{-1} = \begin{bmatrix} 26.04 & -6.94 \\ -6.94 & 46.30 \end{bmatrix}$$

**Step 2: Calculate A**
$$A = [1, 1] \times \boldsymbol{\Sigma}^{-1} \times [1, 1]^T = 58.46$$

**Step 3: Calculate GMVP weights**
$$\mathbf{w}_{gmv} = \frac{1}{58.46}\begin{bmatrix} 26.04 - 6.94 \\ -6.94 + 46.30 \end{bmatrix} = \begin{bmatrix} 0.327 \\ 0.673 \end{bmatrix}$$

**Result:** GMVP is 32.7% Stock A, 67.3% Stock B

---

## 4. Capital Market Line

### Risk-Free Asset

When we add a risk-free asset with return $R_f$:

**Portfolio Return:**
$$E[R_p] = w_{risky}E[R_{risky}] + (1-w_{risky})R_f$$

**Portfolio Volatility:**
$$\sigma_p = w_{risky}\sigma_{risky}$$

### Capital Market Line (CML)

The CML is a straight line from $R_f$ tangent to the efficient frontier:

$$E[R_p] = R_f + \frac{E[R_m] - R_f}{\sigma_m}\sigma_p$$

Where:
- $R_m$ = return of market (tangent) portfolio
- $\sigma_m$ = volatility of market portfolio
- $\frac{E[R_m] - R_f}{\sigma_m}$ = Sharpe ratio of market

### Tangent (Market) Portfolio

The optimal risky portfolio that maximizes Sharpe ratio:

$$\max_{\mathbf{w}} \frac{\mathbf{w}^T\boldsymbol{\mu} - R_f}{\sqrt{\mathbf{w}^T\boldsymbol{\Sigma}\mathbf{w}}}$$

**Solution:**
$$\mathbf{w}_{tan} = \frac{\boldsymbol{\Sigma}^{-1}(\boldsymbol{\mu} - R_f\mathbf{1})}{\mathbf{1}^T\boldsymbol{\Sigma}^{-1}(\boldsymbol{\mu} - R_f\mathbf{1})}$$

### Sharpe Ratio

$$SR = \frac{E[R_p] - R_f}{\sigma_p}$$

**Interpretation:**
- Excess return per unit of risk
- Higher is better
- Allows comparison across different strategies

### Example: Tangent Portfolio

**Given:**
- Risk-free rate: 3%
- Stock A: $\mu_A = 12\%$, $\sigma_A = 20\%$
- Stock B: $\mu_B = 8\%$, $\sigma_B = 15\%$
- $\rho = 0.3$

**Step 1: Excess returns**
$$\boldsymbol{\mu} - R_f = [0.12 - 0.03, 0.08 - 0.03]^T = [0.09, 0.05]^T$$

**Step 2: Calculate numerator** (using $\Sigma^{-1}$ from before)
$$\boldsymbol{\Sigma}^{-1}(\boldsymbol{\mu} - R_f) = \begin{bmatrix} 26.04 & -6.94 \\ -6.94 & 46.30 \end{bmatrix} \begin{bmatrix} 0.09 \\ 0.05 \end{bmatrix} = \begin{bmatrix} 1.996 \\ 1.691 \end{bmatrix}$$

**Step 3: Normalize**
Sum = 1.996 + 1.691 = 3.687

$$\mathbf{w}_{tan} = \begin{bmatrix} 1.996/3.687 \\ 1.691/3.687 \end{bmatrix} = \begin{bmatrix} 0.541 \\ 0.459 \end{bmatrix}$$

**Result:** Tangent portfolio is 54.1% A, 45.9% B

---

## 5. Portfolio Risk Decomposition

### Marginal Contribution to Risk (MCR)

How much does each asset contribute to total portfolio risk?

$$MCR_i = \frac{\partial \sigma_p}{\partial w_i} = \frac{(\boldsymbol{\Sigma}\mathbf{w})_i}{\sigma_p}$$

### Component Contribution to Risk (CCR)

$$CCR_i = w_i \times MCR_i = \frac{w_i(\boldsymbol{\Sigma}\mathbf{w})_i}{\sigma_p}$$

**Property:** $\sum_{i=1}^{N} CCR_i = \sigma_p$

### Percentage Contribution to Risk (PCR)

$$PCR_i = \frac{CCR_i}{\sigma_p} = \frac{w_i(\boldsymbol{\Sigma}\mathbf{w})_i}{\sigma_p^2}$$

**Property:** $\sum_{i=1}^{N} PCR_i = 100\%$

### Example: Risk Decomposition

**Portfolio:** $w_A = 0.6$, $w_B = 0.4$

**Step 1: Calculate Σw**
$$\boldsymbol{\Sigma}\mathbf{w} = \begin{bmatrix} 0.04 & 0.009 \\ 0.009 & 0.0225 \end{bmatrix} \begin{bmatrix} 0.6 \\ 0.4 \end{bmatrix} = \begin{bmatrix} 0.0276 \\ 0.0144 \end{bmatrix}$$

**Step 2: Portfolio variance**
$$\sigma_p^2 = \mathbf{w}^T(\boldsymbol{\Sigma}\mathbf{w}) = 0.6(0.0276) + 0.4(0.0144) = 0.02232$$
$$\sigma_p = 14.94\%$$

**Step 3: PCR**
$$PCR_A = \frac{0.6 \times 0.0276}{0.02232} = 74.2\%$$
$$PCR_B = \frac{0.4 \times 0.0144}{0.02232} = 25.8\%$$

**Interpretation:** Stock A contributes 74.2% of portfolio risk despite only 60% weight.

---

## 6. Advanced Optimization Techniques

### Risk Parity

Equal risk contribution from each asset:

$$w_i \times MCR_i = w_j \times MCR_j \quad \forall i,j$$

**For 2 assets:**
$$\frac{w_1}{w_2} = \frac{\sigma_2}{\sigma_1}$$ (when uncorrelated)

### Black-Litterman Model

Combines market equilibrium with investor views:

$$\boldsymbol{\mu}_{BL} = [(\tau\boldsymbol{\Sigma})^{-1} + \mathbf{P}^T\boldsymbol{\Omega}^{-1}\mathbf{P}]^{-1}[(\tau\boldsymbol{\Sigma})^{-1}\boldsymbol{\Pi} + \mathbf{P}^T\boldsymbol{\Omega}^{-1}\mathbf{Q}]$$

Where:
- $\boldsymbol{\Pi}$ = equilibrium excess returns
- $\mathbf{P}$ = view matrix
- $\mathbf{Q}$ = view returns
- $\boldsymbol{\Omega}$ = view uncertainty
- $\tau$ = scaling factor

### Maximum Diversification Portfolio

Maximize diversification ratio:

$$\max_{\mathbf{w}} \frac{\sum w_i\sigma_i}{\sqrt{\mathbf{w}^T\boldsymbol{\Sigma}\mathbf{w}}}$$

### Minimum Correlation Portfolio

$$\min_{\mathbf{w}} \sum_{i}\sum_{j} w_i w_j \rho_{ij}$$

---

## 7. Practical Considerations

### Estimation Error

Expected returns and covariances must be estimated, introducing error:

**Problems:**
- Small changes in inputs → Large changes in weights
- Optimal portfolios often have extreme weights
- Out-of-sample performance disappoints

### Shrinkage Estimators

**Shrunk Covariance (Ledoit-Wolf):**
$$\boldsymbol{\Sigma}_{shrunk} = \delta \mathbf{F} + (1-\delta)\mathbf{S}$$

Where:
- $\mathbf{S}$ = sample covariance
- $\mathbf{F}$ = structured target (e.g., diagonal)
- $\delta$ = shrinkage intensity (estimated from data)

### Constraints in Practice

| Constraint | Purpose |
|------------|---------|
| $w_i \geq 0$ | No short selling |
| $w_i \leq 0.10$ | Position limits |
| $\sum_{sector} w_i \leq 0.30$ | Sector limits |
| $TE \leq 3\%$ | Tracking error |

### Transaction Costs

Incorporate trading costs into optimization:

$$\max_{\mathbf{w}} \mathbf{w}^T\boldsymbol{\mu} - \frac{\lambda}{2}\mathbf{w}^T\boldsymbol{\Sigma}\mathbf{w} - \sum_i c_i|w_i - w_i^{old}|$$

### Rebalancing

**Calendar:** Monthly, quarterly
**Threshold:** When weights drift by X%
**Optimization-based:** When utility drops below threshold

---

## Key Formulas Summary

| Concept | Formula |
|---------|---------|
| Portfolio Return | $E[R_p] = \mathbf{w}^T\boldsymbol{\mu}$ |
| Portfolio Variance | $\sigma_p^2 = \mathbf{w}^T\boldsymbol{\Sigma}\mathbf{w}$ |
| GMVP Weights | $\mathbf{w} = \frac{\Sigma^{-1}\mathbf{1}}{\mathbf{1}^T\Sigma^{-1}\mathbf{1}}$ |
| Tangent Portfolio | $\mathbf{w} = \frac{\Sigma^{-1}(\mu - R_f)}{\mathbf{1}^T\Sigma^{-1}(\mu - R_f)}$ |
| Sharpe Ratio | $SR = \frac{E[R_p] - R_f}{\sigma_p}$ |
| CML | $E[R_p] = R_f + SR_m \times \sigma_p$ |
| PCR | $\frac{w_i(\Sigma\mathbf{w})_i}{\sigma_p^2}$ |

---

## Practice Problems

1. **Two-asset portfolio:** A (15%, 25%), B (10%, 20%), ρ=0.4
   - Find GMVP weights and volatility
   - Find tangent portfolio (Rf=4%)
   
2. **Three-asset portfolio:** Given covariance matrix, calculate portfolio variance for equal weights.

3. **Risk decomposition:** For a 70/30 portfolio, calculate each asset's percentage contribution to risk.

4. **Sharpe ratio comparison:** Strategy A: 12% return, 20% vol. Strategy B: 8% return, 10% vol. Rf=3%. Which is better?

5. **CML question:** Market portfolio has SR=0.5, Rf=3%. What return can you expect at 15% volatility?

---

*Next Week: Factor Models*
