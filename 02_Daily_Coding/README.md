# Daily Coding Section

This folder contains 168 Jupyter notebooks (7 per week × 24 weeks) for hands-on practice.

## Structure

```
02_Daily_Coding/
├── Week_01_Foundation/
│   ├── Day_01_NumPy_Financial_Arrays.ipynb
│   ├── Day_02_Pandas_TimeSeries_PointInTime.ipynb
│   ├── Day_03_Returns_Volatility_RiskMetrics.ipynb
│   ├── Day_04_Correlation_Covariance_FactorAnalysis.ipynb
│   ├── Day_05_Visualization_and_EDA.ipynb
│   ├── Day_06_Practice_Problems_Foundation.ipynb
│   └── Day_07_Interview_Fundamentals_Week1.ipynb
├── Week_02_Financial_Mathematics/
│   └── [7 notebooks]
├── ... [Weeks 03-24 follow same pattern]
└── datasets/
    ├── README.md
    ├── download_data.py
    └── data_quality_checks.py
```

## Notebook Template

Every notebook follows this structure:

1. **Learning Objectives** - What you'll master
2. **Why This Matters for Interviews** - Company-specific relevance
3. **Theory Recap** - Key math and intuition
4. **Imports and Setup** - Required libraries
5. **Section 1: Algorithm Implementation from Scratch**
6. **Section 2: Finance Application with Real Data**
7. **Section 3: Production Considerations** (costs, latency, SHAP)
8. **Section 4: Backtesting with Realistic Costs**
9. **Section 5: ⏱️ TIMED CODING CHALLENGE** (30-45 min)
10. **Section 6: Interview Question of the Day**
11. **Section 7: Practice Exercises**
12. **Section 8: Key Takeaways**
13. **Section 9: Tomorrow's Preview**

## How to Use

### Daily Workflow

1. **Open notebook** for today
2. **Read theory first** (don't skip!)
3. **Type code, don't copy-paste** (builds muscle memory)
4. **Complete timed challenge** under time pressure
5. **Review solutions** only after attempting
6. **Take notes** on mistakes and insights

### Time Allocation

| Section | Time |
|---------|------|
| Theory recap + setup | 15-20 min |
| Algorithm implementation | 45-60 min |
| Finance application | 45-60 min |
| Production considerations | 20-30 min |
| **Timed challenge** | 30-45 min |
| Interview question + exercises | 30-45 min |
| **Total** | **3-4 hours** |

### Data Sources

All notebooks use real market data:
- **yfinance**: Stock prices, indices, ETFs
- **FRED**: Macroeconomic data
- **Quandl**: Alternative data (free tier)

Download scripts are in `datasets/` folder.

## Quality Standards

- [ ] All cells execute without errors
- [ ] Real data (no toy examples)
- [ ] Transaction costs included in backtests
- [ ] SHAP/LIME for black-box models
- [ ] Point-in-time data integrity
- [ ] Timed challenge completed under time limit

## Progress Tracking

Check off notebooks in `PROGRESS_TRACKER.md` as you complete them.

## Common Issues

### "Module not found"
```bash
pip install -r requirements.txt
```

### "Data download failed"
Check internet connection; yfinance may have rate limits. Wait and retry.

### "Memory error"
Reduce date range or use `.sample()` for development.

### "Results don't match expected"
1. Check random seeds are set
2. Verify data date ranges
3. Check for look-ahead bias in your code
