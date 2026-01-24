# 📈 Quantitative Trading & Machine Learning Curriculum

[![Python](https://img.shields.io/badge/Python-3.12%2B-blue.svg)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebooks-orange.svg)](https://jupyter.org/)
[![yfinance](https://img.shields.io/badge/Data-yfinance-yellow.svg)](https://pypi.org/project/yfinance/)

> A comprehensive 24-week curriculum for mastering Machine Learning in Quantitative Finance, designed for aspiring Quant Developers, Algorithmic Traders, and ML Engineers in Finance.

---

## 🎯 Overview

This repository contains **168+ Jupyter notebooks** covering everything from Python fundamentals to production-ready trading systems. Each week includes:

- **7 daily coding exercises** with hands-on implementations
- **Theory notebooks** with mathematical foundations (LaTeX formulas)
- **Trading Strategy notebooks** demonstrating real-world applications
- **Interview preparation** with common quant interview questions

### 📊 Curriculum Statistics

| Metric | Value |
|--------|-------|
| Total Weeks | 24 |
| Daily Notebooks | 168+ |
| Theory Files | 27 |
| Trading Strategies | 27 |
| Lines of Code | 50,000+ |
| Market Data Source | yfinance (AAPL, GOOGL, MSFT, GS, JPM) |

---

## 🗂️ Curriculum Structure

### Foundation (Weeks 1-4)
| Week | Topic | Key Concepts |
|------|-------|--------------|
| **Week 1** | Python for Finance | NumPy, Pandas, Matplotlib, yfinance, DataFrames |
| **Week 2** | Statistics & Probability | Distributions, Hypothesis Testing, CLT, Bayesian Thinking |
| **Week 3** | Time Series Analysis | Stationarity, ACF/PACF, Decomposition, Autocorrelation |
| **Week 4** | ML Foundations | Bias-Variance, Cross-Validation, Feature Scaling, Pipelines |

### Core ML (Weeks 5-12)
| Week | Topic | Key Concepts |
|------|-------|--------------|
| **Week 5** | Portfolio Optimization | MPT, VaR, Black-Litterman, Risk Parity |
| **Week 5.1** | Linear Models | OLS, Ridge, Lasso, ElasticNet, MLE |
| **Week 6** | Factor Models | CAPM, Fama-French 3/5, APT, Factor Exposure |
| **Week 6.1** | Classification | Logistic Regression, SVM, ROC/AUC |
| **Week 7** | Advanced Volatility | GARCH, EGARCH, GJR-GARCH, DCC-GARCH |
| **Week 7.1** | Tree Ensembles | Decision Trees, Random Forest, XGBoost, LightGBM |
| **Week 8** | Instance-Based | kNN, SVR, Kernel Methods, LOWESS |
| **Week 9** | Unsupervised Learning | K-Means, Hierarchical, PCA, DBSCAN, GMM |
| **Week 10** | Time Series ML | ARIMA, VAR, Cointegration, Kalman Filter |
| **Week 11** | Feature Engineering | Technical Features, Feature Selection, Target Engineering |
| **Week 12** | Backtesting | Performance Metrics, Walk-Forward, Transaction Costs |

### Deep Learning (Weeks 13-16)
| Week | Topic | Key Concepts |
|------|-------|--------------|
| **Week 13** | Neural Networks | Feedforward NN, Activation Functions, Backpropagation |
| **Week 14** | RNN/LSTM/GRU | Sequence Modeling, Vanishing Gradients, Time Series Prediction |
| **Week 15** | Attention & Transformers | Self-Attention, Multi-Head Attention, FinBERT |
| **Week 16** | Reinforcement Learning | MDPs, Q-Learning, DQN, Policy Gradients, PPO |

### Specialized Topics (Weeks 17-20)
| Week | Topic | Key Concepts |
|------|-------|--------------|
| **Week 17** | Options & Deep Hedging | Black-Scholes, Greeks, Delta Hedging, Market Making |
| **Week 18** | Portfolio Optimization | Markowitz, Risk Parity, Robust Optimization, HRP |
| **Week 19** | NLP & Alternative Data | Sentiment Analysis, Word Embeddings, FinBERT, News Trading |
| **Week 20** | Bayesian Methods | Bayes Theorem, Gaussian Processes, Kalman Filter, MCMC |

### Production Systems (Weeks 21-24)
| Week | Topic | Key Concepts |
|------|-------|--------------|
| **Week 21** | Market Microstructure | Order Book, Spread, Kyle's Lambda, Almgren-Chriss |
| **Week 22** | System Design | Architecture, Data Pipelines, Low Latency, Scalability |
| **Week 23** | Production ML | MLOps, Model Monitoring, A/B Testing, Drift Detection |
| **Week 24** | Capstone Project | End-to-End Trading System, Full Pipeline Integration |

---

## 🚀 Quick Start

### Prerequisites

- Python 3.12+
- Jupyter Notebook/Lab
- Git

### Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/Quant_ML_Basics.git
cd Quant_ML_Basics

# Create virtual environment
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### Dependencies

```txt
numpy>=1.24.0
pandas>=2.0.0
matplotlib>=3.7.0
seaborn>=0.12.0
scikit-learn>=1.3.0
yfinance>=0.2.28
scipy>=1.11.0
statsmodels>=0.14.0
torch>=2.0.0
tensorflow>=2.13.0
xgboost>=2.0.0
lightgbm>=4.0.0
transformers>=4.30.0
arch>=6.0.0
```

---

## 📁 Directory Structure

```
Quant_ML_Basics/
├── 01_Theory/                    # Theoretical foundations
│   ├── Foundation_Weeks_01-04/
│   ├── Core_ML_Weeks_05-12/
│   ├── Advanced_Weeks_13-20/
│   └── Production_Weeks_21-24/
│
├── 02_Daily_Coding/              # Hands-on implementations
│   ├── Week_01_Foundation/
│   │   ├── Day_01_NumPy_Financial_Arrays.ipynb
│   │   ├── Day_02_Pandas_DataManipulation.ipynb
│   │   ├── ...
│   │   ├── Day_07_Interview_Review.ipynb
│   │   ├── THEORY.ipynb
│   │   └── Trading_Strategy.ipynb
│   ├── Week_02_Statistics/
│   ├── ...
│   └── Week_24_Capstone/
│
├── 03_Weekly_Projects/           # Mini-projects per week
├── 04_Interview_Preparation/     # Interview Q&A
│   ├── Topic_Based/
│   ├── Company_Specific/
│   └── Mock_Interviews/
├── 05_Capstone_Projects/         # Major final projects
│   ├── Option_1_Multi_Asset_ML_Trading_System/
│   ├── Option_2_Deep_Hedging_Options_Market_Making/
│   ├── Option_3_Alternative_Data_NLP_Alpha_Research/
│   └── Option_4_HFT_Microstructure_Execution_Optimization/
└── 06_Portfolio_Presentation/    # Resume & portfolio guides
```

---

## 📈 Sample Trading Strategy Output

Each week's Trading_Strategy.ipynb generates actionable signals:

```python
# Example output from Week 13 Neural Networks Trading Strategy
================================================================================
                    NEURAL NETWORK TRADING SIGNALS
================================================================================

Stock: AAPL
  Prediction: BUY (60.2% confidence)
  Entry Price: $187.45
  Stop Loss: $182.82 (-2.5%)
  Take Profit: $196.82 (+5.0%)

Stock: GOOGL  
  Prediction: SELL (54.8% confidence)
  Entry Price: $141.23
  Stop Loss: $144.05 (+2.0%)
  Take Profit: $134.17 (-5.0%)

Portfolio Summary:
  Total Signals: 5 (3 BUY, 2 SELL)
  High Confidence (>55%): 2 trades
  Avg Model Accuracy: 52.3%
  Sharpe Ratio (backtest): 1.24
================================================================================
```

---

## 🎓 Learning Objectives

Upon completing this curriculum, you will be able to:

### Technical Skills
- ✅ Implement trading strategies using ML models (RF, XGBoost, LSTM, Transformers)
- ✅ Build portfolio optimization systems (Markowitz, Black-Litterman, Risk Parity)
- ✅ Deploy production-ready ML pipelines with monitoring
- ✅ Analyze market microstructure and execution algorithms
- ✅ Apply NLP for sentiment-driven trading strategies

### Quantitative Finance Knowledge
- ✅ Understand factor models (CAPM, Fama-French, APT)
- ✅ Price derivatives using Black-Scholes and Greeks
- ✅ Implement volatility modeling (GARCH family)
- ✅ Design backtesting frameworks with proper walk-forward validation

### Interview Readiness
- ✅ Answer technical questions on ML algorithms for trading
- ✅ Explain portfolio optimization mathematically
- ✅ Discuss system design for trading platforms
- ✅ Present capstone projects demonstrating end-to-end capabilities

---

## 📊 Quality Assurance

All notebooks have been audited for:

| Check | Status |
|-------|--------|
| Code executes without errors | ✅ 100% |
| yfinance data loads correctly | ✅ 100% |
| Mathematical formulas (LaTeX) | ✅ Present |
| Trading signals generated | ✅ All strategy notebooks |
| Consistent ticker usage | ✅ AAPL, GOOGL, MSFT, GS, JPM |

See [MARKDOWN_AUDIT_REPORT.md](MARKDOWN_AUDIT_REPORT.md) for detailed audit results.

---

## 🤝 Contributing

Contributions are welcome! Please read our contributing guidelines:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-strategy`)
3. Commit changes (`git commit -m 'Add momentum strategy'`)
4. Push to branch (`git push origin feature/new-strategy`)
5. Open a Pull Request

---

## 📚 References & Resources

### Books
- *Advances in Financial Machine Learning* - Marcos López de Prado
- *Machine Learning for Algorithmic Trading* - Stefan Jansen
- *Quantitative Trading* - Ernest Chan

### Papers
- Fama & French (1993) - Common Risk Factors in Stock Returns
- Black & Litterman (1992) - Global Portfolio Optimization
- Gu, Kelly & Xiu (2020) - Empirical Asset Pricing via Machine Learning

### Online Resources
- [QuantConnect](https://www.quantconnect.com/)
- [Kaggle Financial Datasets](https://www.kaggle.com/datasets)
- [Yahoo Finance API (yfinance)](https://pypi.org/project/yfinance/)

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👤 Author

**Your Name**
- GitHub: [@yourusername](https://github.com/yourusername)
- LinkedIn: [Your LinkedIn](https://linkedin.com/in/yourprofile)
- Email: your.email@example.com

---

<p align="center">
  <i>Built with 💹 for aspiring Quant Traders & ML Engineers</i>
</p>
