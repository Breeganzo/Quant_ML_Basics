# Week 1: Mathematical Foundations for Quantitative Finance

## Table of Contents
1. [Returns: The Language of Finance](#1-returns-the-language-of-finance)
2. [Volatility: Measuring Risk](#2-volatility-measuring-risk)
3. [Correlation & Covariance](#3-correlation--covariance)
4. [Time Value of Money](#4-time-value-of-money)
5. [Statistical Foundations](#5-statistical-foundations)

---

## 1. Returns: The Language of Finance

### Why Returns, Not Prices?

In finance, we analyze **returns** rather than prices because:
- Returns are **scale-free** (comparable across assets)
- Returns have better **statistical properties** (more stationary)
- Returns aggregate nicely over time

### Simple (Arithmetic) Return

**Definition:** The percentage change in price over one period.

$$R_t = \frac{P_t - P_{t-1}}{P_{t-1}} = \frac{P_t}{P_{t-1}} - 1$$

Where:
- $R_t$ = Return at time t
- $P_t$ = Price at time t
- $P_{t-1}$ = Price at time t-1

**Example:**
```
Stock price yesterday: $100
Stock price today: $105

Simple Return = (105 - 100) / 100 = 0.05 = 5%
```

### Logarithmic (Continuously Compounded) Return

**Definition:** The natural log of the price ratio.

$$r_t = \ln\left(\frac{P_t}{P_{t-1}}\right) = \ln(P_t) - \ln(P_{t-1})$$

**Why Log Returns?**

1. **Time Additivity:** Log returns sum over time
   $$r_{t:t+n} = r_t + r_{t+1} + ... + r_{t+n}$$

2. **Symmetric:** +10% and -10% log returns are symmetric around zero

3. **Approximate Normality:** Log returns are closer to normally distributed

**Example:**
```
Stock price yesterday: $100
Stock price today: $105

Log Return = ln(105/100) = ln(1.05) = 0.0488 = 4.88%
```

### Relationship Between Simple and Log Returns

$$r_t = \ln(1 + R_t)$$

For small returns (< 10%), they are approximately equal:
$$r_t \approx R_t$$

### Multi-Period Returns

**Simple Returns (Compound):**
$$R_{t:t+n} = (1 + R_t)(1 + R_{t+1})...(1 + R_{t+n}) - 1$$

**Log Returns (Sum):**
$$r_{t:t+n} = r_t + r_{t+1} + ... + r_{t+n}$$

**Example: 2-Day Return**
```
Day 1: +5% simple return
Day 2: +3% simple return

2-Day Simple Return = (1.05)(1.03) - 1 = 8.15%
2-Day Log Return = ln(1.05) + ln(1.03) = 4.88% + 2.96% = 7.84%
```

---

## 2. Volatility: Measuring Risk

### What is Volatility?

Volatility measures the **dispersion of returns** - how much returns deviate from their average.

### Standard Deviation (Population)

$$\sigma = \sqrt{\frac{1}{N}\sum_{i=1}^{N}(r_i - \bar{r})^2}$$

Where:
- $\sigma$ = Standard deviation (volatility)
- $N$ = Number of observations
- $r_i$ = Individual return
- $\bar{r}$ = Mean return

### Sample Standard Deviation

$$s = \sqrt{\frac{1}{N-1}\sum_{i=1}^{N}(r_i - \bar{r})^2}$$

We use $N-1$ (Bessel's correction) for unbiased estimation.

### Step-by-Step Volatility Calculation

**Example: Calculate 5-day volatility**

| Day | Return |
|-----|--------|
| 1 | +2% |
| 2 | -1% |
| 3 | +3% |
| 4 | -2% |
| 5 | +1% |

**Step 1: Calculate mean**
$$\bar{r} = \frac{2 + (-1) + 3 + (-2) + 1}{5} = \frac{3}{5} = 0.6\%$$

**Step 2: Calculate squared deviations**
| Day | Return | Deviation $(r_i - \bar{r})$ | Squared |
|-----|--------|---------------------------|---------|
| 1 | 2% | 1.4% | 0.0196% |
| 2 | -1% | -1.6% | 0.0256% |
| 3 | 3% | 2.4% | 0.0576% |
| 4 | -2% | -2.6% | 0.0676% |
| 5 | 1% | 0.4% | 0.0016% |
| **Sum** | | | **0.172%** |

**Step 3: Calculate variance**
$$\text{Variance} = \frac{0.172\%}{5-1} = \frac{0.172\%}{4} = 0.043\%$$

**Step 4: Calculate standard deviation**
$$\text{Daily Volatility} = \sqrt{0.043\%} = 2.07\%$$

### Annualizing Volatility

Daily volatility must be annualized for comparison:

$$\sigma_{annual} = \sigma_{daily} \times \sqrt{252}$$

Where 252 = trading days per year

**Example:**
```
Daily volatility = 2.07%
Annual volatility = 2.07% × √252 = 2.07% × 15.87 = 32.9%
```

### Variance vs. Standard Deviation

| Measure | Formula | Units | Use Case |
|---------|---------|-------|----------|
| Variance | $\sigma^2$ | %² | Portfolio math |
| Std Dev | $\sigma$ | % | Risk reporting |

---

## 3. Correlation & Covariance

### Covariance: Measuring Co-movement

Covariance measures how two variables move together.

$$\text{Cov}(X, Y) = \sigma_{XY} = \frac{1}{N-1}\sum_{i=1}^{N}(x_i - \bar{x})(y_i - \bar{y})$$

**Interpretation:**
- **Positive covariance:** Variables move in same direction
- **Negative covariance:** Variables move in opposite directions
- **Zero covariance:** No linear relationship

### Correlation: Standardized Covariance

Correlation normalizes covariance to [-1, +1].

$$\rho_{XY} = \frac{\text{Cov}(X, Y)}{\sigma_X \cdot \sigma_Y} = \frac{\sigma_{XY}}{\sigma_X \sigma_Y}$$

**Interpretation:**
| Correlation | Relationship |
|-------------|--------------|
| +1.0 | Perfect positive |
| +0.5 to +0.9 | Strong positive |
| +0.1 to +0.5 | Weak positive |
| 0 | No linear relationship |
| -0.1 to -0.5 | Weak negative |
| -0.5 to -0.9 | Strong negative |
| -1.0 | Perfect negative |

### Step-by-Step Correlation Calculation

**Example: Calculate correlation between Stock A and Stock B**

| Day | Stock A Return | Stock B Return |
|-----|---------------|---------------|
| 1 | +3% | +2% |
| 2 | -1% | -2% |
| 3 | +2% | +1% |
| 4 | -2% | -1% |
| 5 | +1% | +2% |

**Step 1: Calculate means**
$$\bar{r}_A = \frac{3-1+2-2+1}{5} = 0.6\%$$
$$\bar{r}_B = \frac{2-2+1-1+2}{5} = 0.4\%$$

**Step 2: Calculate deviations and products**
| Day | $r_A - \bar{r}_A$ | $r_B - \bar{r}_B$ | Product |
|-----|-------------------|-------------------|---------|
| 1 | 2.4% | 1.6% | 0.0384% |
| 2 | -1.6% | -2.4% | 0.0384% |
| 3 | 1.4% | 0.6% | 0.0084% |
| 4 | -2.6% | -1.4% | 0.0364% |
| 5 | 0.4% | 1.6% | 0.0064% |
| **Sum** | | | **0.128%** |

**Step 3: Calculate covariance**
$$\text{Cov}(A, B) = \frac{0.128\%}{4} = 0.032\%$$

**Step 4: Calculate standard deviations**
$$\sigma_A = 2.07\%, \quad \sigma_B = 1.67\%$$

**Step 5: Calculate correlation**
$$\rho_{AB} = \frac{0.032\%}{2.07\% \times 1.67\%} = \frac{0.032\%}{0.0346\%} = 0.92$$

**Interpretation:** Stock A and B are highly positively correlated.

### Covariance Matrix

For N assets, the covariance matrix $\Sigma$ is N×N:

$$\Sigma = \begin{bmatrix} \sigma_1^2 & \sigma_{12} & \cdots & \sigma_{1N} \\ \sigma_{21} & \sigma_2^2 & \cdots & \sigma_{2N} \\ \vdots & \vdots & \ddots & \vdots \\ \sigma_{N1} & \sigma_{N2} & \cdots & \sigma_N^2 \end{bmatrix}$$

**Properties:**
- Symmetric: $\sigma_{ij} = \sigma_{ji}$
- Diagonal = variances
- Off-diagonal = covariances

---

## 4. Time Value of Money

### Present Value

Money today is worth more than money tomorrow.

$$PV = \frac{FV}{(1+r)^n}$$

Where:
- $PV$ = Present Value
- $FV$ = Future Value
- $r$ = Interest rate per period
- $n$ = Number of periods

**Example:**
```
What is $1,000 in 5 years worth today at 5% rate?

PV = 1000 / (1.05)^5 = 1000 / 1.276 = $783.53
```

### Future Value

$$FV = PV \times (1+r)^n$$

### Continuous Compounding

$$FV = PV \times e^{rt}$$

$$PV = FV \times e^{-rt}$$

**Example:**
```
$1,000 at 5% continuously compounded for 5 years:

FV = 1000 × e^(0.05 × 5) = 1000 × e^0.25 = $1,284.03
```

### Net Present Value (NPV)

$$NPV = \sum_{t=0}^{N} \frac{CF_t}{(1+r)^t}$$

Where $CF_t$ = Cash flow at time t

---

## 5. Statistical Foundations

### Expected Value (Mean)

$$E[X] = \mu = \frac{1}{N}\sum_{i=1}^{N}x_i$$

For probability distribution:
$$E[X] = \sum_{i} x_i \cdot P(x_i)$$

### Variance

$$\text{Var}(X) = E[(X - \mu)^2] = E[X^2] - (E[X])^2$$

### Properties of Expected Value and Variance

**Expected Value:**
- $E[aX + b] = aE[X] + b$
- $E[X + Y] = E[X] + E[Y]$

**Variance:**
- $\text{Var}(aX + b) = a^2\text{Var}(X)$
- $\text{Var}(X + Y) = \text{Var}(X) + \text{Var}(Y) + 2\text{Cov}(X,Y)$

### Skewness: Asymmetry

$$\text{Skewness} = \frac{E[(X-\mu)^3]}{\sigma^3}$$

| Value | Interpretation |
|-------|---------------|
| = 0 | Symmetric |
| > 0 | Right-tailed (positive) |
| < 0 | Left-tailed (negative) |

**In finance:** Stock returns often have **negative skewness** (large losses more common than large gains).

### Kurtosis: Tail Thickness

$$\text{Kurtosis} = \frac{E[(X-\mu)^4]}{\sigma^4}$$

**Excess Kurtosis** = Kurtosis - 3

| Value | Interpretation |
|-------|---------------|
| = 3 (excess = 0) | Normal distribution |
| > 3 | Fat tails (leptokurtic) |
| < 3 | Thin tails (platykurtic) |

**In finance:** Returns typically have **excess kurtosis** (fat tails) - extreme events are more common than normal distribution predicts.

---

## Key Formulas Summary

| Concept | Formula |
|---------|---------|
| Simple Return | $R_t = \frac{P_t - P_{t-1}}{P_{t-1}}$ |
| Log Return | $r_t = \ln(P_t/P_{t-1})$ |
| Annualized Return | $R_{annual} = R_{daily} \times 252$ |
| Annualized Volatility | $\sigma_{annual} = \sigma_{daily} \times \sqrt{252}$ |
| Covariance | $\text{Cov}(X,Y) = E[(X-\mu_X)(Y-\mu_Y)]$ |
| Correlation | $\rho = \frac{\text{Cov}(X,Y)}{\sigma_X \sigma_Y}$ |
| Present Value | $PV = \frac{FV}{(1+r)^n}$ |
| Sharpe Ratio | $SR = \frac{R - R_f}{\sigma}$ |

---

## Practice Problems

1. A stock goes from $50 to $55 to $52. Calculate the 2-day simple and log return.

2. Given daily returns of [1%, -2%, 3%, -1%, 2%], calculate the annualized volatility.

3. Two stocks have correlation of 0.6. Stock A has volatility 20%, Stock B has 30%. What is their covariance?

4. What is the present value of $10,000 received in 3 years at 8% annual rate?

---

*Next Week: Statistics & Probability Distributions*
