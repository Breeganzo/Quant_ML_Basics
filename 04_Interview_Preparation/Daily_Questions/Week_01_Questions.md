# Week 1 Daily Interview Questions

## Day 1: Python Fundamentals

### Question 1.1: List vs NumPy Array
**Company:** All firms  
**Difficulty:** Easy  
**Time:** 5 minutes

What's the difference between a Python list and a NumPy array for financial calculations?

<details>
<summary>Answer</summary>

**Key Differences:**

1. **Memory**: NumPy arrays are contiguous in memory; lists store pointers
2. **Speed**: NumPy uses vectorized operations (C under the hood); lists require loops
3. **Type**: NumPy arrays are homogeneous; lists can mix types
4. **Broadcasting**: NumPy supports broadcasting; lists don't

**For Finance:**
- Use NumPy for numerical calculations (returns, volatility)
- Use lists for heterogeneous data (ticker symbols, mixed types)
- NumPy is 10-100x faster for large datasets

```python
import numpy as np

# NumPy (fast)
returns_np = np.array([0.01, 0.02, -0.01, 0.03])
cumulative = np.cumprod(1 + returns_np) - 1

# List (slow)
returns_list = [0.01, 0.02, -0.01, 0.03]
cumulative_list = []
prod = 1
for r in returns_list:
    prod *= (1 + r)
    cumulative_list.append(prod - 1)
```

</details>

---

### Question 1.2: Time Complexity
**Company:** All firms  
**Difficulty:** Easy  
**Time:** 5 minutes

What's the time complexity of:
1. Appending to a Python list
2. Inserting at the beginning of a list
3. Looking up a value in a dictionary

<details>
<summary>Answer</summary>

1. **Append to list**: O(1) amortized
   - Occasionally O(n) when resizing needed
   
2. **Insert at beginning**: O(n)
   - Must shift all elements
   - Use `collections.deque` for O(1) prepend

3. **Dictionary lookup**: O(1) average
   - O(n) worst case (hash collisions)
   - Python uses well-tuned hash tables

</details>

---

## Day 2: Time Series

### Question 1.3: Forward Fill Risk
**Company:** Two Sigma, Citadel  
**Difficulty:** Medium  
**Time:** 10 minutes

Why is forward-filling missing data dangerous for prediction tasks?

<details>
<summary>Answer</summary>

**The Problem:**
Forward-fill uses future information at the time of filling, but the model doesn't know this data is "filled" vs "real."

**Example:**
```
Date        Price   Volume
2024-01-01  100     1000
2024-01-02  NaN     NaN     # Market closed
2024-01-03  102     1200

# After forward-fill:
2024-01-01  100     1000
2024-01-02  100     1000    # Looks like no change!
2024-01-03  102     1200
```

**Risks:**
1. **Look-ahead bias**: Model sees "stability" that wasn't observable
2. **Signal distortion**: Zero returns when actually missing
3. **Volume issues**: Filled volume isn't real liquidity

**Better Approaches:**
1. Flag missing data explicitly
2. Use different imputation for different purposes
3. Exclude missing periods from analysis
4. Use point-in-time data that respects when info was available

</details>

---

### Question 1.4: Log vs Simple Returns
**Company:** All firms  
**Difficulty:** Easy  
**Time:** 5 minutes

When should you use log returns vs simple returns?

<details>
<summary>Answer</summary>

**Log Returns:** $r_t = \ln(P_t / P_{t-1})$
- **Pros:**
  - Time-additive: Multi-period return = sum of single-period
  - More symmetric distribution
  - Better statistical properties (closer to normal)
- **Use when:** 
  - Statistical analysis
  - Multi-period cumulative calculations
  - Modeling (GARCH, etc.)

**Simple Returns:** $R_t = (P_t - P_{t-1}) / P_{t-1}$
- **Pros:**
  - Asset-additive: Portfolio return = weighted sum
  - Directly interpretable as P&L
- **Use when:**
  - Portfolio calculations
  - Performance reporting
  - P&L attribution

**Key Insight:**
For small returns (<5%), they're approximately equal:
$\ln(1 + R) \approx R$ when $R$ is small

</details>

---

## Day 3: Returns and Risk

### Question 1.5: Annualization
**Company:** Goldman Sachs, JPMorgan  
**Difficulty:** Easy  
**Time:** 5 minutes

How do you annualize:
1. Daily returns
2. Daily volatility
3. Daily Sharpe ratio

<details>
<summary>Answer</summary>

Assuming 252 trading days per year:

1. **Annualize returns:**
   - Compound: $(1 + r_{daily})^{252} - 1$
   - Approximate: $r_{daily} \times 252$

2. **Annualize volatility:**
   - $\sigma_{annual} = \sigma_{daily} \times \sqrt{252}$
   - Assumes returns are i.i.d. (variance scales linearly)

3. **Annualize Sharpe:**
   - $SR_{annual} = SR_{daily} \times \sqrt{252}$
   - Because: $SR = \frac{\mu}{\sigma}$, and $\frac{\mu \times 252}{\sigma \times \sqrt{252}} = SR \times \sqrt{252}$

**Common Pitfall:**
Volatility scales with $\sqrt{T}$, not $T$, due to random walk property.

</details>

---

### Question 1.6: VaR Calculation
**Company:** Goldman Sachs, JPMorgan  
**Difficulty:** Medium  
**Time:** 10 minutes

