# Capstone Option 1: Multi-Asset ML Trading System

## Project Overview

Build a production-grade systematic trading system that generates ML-based signals across multiple asset classes, constructs an optimal portfolio, and manages risk.

## Target Metrics

| Metric | Target | Stretch |
|--------|--------|---------|
| Sharpe Ratio | > 2.0 | > 2.5 |
| Max Drawdown | < 12% | < 8% |
| Correlation to SPY | < 0.3 | < 0.1 |
| Annual Turnover | < 20x | < 10x |

## Asset Universe

- **Equities:** S&P 500 constituents (survivorship-bias adjusted)
- **Futures:** E-mini S&P, Treasury futures, Gold, Oil
- **FX:** G10 currency pairs

## Algorithm Stack

### Alpha Generation
| Model | Purpose | Features |
|-------|---------|----------|
| XGBoost | Cross-sectional equity | 50+ factors |
| LSTM | Time-series patterns | Price sequences |
| Linear | Baseline | Fama-French factors |

### Signal Combination
- Meta-labeling for position sizing
- Ensemble averaging
- Signal decay weighting

### Portfolio Construction
- Hierarchical Risk Parity
- Maximum diversification
- Transaction cost optimization

## Project Structure

```
Option_1_Multi_Asset_ML_Trading_System/
├── Project_Proposal.md
├── Literature_Review.md
├── Data/
│   ├── download_scripts/
│   └── processed/
├── Notebooks/
│   ├── 01_Data_Exploration.ipynb
│   ├── 02_Feature_Engineering.ipynb
│   ├── 03_Model_Development.ipynb
│   ├── 04_Backtesting.ipynb
│   ├── 05_Risk_Analysis.ipynb
│   └── 06_Production_Design.ipynb
├── src/
│   ├── data/
│   ├── features/
│   ├── models/
│   ├── portfolio/
│   └── backtest/
├── tests/
├── docs/
├── Final_Report.md
└── Presentation.pdf
```

## Timeline

| Week | Milestone |
|------|-----------|
| 20 | Project proposal approved |
| 21 | Data pipeline complete |
| 22 | Feature library + models trained |
| 23 | Backtesting + risk analysis |
| 24 | Documentation + presentation |

## Deliverables Checklist

- [ ] Point-in-time data pipeline
- [ ] Feature engineering module (50+ features)
- [ ] Multiple alpha models with comparison
- [ ] SHAP analysis for all models
- [ ] Portfolio optimizer with constraints
- [ ] Walk-forward backtest with costs
- [ ] Stress testing (2008, 2020, flash crash)
- [ ] Production monitoring design
- [ ] Complete documentation
- [ ] 20-minute presentation
