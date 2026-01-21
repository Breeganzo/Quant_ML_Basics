# Week 2: Statistics & Probability for Quantitative Finance

## Overview
This week covers essential statistical concepts and probability theory crucial for quantitative finance. You'll learn the mathematical foundations used in risk modeling, strategy development, and financial analysis.

---

## Day 1: Probability Distributions in Finance

### Discrete Distributions
- **Binomial**: Number of up/down days in n trading days
- **Poisson**: Rare events (defaults, extreme moves)

### Continuous Distributions
- **Normal (Gaussian)**: Central assumption in many models
- **Log-Normal**: Stock prices (prices can't be negative)
- **Student-t**: Heavy tails, better for financial returns
- **Chi-squared**: Variance estimation, risk metrics

### Key Formulas
```
Normal PDF: f(x) = (1/√(2πσ²)) * exp(-(x-μ)²/(2σ²))
Log-Normal: If X ~ N(μ,σ²), then Y = e^X ~ LogNormal
Student-t: Heavier tails, df parameter controls tail weight
```

### Why This Matters
- Financial returns are NOT normal (fat tails, skewness)
- Using wrong distribution underestimates tail risk
- Student-t with ~4-5 df better models equity returns

---

## Day 2: Moments and Descriptive Statistics

### The Four Moments
1. **Mean (μ)**: Expected return
2. **Variance (σ²)**: Risk/Dispersion
3. **Skewness**: Asymmetry (negative = more extreme losses)
4. **Kurtosis**: Tail heaviness (excess > 0 = fat tails)

### Sample vs Population
```python
# Sample statistics (use n-1 for unbiased)
sample_mean = sum(x) / n
sample_var = sum((x - mean)²) / (n-1)  # Bessel's correction

# Standard Error of Mean
SEM = σ / √n
```

### Key Insight for Finance
- Stock returns: Negative skew (~-0.5), Excess kurtosis (~3-10)
- This means: More extreme losses than gains, and more extreme events overall

---

## Day 3: Hypothesis Testing for Trading

### Framework
1. **Null Hypothesis (H₀)**: Strategy has zero alpha
2. **Alternative (H₁)**: Strategy has positive alpha
3. **Test Statistic**: t = (observed - expected) / SE
4. **P-value**: Probability of seeing this result if H₀ true

### Common Tests in Finance
```
t-test for mean: Is strategy return significantly different from zero?
  t = (x̄ - μ₀) / (s/√n)
  
F-test for variance: Compare volatilities of two portfolios
  F = s₁² / s₂²

Jarque-Bera: Are returns normally distributed?
  JB = (n/6) * [S² + (K-3)²/4]  (S=skew, K=kurtosis)
```

### Multiple Testing Problem
- Running 100 backtests → expect 5 "significant" by chance (at α=0.05)
- Bonferroni correction: α_adjusted = α / number_of_tests
- False Discovery Rate (FDR): More sophisticated approach

---

## Day 4: Correlation and Dependence

### Pearson Correlation
```
ρ = Cov(X,Y) / (σ_X * σ_Y)
```
- Measures LINEAR relationship only
- Range: [-1, 1]

### Rank Correlations
- **Spearman**: Correlation of ranks (monotonic relationships)
- **Kendall's Tau**: Based on concordant/discordant pairs

### Limitations
1. Correlation ≠ Causation
2. Correlation is not stable (changes over time)
3. Correlation increases during crises
4. Zero correlation ≠ Independence

### Copulas (Advanced)
- Model dependence structure separately from marginals
- Capture tail dependence
- Used in credit risk, portfolio modeling

---

## Day 5: Central Limit Theorem & Confidence Intervals

### Central Limit Theorem (CLT)
For n independent samples from ANY distribution with mean μ and variance σ²:
```
x̄ ~ N(μ, σ²/n) as n → ∞
```

### Applications in Finance
1. Portfolio returns (sum of many assets) → approximately normal
2. Averaging over time reduces estimation error
3. Foundation for many statistical tests

### Confidence Intervals
```
95% CI for mean: x̄ ± 1.96 * (s/√n)
99% CI for mean: x̄ ± 2.576 * (s/√n)

For Sharpe Ratio:
SE(SR) ≈ √[(1 + 0.5*SR²)/n]  # approximation
```

### Bootstrap Confidence Intervals
- Resample with replacement
- Calculate statistic for each resample
- Use percentiles for CI
- Works for ANY statistic (no formula needed)

---

## Day 6: Bayesian Thinking in Finance

### Bayes' Theorem
```
P(A|B) = P(B|A) * P(A) / P(B)

Posterior ∝ Likelihood × Prior
```

### Applications
1. **Updating beliefs**: Prior return expectation + new data → posterior
2. **Black-Litterman Model**: Combine market equilibrium with views
3. **Signal combination**: How to weight multiple alpha signals

### Example: Strategy Evaluation
```
Prior: 95% of strategies don't work (P(bad) = 0.95)
Backtest: "Significant" at 5% level

P(bad|significant) = P(sig|bad) * P(bad) / P(sig)
                   = 0.05 * 0.95 / P(sig)
                   ≈ 0.76  (still 76% chance strategy is bad!)
```

### Key Insight
- Extraordinary claims require extraordinary evidence
- A single "significant" backtest is weak evidence

---

## Day 7: Interview Questions & Practice

### Common Interview Topics
1. Explain the Law of Large Numbers vs CLT
2. Why are stock returns not normally distributed?
3. How would you test if a trading strategy works?
4. What's the problem with multiple hypothesis testing?
5. Explain Bayesian updating with an example

### Probability Puzzles
- Expected value problems
- Conditional probability
- Order statistics

---

## Key Formulas Summary

| Concept | Formula |
|---------|---------|
| Mean | μ = E[X] = Σx·P(x) |
| Variance | σ² = E[(X-μ)²] = E[X²] - μ² |
| Covariance | Cov(X,Y) = E[(X-μx)(Y-μy)] |
| Correlation | ρ = Cov(X,Y)/(σx·σy) |
| Standard Error | SE = σ/√n |
| t-statistic | t = (x̄ - μ₀)/(s/√n) |
| Sharpe Ratio | SR = (R - Rf)/σ |
| Skewness | S = E[(X-μ)³]/σ³ |
| Kurtosis | K = E[(X-μ)⁴]/σ⁴ |

---

## Reading List
- "Statistics and Data Analysis for Financial Engineering" - Ruppert & Matteson
- "The Concepts and Practice of Mathematical Finance" - Joshi
- "Quantitative Risk Management" - McNeil, Frey & Embrechts

---

## Week 2 Project
**Statistical Analysis of Strategy Returns**
- Analyze return distribution of a momentum strategy
- Test for significance using multiple methods
- Bootstrap confidence intervals for Sharpe ratio
- Document findings and limitations