A portfolio has daily returns with mean 0.05% and standard deviation 2%. Calculate 1-day 95% VaR.

<details>
<summary>Answer</summary>

**Parametric VaR (assuming normal distribution):**

VaR at 95% = $-(\mu - z_{0.95} \times \sigma)$

Where $z_{0.95} = 1.645$ (one-tailed)

VaR = $-(0.0005 - 1.645 \times 0.02)$
VaR = $-0.0005 + 0.0329$
VaR = $0.0324$ or **3.24%**

**Interpretation:** 
With 95% confidence, the portfolio won't lose more than 3.24% in one day.

**Alternative (Historical VaR):**
Sort historical returns and take the 5th percentile.

**Key Considerations:**
- VaR doesn't tell you how bad losses can be beyond the threshold
- Use CVaR (Expected Shortfall) for tail risk
- Assumes normal distribution (fat tails in reality)

</details>

---

## Day 4: Correlation

### Question 1.7: Correlation Breakdown
**Company:** Jane Street, Citadel  
**Difficulty:** Medium  
**Time:** 10 minutes

Why do correlations between assets tend to increase during market crashes?

<details>
<summary>Answer</summary>

**Reasons:**

1. **Flight to safety**: All risky assets sold simultaneously
2. **Leverage unwinding**: Forced selling across positions
3. **Liquidity crunch**: Market makers pull back everywhere
4. **Contagion**: Losses in one asset force sales in others
5. **Investor behavior**: Panic affects all positions

**Implications for Risk Management:**

1. **Diversification fails when needed most**
2. **Correlation matrices should be estimated conditionally**
3. **Stress testing should use crisis correlations**
4. **Don't rely solely on historical correlations**

**Quantitative Approaches:**
- Regime-switching models (HMM)
- DCC-GARCH for dynamic correlations
- Copulas for tail dependence
- Conditional correlation estimation

</details>

---

## Day 5: Visualization

### Question 1.8: Chart Selection
**Company:** All firms  
**Difficulty:** Easy  
**Time:** 5 minutes

What chart type would you use to show:
1. Stock price over time
2. Return distribution
3. Correlation matrix
4. Strategy drawdowns

<details>
<summary>Answer</summary>

1. **Stock price over time:**
   - Line chart (basic)
   - Candlestick/OHLC (detailed)
   - Add moving averages for context

2. **Return distribution:**
   - Histogram with density overlay
   - QQ-plot vs normal (check normality)
   - Box plot for outliers

3. **Correlation matrix:**
   - Heatmap (seaborn, matplotlib)
   - Clustermap for grouped assets
   - Values annotated in cells

4. **Strategy drawdowns:**
   - Underwater plot (area chart below zero)
   - Show drawdown magnitude and duration
   - Mark max drawdown point

</details>

---

## Day 6-7: Practice Problems

### Question 1.9: Coding Challenge
**Company:** All firms  
**Difficulty:** Medium  
**Time:** 20 minutes

Implement a function to calculate rolling Sharpe ratio.

```python
def rolling_sharpe(returns: pd.Series, window: int = 252, 
                   risk_free: float = 0.0) -> pd.Series:
    """
    Calculate rolling Sharpe ratio.
    
    Args:
        returns: Daily returns series
        window: Rolling window size
        risk_free: Annualized risk-free rate
    
    Returns:
        Rolling annualized Sharpe ratio
    """
    # Your implementation here
    pass
```

<details>
<summary>Solution</summary>

```python
def rolling_sharpe(returns: pd.Series, window: int = 252,
                   risk_free: float = 0.0) -> pd.Series:
    """
    Calculate rolling Sharpe ratio.
    """
    # Convert annual risk-free to daily
    rf_daily = (1 + risk_free) ** (1/252) - 1
    
    # Excess returns
    excess = returns - rf_daily
    
    # Rolling mean and std
    rolling_mean = excess.rolling(window).mean()
    rolling_std = returns.rolling(window).std()
    
    # Daily Sharpe
    daily_sharpe = rolling_mean / rolling_std
    
    # Annualize
    annual_sharpe = daily_sharpe * np.sqrt(252)
    
    return annual_sharpe
```

</details>

---

### Question 1.10: Brain Teaser
**Company:** Jane Street  
**Difficulty:** Medium  
**Time:** 10 minutes

You're offered a game: flip a fair coin. Heads you win $2, tails you lose $1. What's the expected value? How much should you pay to play?

<details>
<summary>Answer</summary>

**Expected Value:**
$E[X] = 0.5 \times \$2 + 0.5 \times (-\$1) = \$1 - \$0.50 = \$0.50$

**How much to pay:**
- Any amount less than $0.50 is profitable in expectation
- At exactly $0.50, you break even
- Risk-averse players might pay less due to variance

**Follow-up questions:**
1. If you can only play once, does EV change? (No, but utility might)
2. What if you can play 1000 times? (Variance becomes negligible)
3. What if wins are capped? (Changes EV calculation)

</details>

---

## Weekly Summary

| Day | Topic | Questions | Focus |
|-----|-------|-----------|-------|
| 1 | Python | 2 | Data structures, efficiency |
| 2 | Time Series | 2 | Missing data, returns |
| 3 | Risk | 2 | VaR, annualization |
| 4 | Correlation | 1 | Diversification |
| 5 | Visualization | 1 | Chart selection |
| 6-7 | Practice | 2 | Coding, brain teasers |

**Total Questions Completed:** ___ / 10
