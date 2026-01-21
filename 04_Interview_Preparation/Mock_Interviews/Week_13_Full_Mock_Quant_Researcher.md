# Mock Interview: Quant Researcher (Week 13)

## Overview

**Duration:** 3 hours  
**Format:** 4 rounds  
**Focus:** Quantitative research role at systematic fund

---

## Round 1: Technical Screen (45 minutes)

### Section A: Probability (15 min)

**Problem 1:** You flip a fair coin repeatedly. What's the expected number of flips until you get two heads in a row?

**Problem 2:** A bag contains 3 red balls and 2 blue balls. You draw without replacement. What's the probability the second ball is red?

### Section B: Statistics (15 min)

**Problem 3:** Explain the difference between Type I and Type II errors. How would you choose a significance level for a backtest?

**Problem 4:** Your backtest shows a Sharpe ratio of 2.0 over 3 years of daily data. Is this statistically significant? How would you test this?

### Section C: ML Basics (15 min)

**Problem 5:** Explain the bias-variance tradeoff. Give an example from finance.

**Problem 6:** When would you choose Ridge regression over Lasso? What about Elastic Net?

---

## Round 2: Quantitative Finance (45 minutes)

### Section A: Portfolio Theory (20 min)

**Problem 7:** Derive the minimum variance portfolio weights for two assets.

**Problem 8:** What are the practical problems with Markowitz optimization? How would you address them?

### Section B: Time Series (15 min)

**Problem 9:** Explain GARCH(1,1). What do the parameters mean? How would you use it in trading?

### Section C: Risk Management (10 min)

**Problem 10:** Explain VaR vs CVaR. Why might CVaR be preferred?

---

## Round 3: Coding (60 minutes)

### Problem 11: Factor Model Implementation (30 min)

Implement a function that:
1. Downloads stock price data
2. Calculates factor exposures (momentum, value)
3. Runs a cross-sectional regression
4. Returns factor returns and exposures

```python
def factor_model(tickers: list, start_date: str, end_date: str) -> dict:
    """
    Implement Fama-French style factor model.
    
    Returns:
        dict with 'factor_returns', 'exposures', 'r_squared'
    """
    pass
```

### Problem 12: Backtest Engine (30 min)

Implement a simple backtester with:
- Transaction costs
- Position limits
- Walk-forward validation

```python
class SimpleBacktester:
    def __init__(self, prices: pd.DataFrame, 
                 transaction_cost: float = 0.001):
        pass
    
    def run(self, signals: pd.DataFrame) -> dict:
        """
        Returns performance metrics.
        """
        pass
```

---

## Round 4: Project Discussion (30 minutes)

### Section A: Walk Through a Project (15 min)

Prepare to present:
1. What problem did you solve?
2. What data did you use?
3. What methods did you try?
4. What were the results?
5. What would you do differently?

### Section B: Deep Dive Questions (15 min)

Expect questions like:
- How did you prevent overfitting?
- What was your validation strategy?
- How would this scale with more capital?
- What are the main risks?

---

## Scoring Rubric

| Round | Max Points | Your Score |
|-------|-----------|------------|
| Technical Screen | 25 | ___ |
| Quantitative Finance | 25 | ___ |
| Coding | 30 | ___ |
| Project Discussion | 20 | ___ |
| **Total** | **100** | ___ |

### Score Interpretation

| Score | Assessment |
|-------|------------|
| 85-100 | Strong hire signal |
| 70-84 | Hire with some concerns |
| 55-69 | Borderline |
| <55 | Not ready, more practice needed |

---

## Post-Mock Review

**Strongest Areas:**
1. _______________
2. _______________

**Areas to Improve:**
1. _______________
2. _______________

**Action Items for Next Week:**
1. _______________
2. _______________
3. _______________
