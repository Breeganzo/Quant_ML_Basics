# Week 1: Python for Quantitative Finance

## 📚 Learning Objectives

By the end of this week, you will:
1. Master NumPy for efficient numerical computations with financial data
2. Use Pandas for time series manipulation with point-in-time awareness
3. Calculate returns, volatility, and risk metrics correctly
4. Understand correlation, covariance, and their role in portfolio theory
5. Create publication-quality financial visualizations
6. Solve foundational coding interview problems

---

## 📖 Theory Content

### 1. Why Python for Quantitative Finance?

Python has become the **lingua franca** of quantitative finance for several reasons:

- **NumPy/Pandas ecosystem**: Vectorized operations make financial calculations fast
- **Rich library support**: scikit-learn, PyTorch, statsmodels, etc.
- **Rapid prototyping**: Quick iteration from idea to backtest
- **Production ready**: Many hedge funds deploy Python strategies in production

> "At Jane Street, we use a combination of OCaml and Python. Python is used extensively for data analysis and research." - Jane Street Tech Blog

### 2. NumPy Fundamentals for Finance

#### 2.1 Why NumPy over Pure Python?

```python
# Pure Python (slow)
returns = [r1, r2, r3, ...]
cumulative = 1
for r in returns:
    cumulative *= (1 + r)  # O(n) loop

# NumPy (fast)
returns = np.array([r1, r2, r3, ...])
cumulative = np.prod(1 + returns)  # Vectorized C code
```

**Key NumPy concepts for finance:**
- **Broadcasting**: Apply operations across different shaped arrays
- **Vectorization**: Eliminate Python loops for speed
- **Memory efficiency**: Contiguous memory layout for cache optimization

#### 2.2 Critical NumPy Functions

| Function | Finance Application |
|----------|---------------------|
| `np.log()` | Log returns calculation |
| `np.exp()` | Compound growth |
| `np.cumprod()` | Cumulative returns |
| `np.corrcoef()` | Correlation matrix |
| `np.cov()` | Covariance matrix |
| `np.linalg.inv()` | Portfolio optimization |
| `np.random.normal()` | Monte Carlo simulation |

### 3. Pandas for Time Series

#### 3.1 The DatetimeIndex

Financial data is **temporal**. Pandas DatetimeIndex provides:
- Automatic alignment of different time series
- Resampling (daily → weekly → monthly)
- Business day awareness
- Timezone handling

```python
# Correct: timezone-aware, aligned data
prices = pd.DataFrame(data, index=pd.DatetimeIndex(dates, tz='America/New_York'))

# Dangerous: implicit timezone assumptions
prices = pd.DataFrame(data, index=dates)  # What timezone?
```

#### 3.2 Point-in-Time Data

> ⚠️ **CRITICAL CONCEPT**: Point-in-time (PIT) data ensures you only use information that was available at each historical moment.

**Look-ahead bias example:**
```python
# WRONG: Uses future information
prices['sma_20'] = prices['close'].rolling(20).mean()
signal = prices['close'] > prices['sma_20']  # Today's close compared to SMA including today!

# CORRECT: Use shifted data
prices['sma_20'] = prices['close'].rolling(20).mean().shift(1)
signal = prices['close'] > prices['sma_20']  # Compare to yesterday's SMA
```

### 4. Returns Calculation

#### 4.1 Simple vs Log Returns

**Simple Returns:**
$$R_t = \frac{P_t - P_{t-1}}{P_{t-1}} = \frac{P_t}{P_{t-1}} - 1$$

**Log Returns:**
$$r_t = \ln\left(\frac{P_t}{P_{t-1}}\right) = \ln(P_t) - \ln(P_{t-1})$$

**When to use which:**
| Scenario | Use |
|----------|-----|
| Portfolio returns (cross-sectional) | Simple returns |
| Time series analysis | Log returns |
| Multi-period compounding | Log returns (additive) |
| Risk metrics (VaR) | Either (depends on model) |

#### 4.2 Annualization

Trading days per year: **252** (approximate)

| Metric | Annualization Formula |
|--------|----------------------|
| Return | $R_{annual} = R_{daily} \times 252$ |
| Volatility | $\sigma_{annual} = \sigma_{daily} \times \sqrt{252}$ |
| Sharpe Ratio | $SR_{annual} = SR_{daily} \times \sqrt{252}$ |

