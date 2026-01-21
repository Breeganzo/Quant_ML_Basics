# Prerequisites Self-Assessment

**Purpose:** Evaluate your readiness for this 24-week intensive program.  
**Time Required:** 2-3 hours to complete honestly.  
**Scoring:** Be brutally honest—gaps identified now are gaps fixed before interviews.

---

## 📊 Scoring Summary

| Section | Points Available | Your Score | Required |
|---------|-----------------|------------|----------|
| 1. Python Programming | 150 | ___ / 150 | 120+ (80%) |
| 2. Mathematics | 100 | ___ / 100 | 70+ (70%) |
| 3. Probability & Statistics | 100 | ___ / 100 | 75+ (75%) |
| 4. Finance Basics | 100 | ___ / 100 | 60+ (60%) |
| 5. Tools & Environment | 100 | ___ / 100 | 90+ (90%) |
| **TOTAL** | **550** | ___ / 550 | **415+ (75%)** |

### Interpretation

| Total Score | Readiness | Action |
|-------------|-----------|--------|
| 450+ (82%+) | ✅ Excellent | Start immediately |
| 385-449 (70-81%) | ⚠️ Good | Review weak sections for 1-2 weeks |
| 330-384 (60-69%) | ⚠️ Gaps | Complete prep resources for 2-4 weeks |
| <330 (<60%) | ❌ Not Ready | Build fundamentals first (1-2 months) |

---

## Section 1: Python Programming (150 points)

### 1.1 NumPy Operations (40 points)

**Rate yourself 0-10 on each (0=never seen, 10=teach others):**

| Skill | Score (0-10) |
|-------|--------------|
| Array creation (zeros, ones, arange, linspace) | ___ |
| Array indexing and slicing | ___ |
| Broadcasting rules | ___ |
| Vectorized operations (no loops) | ___ |

**Total: ___ / 40**

<details>
<summary>📝 Validation Problems (click to expand)</summary>

**Problem 1.1.1:** Create a 252×10 array of random returns (mean=0.0005, std=0.02), calculate cumulative returns for each column.

```python
# Your solution:



# Expected output: Array of shape (252, 10) with cumulative products
```

**Problem 1.1.2:** Given a 1D array of prices, calculate log returns without using loops.

```python
prices = np.array([100, 102, 99, 103, 105, 101])
# Your solution:



# Expected: array([ 0.0198, -0.0299,  0.0396,  0.0193, -0.0388])
```

**Problem 1.1.3:** Implement a rolling mean using only NumPy (no pandas).

```python
def rolling_mean_numpy(arr, window):
    # Your solution:
    pass
```

</details>

---

### 1.2 Pandas Time Series (40 points)

**Rate yourself 0-10 on each:**

| Skill | Score (0-10) |
|-------|--------------|
| DataFrame creation and manipulation | ___ |
| Time series indexing (DatetimeIndex) | ___ |
| Resampling (daily to monthly, etc.) | ___ |
| Rolling window operations | ___ |

**Total: ___ / 40**

<details>
<summary>📝 Validation Problems</summary>

**Problem 1.2.1:** Download AAPL data using yfinance, calculate 20-day rolling volatility (annualized), and resample to monthly.

```python
# Your solution:




```

**Problem 1.2.2:** Given a DataFrame with columns ['open', 'high', 'low', 'close', 'volume'], calculate:
- Daily returns
- 5-day momentum (close[t] / close[t-5] - 1)
- Volume-weighted average price (VWAP)

```python
# Your solution:



```

**Problem 1.2.3:** Handle missing data: forward-fill prices but NOT returns (explain why).

```python
# Your solution + explanation:



```

</details>

---

### 1.3 Functions and Classes (40 points)

**Rate yourself 0-10 on each:**

| Skill | Score (0-10) |
|-------|--------------|
| Function definition with type hints | ___ |
| Class definition and inheritance | ___ |
| Decorators (@property, @staticmethod) | ___ |
| Exception handling (try/except) | ___ |

**Total: ___ / 40**

<details>
<summary>📝 Validation Problems</summary>

