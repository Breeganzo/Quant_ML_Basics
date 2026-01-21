# Weekly Projects Section

This folder contains 24 portfolio-ready projects—one per week.

## Structure

```
03_Weekly_Projects/
├── README.md                                     ← You are here
├── Week_01_Market_Data_Pipeline_with_Quality_Checks/
├── Week_02_Bond_Pricing_and_YieldCurve_Analytics/
├── Week_03_Volatility_Forecasting_GARCH_vs_ML/
├── Week_04_Backtesting_Engine_with_Costs_and_Slippage/
├── Week_05_Linear_Factor_Model_OLS_Ridge_Lasso/
├── Week_06_Classification_Trading_Signals_MetaLabeling/
├── Week_07_Tree_Ensemble_Alpha_Factors_XGBoost/
├── Week_08_SVM_KNN_Regime_Classification/
├── Week_09_PCA_HMM_Clustering_for_Regimes/
├── Week_10_ARIMA_GARCH_Forecasting_Strategy/
├── Week_11_Feature_Library_with_SHAP_Explainability/
├── Week_12_Advanced_Backtesting_CPCV_DeflatedSharpe_TCA/
├── Week_13_Deep_MLP_Factor_Prediction/
├── Week_14_LSTM_Sequence_Prediction_with_Attention/
├── Week_15_RL_Trading_Agent_DQN_Thompson_Sampling/
├── Week_16_Options_Pricer_VolSurface_DeepHedging/
├── Week_17_Multi_Strategy_Portfolio_Optimizer/
├── Week_18_NLP_Sentiment_Trading_BERT_FinBERT/
├── Week_19_Bayesian_Kalman_Adaptive_Portfolio/
├── Week_20_HFT_Microstructure_LOB_Analysis/
├── Week_21_Research_Platform_Design_and_Implementation/
├── Week_22_Real_Time_Execution_System/
├── Week_23_Production_Monitoring_AlphaDecay_Dashboard/
└── Week_24_Capstone_Final_Integration/
```

## Project Template

Each project folder contains:

```
Week_XX_Project_Name/
├── README.md              # Business problem, algorithms, results
├── requirements.txt       # Dependencies with versions
├── data/
│   ├── README.md          # Data sources and date ranges
│   └── download_data.py   # Reproducible data download
├── notebooks/
│   ├── 01_exploration.ipynb
│   ├── 02_modeling.ipynb
│   └── 03_backtesting_validation.ipynb
├── src/
│   ├── __init__.py
│   ├── features.py
│   ├── models.py
│   └── backtesting.py
├── tests/
│   ├── test_features.py
│   └── test_models.py
├── results/
│   ├── figures/
│   └── metrics.json
└── presentation.pdf       # 5-8 slides
```

## Grading Rubric

Use this to self-assess each project:

| Criterion | Weight | Excellent (90-100) | Good (75-89) | Acceptable (60-74) |
|-----------|--------|-------------------|--------------|-------------------|
| Data quality & point-in-time | 15% | No look-ahead, survivorship handled | Minor issues | Significant gaps |
| Algorithm implementation | 20% | Correct, efficient, from-scratch elements | Works but inefficient | Bugs or incomplete |
| Backtesting rigor | 20% | Purged CV, costs, walk-forward | Missing one element | Naive time-series split |
| Production awareness | 15% | SHAP, costs, latency, capacity | Missing one element | No production thinking |
| Code quality | 15% | Tested, documented, modular | Missing tests or docs | Messy, no structure |
| Presentation | 15% | Clear, concise, interview-ready | Minor clarity issues | Confusing or incomplete |

**Scoring:**
- 90-100: Portfolio showcase ready
- 75-89: Needs minor polish
- 60-74: Significant improvements needed
- <60: Major rework required

## Project Summaries

### Foundation (Weeks 1-4)

| Week | Project | Key Skills |
|------|---------|------------|
| 1 | Market Data Pipeline | Data quality, survivorship, point-in-time |
| 2 | Bond Pricing Analytics | Fixed income math, yield curves |
| 3 | Volatility Forecasting | GARCH vs ML comparison |
| 4 | Backtesting Engine | Transaction costs, slippage |

### Core ML (Weeks 5-12)

| Week | Project | Key Skills |
|------|---------|------------|
| 5 | Linear Factor Model | OLS, Ridge, Lasso comparison |
| 6 | Classification Signals | Meta-labeling, bet sizing |
| 7 | Tree Ensemble Alphas | XGBoost, SHAP, feature importance |
| 8 | Regime Classification | kNN, SVM, regime-aware trading |
| 9 | PCA HMM Clustering | Unsupervised regime detection |
| 10 | ARIMA GARCH Strategy | Time series forecasting |
| 11 | Feature Library | Fractional diff, SHAP, LIME |
| 12 | Advanced Backtesting | CPCV, deflated Sharpe, TCA |

### Advanced (Weeks 13-20)

| Week | Project | Key Skills |
|------|---------|------------|
| 13 | Deep MLP Factors | Neural networks for alpha |
| 14 | LSTM Sequences | Attention, temporal patterns |
| 15 | RL Trading Agent | DQN, Thompson Sampling |
| 16 | Options & Deep Hedging | Greeks, vol surface, hedging |
| 17 | Portfolio Optimizer | Markowitz, BL, HRP comparison |
| 18 | NLP Sentiment | FinBERT, news signals |
| 19 | Bayesian Adaptive | Kalman, uncertainty quantification |
| 20 | HFT Microstructure | LOB, optimal execution |

### Production (Weeks 21-24)

| Week | Project | Key Skills |
|------|---------|------------|
| 21 | Research Platform | System design, APIs |
| 22 | Real-Time Execution | Streaming, event-driven |
| 23 | Production Monitoring | Alpha decay, drift detection |
| 24 | Capstone Integration | Full system, documentation |

## Interview Talking Points

For each project, prepare:

1. **30-second summary**: "This project does X using Y to achieve Z"
2. **Technical deep-dive**: Algorithm choices, trade-offs, results
3. **Challenges faced**: What didn't work, how you fixed it
4. **Extensions**: What you'd do with more time/data
5. **Business impact**: Why this matters to a trading firm

## GitHub Best Practices

1. **Clean commit history**: Meaningful messages, logical progression
2. **README quality**: Clear, professional, results visible
3. **No secrets**: API keys in `.env`, not in code
4. **Reproducibility**: `requirements.txt`, random seeds, data scripts
5. **Code quality**: PEP 8, type hints, docstrings