### 5. Volatility and Risk Metrics

#### 5.1 Historical Volatility

```python
# Standard deviation of returns
volatility = returns.std() * np.sqrt(252)

# Exponentially weighted (more recent data weighted higher)
ewm_vol = returns.ewm(span=20).std() * np.sqrt(252)
```

#### 5.2 Key Risk Metrics

| Metric | Formula | Interpretation |
|--------|---------|----------------|
| **Sharpe Ratio** | $(R_p - R_f) / \sigma_p$ | Return per unit of total risk |
| **Sortino Ratio** | $(R_p - R_f) / \sigma_{downside}$ | Return per unit of downside risk |
| **Max Drawdown** | $\max_{t}(1 - P_t / \max_{s \leq t} P_s)$ | Worst peak-to-trough decline |
| **VaR (95%)** | 5th percentile of returns | "95% of the time, loss won't exceed X" |

### 6. Correlation and Covariance

#### 6.1 Definitions

**Correlation** (normalized, -1 to +1):
$$\rho_{X,Y} = \frac{Cov(X,Y)}{\sigma_X \sigma_Y}$$

**Covariance** (in return units):
$$Cov(X,Y) = E[(X - \mu_X)(Y - \mu_Y)]$$

#### 6.2 Finance Applications

- **Portfolio variance**: $\sigma_p^2 = w^T \Sigma w$ (where $\Sigma$ is covariance matrix)
- **Diversification**: Low correlation → risk reduction
- **Pairs trading**: High correlation → mean-reversion opportunities
- **Factor models**: Correlation with market factor → beta

### 7. Common Interview Topics

#### Probability & Statistics
- Expected value calculations
- Variance and covariance properties
- Central Limit Theorem applications
- Conditional probability (Bayes' theorem)

#### Python Coding
- Efficient array operations (avoid loops)
- Time series manipulation
- Edge cases (NaN handling, empty arrays)
- Memory efficiency

#### Finance Concepts
- Why use log returns?
- Explain diversification mathematically
- What is the Sharpe ratio measuring?
- How would you detect data quality issues?

---

## 📝 Daily Schedule

| Day | Topic | Notebook | Key Skills |
|-----|-------|----------|------------|
| 1 | NumPy Financial Arrays | `Day_01_NumPy_Financial_Arrays.ipynb` | Vectorization, broadcasting |
| 2 | Pandas TimeSeries | `Day_02_Pandas_TimeSeries_PointInTime.ipynb` | DatetimeIndex, resampling |
| 3 | Returns & Volatility | `Day_03_Returns_Volatility_RiskMetrics.ipynb` | Risk calculations |
| 4 | Correlation & Covariance | `Day_04_Correlation_Covariance_FactorAnalysis.ipynb` | Matrix operations |
| 5 | Visualization & EDA | `Day_05_Visualization_EDA_FinancialCharts.ipynb` | Matplotlib, Plotly |
| 6 | Practice Problems | `Day_06_Practice_Problems_Foundation.ipynb` | Coding challenges |
| 7 | Interview Prep | `Day_07_Interview_Fundamentals_Week1.ipynb` | Mock questions |

---

## 📚 Required Reading

1. **Python for Finance** (Hilpisch) - Chapters 1-4
2. **Quantitative Trading** (Chan) - Chapter 2: Backtesting
3. **NumPy Documentation**: Broadcasting rules
4. **Pandas Documentation**: Time series / date functionality

---

## 🎯 Week 1 Project

**Market Data Pipeline with Quality Checks**

Build a production-ready data pipeline that:
1. Downloads multi-asset data (equities, ETFs, FX)
2. Performs comprehensive quality checks
3. Calculates standard risk metrics
4. Generates a data quality report

See: `03_Weekly_Projects/Week_01_Market_Data_Pipeline_with_Quality_Checks/`

---

## ✅ Self-Assessment Checklist

Before moving to Week 2, ensure you can:

- [ ] Explain the difference between simple and log returns
- [ ] Calculate annualized volatility from daily returns
- [ ] Create a correlation matrix and interpret it
- [ ] Handle missing data in time series appropriately
- [ ] Explain point-in-time data and look-ahead bias
- [ ] Write vectorized NumPy code (no Python loops)
- [ ] Calculate Sharpe ratio and max drawdown
- [ ] Resample daily data to weekly/monthly