**Problem 1.3.1:** Create a `Portfolio` class with:
- Constructor taking list of tickers and weights
- Method `returns(prices_df)` calculating portfolio returns
- Property `is_valid` checking weights sum to 1.0

```python
# Your solution:



```

**Problem 1.3.2:** Write a decorator `@timer` that prints execution time of any function.

```python
# Your solution:



```

**Problem 1.3.3:** Implement a `TradingStrategy` abstract base class with methods `generate_signals()` and `backtest()`.

```python
# Your solution:



```

</details>

---

### 1.4 Data Visualization (30 points)

**Rate yourself 0-10 on each:**

| Skill | Score (0-10) |
|-------|--------------|
| Matplotlib basics (line, scatter, bar) | ___ |
| Subplots and figure customization | ___ |
| Seaborn for statistical plots | ___ |

**Total: ___ / 30**

<details>
<summary>📝 Validation Problems</summary>

**Problem 1.4.1:** Create a 2×2 subplot showing:
- Top-left: Price chart with 20-day MA
- Top-right: Returns histogram with normal fit
- Bottom-left: Rolling 20-day volatility
- Bottom-right: Drawdown chart

```python
# Your solution:



```

</details>

---

## Section 2: Mathematics (100 points)

### 2.1 Linear Algebra (50 points)

**Rate yourself 0-10 on each:**

