# Week 2: Statistics and Probability for Quantitative Finance

## Table of Contents
1. [Probability Distributions](#1-probability-distributions)
2. [Normal Distribution in Finance](#2-normal-distribution-in-finance)
3. [Hypothesis Testing](#3-hypothesis-testing)
4. [Regression Analysis](#4-regression-analysis)
5. [Maximum Likelihood Estimation](#5-maximum-likelihood-estimation)

---

## 1. Probability Distributions

### What is a Probability Distribution?

A probability distribution describes all possible values a random variable can take and their probabilities.

### Discrete vs. Continuous

| Type | Examples | Description |
|------|----------|-------------|
| **Discrete** | Binomial, Poisson | Countable outcomes |
| **Continuous** | Normal, Log-normal | Infinite possible values |

### Key Distribution Properties

**Probability Density Function (PDF):** $f(x)$
- Gives relative likelihood at point x
- $P(a \leq X \leq b) = \int_a^b f(x)dx$

**Cumulative Distribution Function (CDF):** $F(x)$
- $F(x) = P(X \leq x)$
- $F(x) = \int_{-\infty}^x f(t)dt$

### Binomial Distribution

Models the number of successes in n independent trials.

$$P(X = k) = \binom{n}{k} p^k (1-p)^{n-k}$$

Where:
- $n$ = number of trials
- $k$ = number of successes
- $p$ = probability of success

**Example: Stock Movement**
```
Probability stock goes up on any day: 55%
What's the probability it goes up exactly 3 out of 5 days?

P(X=3) = C(5,3) × (0.55)³ × (0.45)²
       = 10 × 0.166 × 0.203
       = 0.337 = 33.7%
```

**Mean and Variance:**
$$E[X] = np, \quad \text{Var}(X) = np(1-p)$$

### Poisson Distribution

Models rare events occurring in a fixed interval.

$$P(X = k) = \frac{\lambda^k e^{-\lambda}}{k!}$$

Where $\lambda$ = average rate of occurrence

**Example: Trading Halts**
```
Average 2 trading halts per month.
Probability of exactly 4 halts this month?

P(X=4) = (2⁴ × e⁻²) / 4!
       = (16 × 0.135) / 24
       = 0.090 = 9.0%
```

**Mean and Variance:**
$$E[X] = \lambda, \quad \text{Var}(X) = \lambda$$

---

## 2. Normal Distribution in Finance

### The Normal (Gaussian) Distribution

$$f(x) = \frac{1}{\sigma\sqrt{2\pi}} e^{-\frac{(x-\mu)^2}{2\sigma^2}}$$

Where:
- $\mu$ = mean (center)
- $\sigma$ = standard deviation (spread)

### Properties

1. **Symmetric** around the mean
2. **68-95-99.7 Rule:**
   - 68% of data within 1σ of mean
   - 95% of data within 2σ of mean
   - 99.7% of data within 3σ of mean

### Standard Normal Distribution

When $\mu = 0$ and $\sigma = 1$:

$$Z = \frac{X - \mu}{\sigma}$$

This is called **standardization** or **z-score transformation**.

### Z-Score Interpretation

| Z-Score | Meaning | Percentile |
|---------|---------|------------|
| -3 | 3σ below mean | 0.13% |
| -2 | 2σ below mean | 2.28% |
| -1 | 1σ below mean | 15.87% |
| 0 | At mean | 50% |
| +1 | 1σ above mean | 84.13% |
| +2 | 2σ above mean | 97.72% |
| +3 | 3σ above mean | 99.87% |

### Example: Probability Calculation

**Problem:** Stock returns are normally distributed with mean 10% and volatility 20%. What's the probability of a loss (return < 0)?

**Solution:**
$$Z = \frac{0 - 0.10}{0.20} = \frac{-0.10}{0.20} = -0.5$$

Look up $P(Z < -0.5) = 0.3085 = 30.85\%$

### Log-Normal Distribution

If $\ln(X)$ is normally distributed, then $X$ is log-normally distributed.

$$f(x) = \frac{1}{x\sigma\sqrt{2\pi}} e^{-\frac{(\ln x - \mu)^2}{2\sigma^2}}$$

**Why Log-Normal for Prices?**
- Prices can't be negative
- Returns (log changes) are approximately normal
- Price = $P_0 \times e^{r}$ where $r$ is normal

### Fat Tails in Finance

Real financial returns have **fatter tails** than normal:

| Distribution | Kurtosis | Tail Behavior |
|--------------|----------|---------------|
| Normal | 3 | Thin tails |
| Student-t (low df) | > 3 | Fat tails |
| Financial Returns | 5-10 | Very fat tails |

**Implication:** Extreme events (crashes, spikes) occur more often than normal distribution predicts.

---

## 3. Hypothesis Testing

### The Framework

1. **Null Hypothesis ($H_0$):** Default assumption (usually "no effect")
2. **Alternative Hypothesis ($H_1$):** What we're testing for
3. **Test Statistic:** Calculated from data
4. **P-value:** Probability of observing data if $H_0$ is true
5. **Decision:** Reject $H_0$ if p-value < significance level (α)

### Type I and Type II Errors

| | $H_0$ True | $H_0$ False |
|---|-----------|------------|
| **Reject $H_0$** | Type I Error (α) | Correct |
| **Don't Reject** | Correct | Type II Error (β) |

- **Type I (α):** False positive - rejecting true null
- **Type II (β):** False negative - failing to reject false null
- **Power (1-β):** Probability of correctly rejecting false null

### T-Test: Testing Means

**One-Sample T-Test:** Is the mean different from a specified value?

$$t = \frac{\bar{x} - \mu_0}{s / \sqrt{n}}$$

Where:
- $\bar{x}$ = sample mean
- $\mu_0$ = hypothesized mean
- $s$ = sample standard deviation
- $n$ = sample size

**Degrees of Freedom:** $df = n - 1$

### Example: Testing Strategy Returns

**Problem:** A trading strategy produced these monthly returns: 2%, 3%, -1%, 4%, 1%, 2%. Is the true mean return significantly different from 0?

**Step 1: State hypotheses**
- $H_0: \mu = 0$ (strategy has no edge)
- $H_1: \mu \neq 0$ (strategy has an edge)

**Step 2: Calculate statistics**
- $\bar{x} = (2+3-1+4+1+2)/6 = 1.83\%$
- $s = 1.72\%$
- $n = 6$

**Step 3: Calculate t-statistic**
$$t = \frac{1.83 - 0}{1.72 / \sqrt{6}} = \frac{1.83}{0.70} = 2.61$$

**Step 4: Find p-value**
With df = 5, t = 2.61 gives p-value ≈ 0.048

**Step 5: Conclusion**
At α = 0.05, p-value < α, so **reject $H_0$**. The strategy return is significantly different from zero.

### Two-Sample T-Test

Comparing means of two groups:

$$t = \frac{\bar{x}_1 - \bar{x}_2}{\sqrt{\frac{s_1^2}{n_1} + \frac{s_2^2}{n_2}}}$$

### F-Test: Testing Variances

$$F = \frac{s_1^2}{s_2^2}$$

Under $H_0$: variances are equal, F follows F-distribution.

---

## 4. Regression Analysis

### Simple Linear Regression

Models the relationship between dependent variable Y and independent variable X.

$$Y = \alpha + \beta X + \epsilon$$

Where:
- $\alpha$ = intercept (Y when X = 0)
- $\beta$ = slope (change in Y per unit change in X)
- $\epsilon$ = error term (residual)

### Ordinary Least Squares (OLS)

OLS minimizes the sum of squared residuals:

$$\min_{\alpha, \beta} \sum_{i=1}^{n} (y_i - \alpha - \beta x_i)^2$$

### OLS Formulas

**Slope:**
$$\hat{\beta} = \frac{\sum_{i=1}^{n}(x_i - \bar{x})(y_i - \bar{y})}{\sum_{i=1}^{n}(x_i - \bar{x})^2} = \frac{\text{Cov}(X,Y)}{\text{Var}(X)}$$

**Intercept:**
$$\hat{\alpha} = \bar{y} - \hat{\beta}\bar{x}$$

### Step-by-Step Regression Example

**Problem:** Find the regression of Stock Return (Y) on Market Return (X)

| Observation | Market (X) | Stock (Y) |
|-------------|-----------|-----------|
| 1 | 2% | 3% |
| 2 | -1% | -2% |
| 3 | 3% | 4% |
| 4 | 1% | 1% |
| 5 | -2% | -3% |

**Step 1: Calculate means**
$$\bar{x} = 0.6\%, \quad \bar{y} = 0.6\%$$

**Step 2: Calculate deviations and products**
| i | $x_i - \bar{x}$ | $y_i - \bar{y}$ | Product | $(x_i - \bar{x})^2$ |
|---|-----------------|-----------------|---------|---------------------|
| 1 | 1.4% | 2.4% | 0.0336% | 0.0196% |
| 2 | -1.6% | -2.6% | 0.0416% | 0.0256% |
| 3 | 2.4% | 3.4% | 0.0816% | 0.0576% |
| 4 | 0.4% | 0.4% | 0.0016% | 0.0016% |
| 5 | -2.6% | -3.6% | 0.0936% | 0.0676% |
| **Sum** | | | **0.252%** | **0.172%** |

**Step 3: Calculate beta**
$$\hat{\beta} = \frac{0.252\%}{0.172\%} = 1.47$$

**Step 4: Calculate alpha**
$$\hat{\alpha} = 0.6\% - 1.47 \times 0.6\% = 0.6\% - 0.88\% = -0.28\%$$

**Interpretation:** Stock return = -0.28% + 1.47 × Market return

The stock has beta of 1.47 (more volatile than market) and slight negative alpha.

### R-Squared: Goodness of Fit

$$R^2 = 1 - \frac{SS_{residual}}{SS_{total}} = 1 - \frac{\sum(y_i - \hat{y}_i)^2}{\sum(y_i - \bar{y})^2}$$

**Interpretation:**
- $R^2 = 0$: Model explains nothing
- $R^2 = 1$: Model explains everything
- $R^2 = 0.8$: Model explains 80% of variance

### Multiple Regression

$$Y = \alpha + \beta_1 X_1 + \beta_2 X_2 + ... + \beta_k X_k + \epsilon$$

In matrix form:
$$\mathbf{Y} = \mathbf{X}\boldsymbol{\beta} + \boldsymbol{\epsilon}$$

OLS solution:
$$\hat{\boldsymbol{\beta}} = (\mathbf{X}'\mathbf{X})^{-1}\mathbf{X}'\mathbf{Y}$$

### Regression Assumptions (BLUE)

For OLS to be Best Linear Unbiased Estimator:

1. **Linearity:** Relationship is linear
2. **Independence:** Observations are independent
3. **Homoscedasticity:** Constant variance of errors
4. **Normality:** Errors are normally distributed
5. **No multicollinearity:** Independent variables not highly correlated

---

## 5. Maximum Likelihood Estimation

### The Concept

MLE finds parameter values that maximize the probability of observing the data.

$$\hat{\theta}_{MLE} = \arg\max_{\theta} L(\theta | data)$$

Where $L(\theta | data)$ is the likelihood function.

### Log-Likelihood

We typically maximize log-likelihood (easier to work with):

$$\ell(\theta) = \ln L(\theta) = \sum_{i=1}^{n} \ln f(x_i | \theta)$$

### MLE for Normal Distribution

Given data $x_1, ..., x_n$ from $N(\mu, \sigma^2)$:

**Likelihood:**
$$L(\mu, \sigma^2) = \prod_{i=1}^{n} \frac{1}{\sigma\sqrt{2\pi}} e^{-\frac{(x_i-\mu)^2}{2\sigma^2}}$$

**Log-Likelihood:**
$$\ell(\mu, \sigma^2) = -\frac{n}{2}\ln(2\pi) - \frac{n}{2}\ln(\sigma^2) - \frac{1}{2\sigma^2}\sum_{i=1}^{n}(x_i - \mu)^2$$

**MLE Solutions:**
$$\hat{\mu}_{MLE} = \bar{x} = \frac{1}{n}\sum_{i=1}^{n}x_i$$

$$\hat{\sigma}^2_{MLE} = \frac{1}{n}\sum_{i=1}^{n}(x_i - \bar{x})^2$$

Note: MLE variance uses $n$, not $n-1$ (biased but consistent).

---

## Key Formulas Summary

| Concept | Formula |
|---------|---------|
| Z-Score | $Z = \frac{X - \mu}{\sigma}$ |
| T-Statistic | $t = \frac{\bar{x} - \mu_0}{s/\sqrt{n}}$ |
| Regression Beta | $\hat{\beta} = \frac{\text{Cov}(X,Y)}{\text{Var}(X)}$ |
| R-Squared | $R^2 = 1 - \frac{SS_{res}}{SS_{tot}}$ |
| Normal PDF | $f(x) = \frac{1}{\sigma\sqrt{2\pi}}e^{-\frac{(x-\mu)^2}{2\sigma^2}}$ |
| Binomial | $P(X=k) = \binom{n}{k}p^k(1-p)^{n-k}$ |

---

## Practice Problems

1. Stock returns are N(8%, 15%). What's the probability of losing more than 10%?

2. A strategy's Sharpe ratio is 0.8 over 36 months. Is it significantly different from 0?

3. Run a regression of AAPL on SPY. Interpret the beta and alpha.

4. Given 5 returns: [3%, -1%, 2%, 4%, -2%], find MLE estimates for μ and σ.

---

*Next Week: Time Series Analysis*
