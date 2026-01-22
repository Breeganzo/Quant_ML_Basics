# Week 12: Backtesting, Transaction Costs & Walk-Forward Validation

## Table of Contents
1. [Performance Metrics](#1-performance-metrics)
2. [Transaction Costs](#2-transaction-costs)
3. [Walk-Forward Validation](#3-walk-forward-validation)
4. [Backtesting Best Practices](#4-backtesting-best-practices)
5. [Common Pitfalls](#5-common-pitfalls)

---

## 1. Performance Metrics

### Why Proper Metrics Matter

In quantitative finance, choosing the right performance metrics determines whether you're evaluating strategies correctly. Different metrics capture different aspects of risk and return.

### Sharpe Ratio

**Definition:** Risk-adjusted return using total volatility.

$$SR = \frac{E[R - R_f]}{\sigma_R} \times \sqrt{252}$$

Where:
- $E[R - R_f]$ = Expected excess return over risk-free rate
- $\sigma_R$ = Standard deviation of returns
- $\sqrt{252}$ = Annualization factor (252 trading days)

**Example:**
```
Daily return: 0.05%
Daily volatility: 1.5%
Risk-free rate: 0%

Sharpe = (0.0005 / 0.015) × √252 = 0.033 × 15.87 = 0.53
```

**Interpretation:**
| Sharpe Ratio | Quality |
|--------------|---------|
| < 0 | Losing money |
| 0 - 0.5 | Poor |
| 0.5 - 1.0 | Acceptable |
| 1.0 - 2.0 | Good |
| 2.0 - 3.0 | Very Good |
| > 3.0 | Excellent (verify for overfitting) |

**Limitations:**
- Assumes normally distributed returns
- Penalizes upside and downside volatility equally
- Sensitive to measurement period

### Sortino Ratio

**Definition:** Risk-adjusted return using only downside volatility.

$$Sortino = \frac{E[R - R_f]}{\sigma_{downside}} \times \sqrt{252}$$

Where:
$$\sigma_{downside} = \sqrt{\frac{1}{N}\sum_{r_i < 0}(r_i - 0)^2}$$

**Why Use Sortino?**
- Investors care more about losses than gains
- Doesn't penalize positive volatility
- Better for asymmetric return distributions

### Maximum Drawdown (MDD)

**Definition:** Largest peak-to-trough decline before a new peak.

$$MDD = \max_{t \in [0,T]} \left(\frac{\text{Peak}_t - \text{Value}_t}{\text{Peak}_t}\right)$$

**Step-by-Step Calculation:**
1. Calculate cumulative returns
2. Track running maximum (peak)
3. Calculate drawdown at each point
4. Find maximum drawdown

**Example:**
```
Portfolio values: [100, 110, 105, 95, 108, 115]
Peaks:           [100, 110, 110, 110, 110, 115]
Drawdowns:       [0%, 0%, -4.5%, -13.6%, -1.8%, 0%]

Maximum Drawdown = -13.6%
```

### Calmar Ratio

**Definition:** Annual return divided by maximum drawdown.

$$Calmar = \frac{R_{annual}}{|MDD|}$$

**Rule of Thumb:** Calmar > 1 is generally acceptable.

### Win Rate and Profit Factor

**Win Rate:**
$$Win\ Rate = \frac{\text{Number of Winning Trades}}{\text{Total Trades}}$$

**Profit Factor:**
$$Profit\ Factor = \frac{\text{Gross Profits}}{\text{Gross Losses}}$$

| Profit Factor | Interpretation |
|---------------|----------------|
| < 1.0 | Losing strategy |
| 1.0 - 1.5 | Break-even to marginal |
| 1.5 - 2.0 | Good |
| > 2.0 | Excellent |

---

## 2. Transaction Costs

### Why Costs Kill Strategies

Many strategies look profitable in backtest but fail live due to transaction costs. A strategy with 10 bps daily return and 20 bps round-trip cost loses money!

### Cost Components

**1. Commission/Brokerage Fees**
- Fixed fee per trade or per share
- Example: $0.005 per share

**2. Bid-Ask Spread**
- Cost of crossing the spread
- Liquid stocks: 1-5 bps
- Illiquid stocks: 20-100+ bps

**3. Slippage**
- Difference between expected and executed price
- Increases with order size and market volatility

**4. Market Impact**
- Large orders move prices against you
- Modeled as: $Impact = \eta \times \sigma \times \sqrt{\frac{V}{ADV}}$
- Where V = order volume, ADV = average daily volume

### Cost Modeling

**Simple Model (Fixed Costs):**
$$Net\ Return = Gross\ Return - Cost \times |Position\ Change|$$

**More Realistic Model:**
$$Cost_{total} = Commission + \frac{Spread}{2} + Slippage + Impact$$

### Rule of Thumb for Costs

| Asset Class | Round-Trip Cost (bps) |
|-------------|----------------------|
| Large-cap US stocks | 5-15 |
| Mid-cap stocks | 15-30 |
| Small-cap stocks | 30-100+ |
| Futures (liquid) | 1-5 |
| Options | 10-50 |
| Crypto | 10-50 |

### Break-Even Analysis

$$\text{Break-even Sharpe} = \frac{Cost \times Turnover}{\sigma} \times \sqrt{252}$$

**Example:**
- Cost = 10 bps round-trip
- Turnover = 100% daily (full rebalance)
- Daily volatility = 1%

Break-even Sharpe = (0.001 × 1) / 0.01 × √252 = 1.59

**Conclusion:** Strategy needs Sharpe > 1.59 just to cover costs!

---

## 3. Walk-Forward Validation

### The Problem with K-Fold CV

Standard K-Fold cross-validation shuffles data, which:
- **Destroys temporal structure**
- **Creates lookahead bias** (using future data to predict past)
- **Overestimates performance**

### Walk-Forward Solution

Train on historical data, test on future data, then roll forward.

```
Window 1: |---Train---|--Test--|
Window 2:    |---Train---|--Test--|
Window 3:       |---Train---|--Test--|
```

### Implementation Variants

**1. Expanding Window**
- Training set grows over time
- Uses all available historical data
- More data but older patterns may not be relevant

```
Train: |--------|      Test: |--|
Train: |-----------|   Test:    |--|
Train: |--------------|Test:       |--|
```

**2. Rolling Window**
- Fixed-size training window
- More recent data only
- Adapts to regime changes

```
Train: |--------|     Test: |--|
Train:    |--------|  Test:    |--|
Train:       |--------| Test:      |--|
```

### Embargo/Gap Period

**Why Add a Gap?**
- Labels may use future information (e.g., target is next day's return)
- Features may have lookahead in calculation
- Prevents information leakage

```
Train: |--------|  [Gap]  Test: |--|
```

**Typical Gap Sizes:**
- Daily data: 1-5 days
- Minute data: 1-2 hours
- Depends on prediction horizon

### Purging and Combinatorial CV

**Purging:** Remove training samples that overlap with test samples.

**Combinatorial Purged CV (CPCV):**
- Advanced technique from "Advances in Financial Machine Learning"
- Creates non-overlapping paths through data
- Reduces overfitting risk

### Time Series Split (sklearn)

```python
from sklearn.model_selection import TimeSeriesSplit

tscv = TimeSeriesSplit(n_splits=5)
for train_idx, test_idx in tscv.split(X):
    X_train, X_test = X[train_idx], X[test_idx]
    y_train, y_test = y[train_idx], y[test_idx]
```

---

## 4. Backtesting Best Practices

### Data Quality

**Point-in-Time Data:**
- Use data as it existed at the time
- Avoid revised economic data
- Handle stock splits and dividends correctly

**Survivorship Bias:**
- Include delisted stocks
- Don't only test on current index constituents

### Realistic Assumptions

**Trading Costs:**
- Include commission, spread, slippage
- Scale costs with order size

**Capacity:**
- Can you actually execute the strategy at this size?
- Market impact grows with AUM

**Execution:**
- You can't always trade at close price
- Use VWAP or mid-price assumptions

### Sanity Checks

1. **Is the Sharpe too good?** (> 3 is suspicious)
2. **Does it survive with costs?**
3. **Is turnover realistic?**
4. **Does it work out-of-sample?**
5. **Is there a reasonable economic explanation?**

### Multiple Testing Correction

When testing many strategies, some will be profitable by chance.

**Bonferroni Correction:**
$$\alpha_{adjusted} = \frac{\alpha}{N_{tests}}$$

**Rule of Thumb:** 
- Testing 100 strategies? Expect 5 to look significant at 5% level
- Require higher Sharpe or longer track record

---

## 5. Common Pitfalls

### Lookahead Bias

**Definition:** Using information not available at decision time.

**Examples:**
- Using adjusted close for returns (dividends may not be known)
- Using revised economic data
- Feature calculation using future data

**Solution:** Strict point-in-time data management

### Survivorship Bias

**Definition:** Only testing on assets that survived.

**Examples:**
- Testing momentum on current S&P 500 companies
- Ignoring delisted or bankrupt stocks

**Solution:** Include dead stocks in universe

### Overfitting

**Definition:** Fitting noise rather than signal.

**Signs:**
- Great in-sample, poor out-of-sample
- Many parameters relative to data
- Strategy works only on specific period

**Solutions:**
- Walk-forward validation
- Regularization
- Fewer parameters
- Multiple testing correction

### Transaction Cost Underestimation

**Common Mistakes:**
- Assuming you trade at close price
- Ignoring market impact
- Not accounting for capacity

**Solution:** 
- Conservative cost assumptions
- Scale costs with order size
- Test at different cost levels

---

## Key Formulas Summary

| Metric | Formula |
|--------|---------|
| Sharpe Ratio | $SR = \frac{\mu - R_f}{\sigma} \times \sqrt{252}$ |
| Sortino Ratio | $Sortino = \frac{\mu - R_f}{\sigma_{down}} \times \sqrt{252}$ |
| Max Drawdown | $MDD = \max_t \frac{Peak_t - Value_t}{Peak_t}$ |
| Calmar Ratio | $Calmar = \frac{R_{annual}}{|MDD|}$ |
| Profit Factor | $PF = \frac{\sum Gains}{\sum Losses}$ |

---

## Practice Problems

1. A strategy has daily returns with mean 0.03% and std 1.2%. Risk-free rate is 0%. Calculate the annualized Sharpe ratio.

2. Given the following portfolio values: [100, 105, 98, 102, 95, 110], calculate the maximum drawdown.

3. A strategy trades 200% per day (full turnover twice). Transaction costs are 5 bps per trade. What is the annual cost drag in percentage terms?

4. Explain why K-Fold cross-validation can lead to optimistic performance estimates in time series prediction.

5. Your backtest shows a Sharpe of 2.5 with 50% annual turnover and no transaction costs modeled. Assuming 10 bps round-trip costs, what is the adjusted Sharpe?

---

*Next Week: Neural Networks and Deep Learning*