| Concept | Score (0-10) |
|---------|--------------|
| Matrix multiplication and transpose | ___ |
| Matrix inverse and determinant | ___ |
| Eigenvalues and eigenvectors | ___ |
| Singular Value Decomposition (SVD) | ___ |
| Quadratic forms (x'Ax) | ___ |

**Total: ___ / 50**

<details>
<summary>📝 Validation Problems</summary>

**Problem 2.1.1:** Given a covariance matrix Σ, derive the variance of a portfolio with weights w.

$$\sigma_p^2 = ?$$

**Problem 2.1.2:** Explain why PCA uses eigendecomposition of the covariance matrix.

**Problem 2.1.3:** For a matrix A, when does $(A'A)^{-1}A'$ give the least squares solution?

**Problem 2.1.4:** Calculate by hand:
$$\begin{bmatrix} 2 & 1 \\ 1 & 3 \end{bmatrix}^{-1}$$

</details>

---

### 2.2 Calculus & Optimization (50 points)

**Rate yourself 0-10 on each:**

| Concept | Score (0-10) |
|---------|--------------|
| Derivatives and chain rule | ___ |
| Partial derivatives | ___ |
| Gradient descent intuition | ___ |
| Lagrange multipliers | ___ |
| Convexity and local minima | ___ |

**Total: ___ / 50**

<details>
<summary>📝 Validation Problems</summary>

**Problem 2.2.1:** Derive the gradient of the OLS loss function:
$$L(\beta) = \|y - X\beta\|^2$$

**Problem 2.2.2:** Why does Ridge regression have a closed-form solution but Lasso doesn't?

**Problem 2.2.3:** Explain the gradient descent update rule and learning rate selection.

**Problem 2.2.4:** Set up the Lagrangian for minimizing portfolio variance subject to weights summing to 1.

</details>

---

## Section 3: Probability & Statistics (100 points)

### 3.1 Probability (50 points)

**Rate yourself 0-10 on each:**

| Concept | Score (0-10) |
|---------|--------------|
| Conditional probability | ___ |
| Bayes' theorem | ___ |
| Expected value and variance | ___ |
| Common distributions (Normal, Poisson, Binomial) | ___ |
| Law of large numbers / CLT | ___ |

**Total: ___ / 50**

<details>
<summary>📝 Validation Problems</summary>

**Problem 3.1.1:** A trading strategy has 55% win rate. What's the probability of having 3 consecutive losses?

**Problem 3.1.2:** Bayes' theorem: If P(market up | good earnings) = 0.7, P(good earnings) = 0.4, and P(market up) = 0.5, what is P(good earnings | market up)?

**Problem 3.1.3:** Calculate E[X] and Var[X] for X ~ Poisson(λ).

**Problem 3.1.4:** A stock has daily returns ~ N(0.05%, 2%). What's the probability of losing more than 5% in a day?

**Problem 3.1.5:** You flip a fair coin. If heads, you win $2. If tails, you flip again. If heads on second flip, you win $1. Otherwise $0. What's E[winnings]?

</details>

---

### 3.2 Statistics (50 points)

**Rate yourself 0-10 on each:**

| Concept | Score (0-10) |
|---------|--------------|
| Hypothesis testing (null, alternative, p-value) | ___ |
| t-tests and confidence intervals | ___ |
| Linear regression interpretation | ___ |
| R², adjusted R², F-statistic | ___ |
| Correlation vs. causation | ___ |

**Total: ___ / 50**

<details>
<summary>📝 Validation Problems</summary>

**Problem 3.2.1:** A backtest shows Sharpe = 1.5 over 2 years of daily data. Is this statistically significant at 5%?

**Problem 3.2.2:** Interpret: β₁ = 0.8 with t-stat = 2.5 in a regression of stock returns on market returns.

**Problem 3.2.3:** What's the difference between R² = 0.10 and R² = 0.90 in a factor model? When is 0.10 actually good?

**Problem 3.2.4:** Your strategy has positive returns correlated with VIX. Is this alpha or risk premium?

</details>

---

## Section 4: Finance Basics (100 points)

### 4.1 Asset Classes & Instruments (25 points)

**Rate yourself 0-5 on knowledge of each:**

| Instrument | Score (0-5) |
|------------|-------------|
| Equities (stocks, indices, ETFs) | ___ |
| Fixed income (bonds, rates, credit) | ___ |
| Derivatives (options, futures, swaps) | ___ |
| FX (currency pairs, crosses) | ___ |
| Commodities | ___ |

**Total: ___ / 25**

<details>
<summary>📝 Validation Questions</summary>

1. What's the difference between a stock and an ETF?
2. Why do bond prices move inversely to interest rates?
3. Define: call option, put option, strike price, expiration.
4. What does EUR/USD = 1.10 mean?
5. What's contango vs. backwardation in futures?

</details>

---

### 4.2 Risk and Return (25 points)

**Rate yourself 0-5 on each:**

| Concept | Score (0-5) |
|---------|-------------|
| Return calculation (simple, log) | ___ |
| Volatility (realized, implied) | ___ |
| Sharpe ratio interpretation | ___ |
| Maximum drawdown | ___ |
| Beta and market risk | ___ |

**Total: ___ / 25**

<details>
<summary>📝 Validation Questions</summary>

1. Why do we use log returns for multi-period analysis?
2. Sharpe = 1.0. What does this mean in practical terms?
3. How do you annualize daily volatility?
4. What's the difference between VaR and max drawdown?
5. A stock has β = 1.5. What happens if market drops 10%?

</details>

---

### 4.3 Options Basics (25 points)

**Rate yourself 0-5 on each:**

| Concept | Score (0-5) |
|---------|-------------|
| Call/put payoff diagrams | ___ |
| Put-call parity | ___ |
| Greeks intuition (delta, gamma) | ___ |
| Implied volatility | ___ |
| Basic option strategies | ___ |

**Total: ___ / 25**

<details>
<summary>📝 Validation Questions</summary>

1. Draw the payoff diagram for a long call with strike $100.
2. State put-call parity formula.
3. What does delta = 0.5 mean for a call option?
4. Why is implied volatility often called the "fear gauge"?
5. Construct a bull spread using calls.

</details>

---

### 4.4 Market Efficiency & Factors (25 points)

**Rate yourself 0-5 on each:**

| Concept | Score (0-5) |
|---------|-------------|
| Efficient Market Hypothesis (weak, semi-strong, strong) | ___ |
| Factor investing (value, momentum, quality) | ___ |
| Alpha vs. beta | ___ |
| Transaction costs impact | ___ |
| Behavioral finance basics | ___ |

**Total: ___ / 25**

<details>
<summary>📝 Validation Questions</summary>

1. What's the difference between weak and strong form EMH?
2. What is the Fama-French 3-factor model?
3. If your strategy has alpha = 2% and beta = 0, what does that mean?
4. How do transaction costs affect strategy Sharpe ratio?
5. Name two behavioral biases that create trading opportunities.

</details>

---

## Section 5: Tools & Environment (100 points)

### 5.1 Jupyter Notebooks (20 points)

**Rate yourself 0-10 on each:**

| Skill | Score (0-10) |
|-------|--------------|
| Cell execution and kernel management | ___ |
| Markdown formatting (headers, LaTeX) | ___ |

**Total: ___ / 20**

---

### 5.2 Git & GitHub (20 points)

**Rate yourself 0-10 on each:**

| Skill | Score (0-10) |
|-------|--------------|
| Basic commands (clone, add, commit, push, pull) | ___ |
| Branching and merging | ___ |

**Total: ___ / 20**

<details>
<summary>📝 Validation</summary>

Execute these commands from memory:
1. Clone a repo
2. Create a new branch
3. Make changes, commit, push
4. Create a pull request (describe the process)

</details>

---

### 5.3 Terminal / Command Line (20 points)

**Rate yourself 0-10 on each:**

| Skill | Score (0-10) |
|-------|--------------|
| Navigation (cd, ls, pwd, mkdir) | ___ |
| File operations (cp, mv, rm, cat, grep) | ___ |

**Total: ___ / 20**

---

### 5.4 Virtual Environments (20 points)

**Rate yourself 0-10 on each:**

| Skill | Score (0-10) |
|-------|--------------|
| Creating environments (venv, conda) | ___ |
| Installing packages (pip, conda) | ___ |

**Total: ___ / 20**

<details>
<summary>📝 Validation</summary>

From memory:
1. Create a new conda environment with Python 3.10
2. Activate it
3. Install pandas, numpy, scikit-learn
4. Export requirements.txt

</details>

---

### 5.5 Debugging (20 points)

**Rate yourself 0-10 on each:**

| Skill | Score (0-10) |
|-------|--------------|
| Print debugging and logging | ___ |
| Using debugger (breakpoints, step through) | ___ |

**Total: ___ / 20**

---

## 🕐 Time Commitment Reality Check

Answer honestly:

| Question | Yes / No |
|----------|----------|
| Can you dedicate 4-6 hours EVERY weekday for 6 months? | ___ |
| Can you dedicate 10-14 hours on weekends? | ___ |
| Will you code EVERY SINGLE DAY for 24 weeks? | ___ |
| Can you eliminate distractions during study time? | ___ |
| Do you have support (family, roommates) for this commitment? | ___ |

**If ANY answer is "No":** Adjust timeline or expectations before starting.

---

## 📚 Remediation Resources

### If Python score < 120:
- Complete "Python for Data Science" on DataCamp (10-15 hours)
- Work through "Python Crash Course" chapters 1-10 (20 hours)

### If Math score < 70:
- Khan Academy Linear Algebra (15-20 hours)
- 3Blue1Brown "Essence of Linear Algebra" YouTube series (4 hours)
- MIT OCW 18.01 Single Variable Calculus (selected lectures)

### If Probability/Stats score < 75:
- Khan Academy Statistics and Probability (20 hours)
- "Think Stats" by Allen Downey (free online)
- MIT OCW 18.05 Introduction to Probability (selected lectures)

### If Finance score < 60:
- Investopedia tutorials (10 hours)
- "Options, Futures, and Other Derivatives" Hull Ch. 1-5 (20 hours)
- "A Random Walk Down Wall Street" (audiobook while commuting)

### If Tools score < 90:
- Git: Complete "Learn Git Branching" interactive tutorial (3 hours)
- Terminal: Linux Command Line Basics on Udacity (5 hours)
- Practice daily until comfortable

---

## ✍️ Final Assessment

**Date Completed:** _______________

**Total Score:** ___ / 550 (___ %)

**Weakest Area:** _______________

**Action Plan:**
1. _______________
2. _______________
3. _______________

**Planned Start Date:** _______________

**Signature (commitment to yourself):** _______________

---

*"An honest assessment today prevents failure tomorrow."*
