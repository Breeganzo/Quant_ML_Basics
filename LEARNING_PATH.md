# 24-Week Learning Path

## Overview

| Phase | Weeks | Focus | Hours |
|-------|-------|-------|-------|
| Foundation | 1-4 | Python, Math, Probability, Data Quality | 100 |
| Core ML | 5-12 | Supervised, Unsupervised, Time Series, Validation | 200 |
| Advanced | 13-20 | Deep Learning, RL, Specialized Models | 200 |
| Production | 21-24 | System Design, Deployment, Capstone | 100 |
| **Total** | **24** | **Complete Quant Finance + ML** | **600** |

---

## Phase 1: Foundation (Weeks 1-4)

### Week 1: Python for Quantitative Finance

**Theory:** `01_Theory/Foundation_Weeks_01-04/Week_01_Python_for_Finance.md`

| Day | Notebook | Topic | Key Skills | Time |
|-----|----------|-------|------------|------|
| Mon | `Day_01_NumPy_Financial_Arrays.ipynb` | NumPy fundamentals | Vectorization, broadcasting, no loops | 4-5h |
| Tue | `Day_02_Pandas_TimeSeries_PointInTime.ipynb` | Pandas time series | DatetimeIndex, point-in-time, resampling | 4-5h |
| Wed | `Day_03_Returns_Volatility_RiskMetrics.ipynb` | Return calculations | Simple, log, rolling volatility, VaR | 4-5h |
| Thu | `Day_04_Correlation_Covariance_FactorAnalysis.ipynb` | Correlation analysis | Covariance matrices, factor exposure | 4-5h |
| Fri | `Day_05_Visualization_and_EDA.ipynb` | Data visualization | Matplotlib, seaborn, financial charts | 4-5h |
| Sat | `Day_06_Practice_Problems_Foundation.ipynb` | Practice problems | Timed exercises, real data | 6-8h |
| Sun | `Day_07_Interview_Fundamentals_Week1.ipynb` | Interview prep | Python fundamentals questions | 4-6h |

**Weekly Project:** `03_Weekly_Projects/Week_01_Market_Data_Pipeline_with_Quality_Checks/`
- Build data pipeline with yfinance
- Implement survivorship bias checks
- Create data quality validation framework
- Handle corporate actions

**Interview Questions (5-7):**
- Explain vectorization vs. loops in NumPy
- How do you handle missing data in time series?
- What is point-in-time data and why does it matter?

---

### Week 2: Financial Mathematics

**Theory:** `01_Theory/Foundation_Weeks_01-04/Week_02_Financial_Mathematics.md`

| Day | Notebook | Topic | Key Skills | Time |
|-----|----------|-------|------------|------|
| Mon | `Day_01_TimeValue_Compounding.ipynb` | Time value of money | PV, FV, continuous compounding | 4-5h |
| Tue | `Day_02_Bond_Pricing_Duration.ipynb` | Bond mathematics | YTM, duration, convexity | 4-5h |
| Wed | `Day_03_YieldCurve_Construction.ipynb` | Yield curves | Bootstrapping, interpolation | 4-5h |
| Thu | `Day_04_Discount_Factors_IRR.ipynb` | Discounting | NPV, IRR, discount factors | 4-5h |
| Fri | `Day_05_Portfolio_Returns.ipynb` | Portfolio math | Weighted returns, rebalancing | 4-5h |
| Sat | `Day_06_Practice_Problems_FinMath.ipynb` | Practice problems | Bond pricing, yield curves | 6-8h |
| Sun | `Day_07_Interview_FinMath_Week2.ipynb` | Interview prep | Financial math questions | 4-6h |

**Weekly Project:** `03_Weekly_Projects/Week_02_Bond_Pricing_and_YieldCurve_Analytics/`
- Build bond pricing calculator
- Implement yield curve bootstrapping
- Calculate duration and convexity
- DV01 and risk analysis

**Interview Questions (5-7):**
- Derive the duration formula
- Why does convexity matter for bonds?
- Calculate YTM given price, coupon, maturity

---

### Week 3: Probability and Statistics

**Theory:** `01_Theory/Foundation_Weeks_01-04/Week_03_Probability_and_Statistics.md`

| Day | Notebook | Topic | Key Skills | Time |
|-----|----------|-------|------------|------|
| Mon | `Day_01_Probability_Distributions.ipynb` | Distributions | Normal, log-normal, t, Poisson | 4-5h |
| Tue | `Day_02_Bayes_Theorem_Conditional.ipynb` | Bayesian probability | Bayes' theorem, conditional prob | 4-5h |
| Wed | `Day_03_Expected_Value_Variance.ipynb` | Moments | E[X], Var[X], covariance | 4-5h |
| Thu | `Day_04_Hypothesis_Testing.ipynb` | Statistical testing | t-tests, p-values, confidence | 4-5h |
| Fri | `Day_05_MLE_Estimation.ipynb` | Estimation | MLE, method of moments | 4-5h |
| Sat | `Day_06_Practice_Problems_Stats.ipynb` | Practice problems | Probability puzzles | 6-8h |
| Sun | `Day_07_Interview_Probability_Week3.ipynb` | Interview prep | Probability questions (Jane Street style) | 4-6h |

**Weekly Project:** `03_Weekly_Projects/Week_03_Volatility_Forecasting_GARCH_vs_ML/`
- Implement GARCH(1,1) from scratch
- Compare with ML-based volatility forecasts
- Evaluate forecast accuracy
- Trading strategy based on vol forecasts

**Interview Questions (5-7):**
- Calculate E[X²] for uniform distribution
- Apply Bayes' theorem to trading scenario
- Is Sharpe = 1.5 statistically significant over 1 year?

---

### Week 4: Market Microstructure & Data Quality

**Theory:** `01_Theory/Foundation_Weeks_01-04/Week_04_Market_Microstructure_and_Data_Quality.md`

| Day | Notebook | Topic | Key Skills | Time |
|-----|----------|-------|------------|------|
| Mon | `Day_01_Order_Types_Execution.ipynb` | Market mechanics | Order types, matching engines | 4-5h |
| Tue | `Day_02_BidAsk_Spread_Liquidity.ipynb` | Liquidity | Spread decomposition, market impact | 4-5h |
| Wed | `Day_03_Survivorship_Bias.ipynb` | Data biases | Survivorship, look-ahead | 4-5h |
| Thu | `Day_04_Corporate_Actions.ipynb` | Adjustments | Splits, dividends, mergers | 4-5h |
| Fri | `Day_05_PointInTime_Fundamentals.ipynb` | Point-in-time | Earnings dates, reporting lags | 4-5h |
| Sat | `Day_06_Practice_Problems_DataQuality.ipynb` | Practice problems | Data validation exercises | 6-8h |
| Sun | `Day_07_Interview_Microstructure_Week4.ipynb` | Interview prep | Market structure questions | 4-6h |

**Weekly Project:** `03_Weekly_Projects/Week_04_Backtesting_Engine_with_Costs_and_Slippage/`
- Build backtesting framework
- Implement transaction cost models
- Add slippage modeling
- Walk-forward validation structure

**Interview Questions (5-7):**
- What is survivorship bias and how do you avoid it?
- Explain the square-root market impact model
- How do you handle look-ahead bias in feature engineering?

---

## Phase 2: Core ML (Weeks 5-12)

### Week 5: Linear Models (OLS, Ridge, Lasso, Elastic Net)

**Theory:** `01_Theory/Core_ML_Weeks_05-12/Week_05_Linear_Models_OLS_Ridge_Lasso_ElasticNet.md`

**Algorithms Covered:**

| Algorithm | Loss Function | Regularization | Sparsity |
|-----------|---------------|----------------|----------|
| OLS | $\sum(y - X\beta)^2$ | None | No |
| Ridge | $\sum(y - X\beta)^2 + \lambda\|\beta\|_2^2$ | L2 | No |
| Lasso | $\sum(y - X\beta)^2 + \lambda\|\beta\|_1$ | L1 | Yes |
| Elastic Net | $\sum(y - X\beta)^2 + \lambda_1\|\beta\|_1 + \lambda_2\|\beta\|_2^2$ | L1+L2 | Yes |

| Day | Notebook | Topic | Key Skills | Time |
|-----|----------|-------|------------|------|
| Mon | `Day_01_OLS_From_Scratch.ipynb` | OLS derivation | Normal equations, assumptions | 4-5h |
| Tue | `Day_02_Ridge_Regression.ipynb` | Ridge regression | L2 regularization, bias-variance | 4-5h |
| Wed | `Day_03_Lasso_Regression.ipynb` | Lasso regression | L1 regularization, sparsity | 4-5h |
| Thu | `Day_04_ElasticNet_Selection.ipynb` | Elastic Net | Combining L1/L2, cross-validation | 4-5h |
| Fri | `Day_05_Factor_Model_Application.ipynb` | Factor models | Fama-French, alpha estimation | 4-5h |
| Sat | `Day_06_Practice_Linear_Models.ipynb` | Practice problems | Implementation + timed challenges | 6-8h |
| Sun | `Day_07_Interview_Linear_Week5.ipynb` | Interview prep | Linear algebra, regularization questions | 4-6h |

**Weekly Project:** `03_Weekly_Projects/Week_05_Linear_Factor_Model_OLS_Ridge_Lasso/`
- Implement Fama-French 5-factor model
- Compare OLS vs Ridge vs Lasso for factor selection
- Cross-validation for lambda selection
- Transaction cost analysis

**Interview Questions (5-7):**
- Derive the OLS closed-form solution
- When would you choose Ridge vs Lasso?
- What happens to Ridge coefficients as λ → ∞?

---

### Week 6: Classification (Logistic, SVM, Meta-Labeling)

**Theory:** `01_Theory/Core_ML_Weeks_05-12/Week_06_Classification_Logistic_SVM_MetaLabeling.md`

**Algorithms Covered:**

| Algorithm | Output | Decision Boundary | Key Hyperparameter |
|-----------|--------|-------------------|-------------------|
| Logistic Regression | P(y=1\|x) | Linear | C (inverse regularization) |
| Linear SVM | Class label | Maximum margin | C (regularization) |
| Triple-Barrier Method | Labels | Time-aware | Barrier widths |
| Meta-Labeling | Bet size | Secondary model | Threshold |

| Day | Notebook | Topic | Key Skills | Time |
|-----|----------|-------|------------|------|
| Mon | `Day_01_Logistic_Regression.ipynb` | Logistic regression | Sigmoid, cross-entropy, gradient | 4-5h |
| Tue | `Day_02_SVM_Classification.ipynb` | Linear SVM | Margin maximization, hinge loss | 4-5h |
| Wed | `Day_03_Triple_Barrier_Method.ipynb` | Triple barrier | Dynamic labeling, CUSUM filter | 4-5h |
| Thu | `Day_04_MetaLabeling_BetSize.ipynb` | Meta-labeling | Secondary classifier, bet sizing | 4-5h |
| Fri | `Day_05_Classification_Trading_Signals.ipynb` | Trading signals | Full pipeline with costs | 4-5h |
| Sat | `Day_06_Practice_Classification.ipynb` | Practice problems | ROC, precision-recall, calibration | 6-8h |
| Sun | `Day_07_Interview_Classification_Week6.ipynb` | Interview prep | Classification questions | 4-6h |

**Weekly Project:** `03_Weekly_Projects/Week_06_Classification_Trading_Signals_MetaLabeling/`
- Implement triple-barrier labeling
- Build meta-labeling framework
- Compare logistic vs SVM
- SHAP for feature importance

**Interview Questions (5-7):**
- Derive the logistic regression gradient
- Why is accuracy often wrong for trading signals?
- Explain meta-labeling and when to use it

---

### Week 7: Tree Ensembles (RF, GBM, XGBoost, LightGBM)

**Theory:** `01_Theory/Core_ML_Weeks_05-12/Week_07_Tree_Models_RF_GBM_XGBoost_LightGBM.md`

**Algorithms Covered:**

| Algorithm | Ensemble Type | Key Innovation | Speed |
|-----------|---------------|----------------|-------|
| Decision Tree | Single | Information gain, Gini | Fast |
| Random Forest | Bagging | Feature subsampling | Medium |
| GBM | Boosting | Sequential improvement | Slow |
| XGBoost | Boosting | Regularization, speed | Fast |
| LightGBM | Boosting | Histogram-based | Fastest |

| Day | Notebook | Topic | Key Skills | Time |
|-----|----------|-------|------------|------|
| Mon | `Day_01_Decision_Trees_CART.ipynb` | Decision trees | Splits, pruning, overfitting | 4-5h |
| Tue | `Day_02_Random_Forests.ipynb` | Random forests | Bagging, OOB error | 4-5h |
| Wed | `Day_03_Gradient_Boosting.ipynb` | Gradient boosting | Sequential fitting, shrinkage | 4-5h |
| Thu | `Day_04_XGBoost_LightGBM.ipynb` | XGBoost/LightGBM | Hyperparameter tuning | 4-5h |
| Fri | `Day_05_SHAP_Feature_Importance.ipynb` | Explainability | SHAP values, importance plots | 4-5h |
| Sat | `Day_06_Practice_Trees.ipynb` | Practice problems | Implementation + tuning | 6-8h |
| Sun | `Day_07_Interview_Trees_Week7.ipynb` | Interview prep | Tree algorithm questions | 4-6h |

**Weekly Project:** `03_Weekly_Projects/Week_07_Tree_Ensemble_Alpha_Factors_XGBoost/`
- Build alpha factor discovery pipeline
- Compare RF vs XGBoost vs LightGBM
- SHAP analysis for factor importance
- Cross-validation with purging

**Interview Questions (5-7):**
- How does bagging reduce variance?
- Why does boosting reduce bias?
- What are SHAP values and how do you interpret them?

---

### Week 8: Instance-Based Methods (kNN, SVM Regression)

**Theory:** `01_Theory/Core_ML_Weeks_05-12/Week_08_Instance_Methods_KNN_and_SVM_Regression.md`

**Algorithms Covered:**

| Algorithm | Type | Key Idea | Hyperparameters |
|-----------|------|----------|-----------------|
| kNN | Non-parametric | Nearest neighbors | k, distance metric |
| SVR | Kernel-based | ε-insensitive tube | C, ε, kernel |
| Kernel SVM | Kernel-based | Feature mapping | C, γ, kernel |

| Day | Notebook | Topic | Key Skills | Time |
|-----|----------|-------|------------|------|
| Mon | `Day_01_KNN_Implementation.ipynb` | k-Nearest Neighbors | Distance metrics, k selection | 4-5h |
| Tue | `Day_02_KNN_Regime_Detection.ipynb` | Regime detection | Historical similarity signals | 4-5h |
| Wed | `Day_03_SVM_Kernels.ipynb` | Kernel methods | RBF, polynomial kernels | 4-5h |
| Thu | `Day_04_SVR_Regression.ipynb` | Support Vector Regression | ε-tube, margin | 4-5h |
| Fri | `Day_05_Instance_Trading_Strategies.ipynb` | Trading strategies | Combining kNN and SVR | 4-5h |
| Sat | `Day_06_Practice_Instance_Methods.ipynb` | Practice problems | Implementation challenges | 6-8h |
| Sun | `Day_07_Interview_Instance_Week8.ipynb` | Interview prep | Kernel trick, distance questions | 4-6h |

**Weekly Project:** `03_Weekly_Projects/Week_08_SVM_KNN_Regime_Classification/`
- Build regime detection with kNN
- Compare with SVM classification
- Feature scaling importance
- Backtesting with regime awareness

**Interview Questions (5-7):**
- Explain the kernel trick
- How do you choose k in kNN?
- What is the curse of dimensionality?

---

### Week 9: Unsupervised Learning (PCA, Clustering, HMM, Anomaly)

**Theory:** `01_Theory/Core_ML_Weeks_05-12/Week_09_Unsupervised_PCA_Clustering_HMM_Anomaly.md`

**Algorithms Covered:**

| Algorithm | Type | Output | Use Case |
|-----------|------|--------|----------|
| PCA | Dimensionality reduction | Principal components | Factor compression |
| k-Means | Hard clustering | Cluster labels | Asset grouping |
| Hierarchical | Hard clustering | Dendrogram | Portfolio structure |
| HMM | Sequence model | Hidden states | Regime detection |
| GMM | Soft clustering | Probabilities | Regime mixing |
| Isolation Forest | Anomaly detection | Anomaly scores | Tail events |

| Day | Notebook | Topic | Key Skills | Time |
|-----|----------|-------|------------|------|
| Mon | `Day_01_PCA_Factor_Compression.ipynb` | PCA | Eigendecomposition, variance explained | 4-5h |
| Tue | `Day_02_KMeans_Clustering.ipynb` | k-Means | Elbow method, silhouette | 4-5h |
| Wed | `Day_03_Hierarchical_Clustering.ipynb` | Hierarchical | Dendrograms, linkage | 4-5h |
| Thu | `Day_04_HMM_Regime_Detection.ipynb` | Hidden Markov Models | State transitions, Viterbi | 4-5h |
| Fri | `Day_05_Isolation_Forest_Anomaly.ipynb` | Anomaly detection | Isolation, LOF | 4-5h |
| Sat | `Day_06_Practice_Unsupervised.ipynb` | Practice problems | Implementation challenges | 6-8h |
| Sun | `Day_07_Interview_Unsupervised_Week9.ipynb` | Interview prep | Clustering, PCA questions | 4-6h |

**Weekly Project:** `03_Weekly_Projects/Week_09_PCA_HMM_Clustering_for_Regimes/`
- PCA for factor compression
- HMM regime detection
- Cluster-based allocation
- Anomaly-aware risk management

**Interview Questions (5-7):**
- How many principal components to keep?
- Explain the EM algorithm for GMM
- How does Isolation Forest detect anomalies?

---

### Week 10: Time Series Models (ARIMA, VAR, GARCH)

**Theory:** `01_Theory/Core_ML_Weeks_05-12/Week_10_TimeSeries_ARIMA_VAR_GARCH_StatModels.md`

**Algorithms Covered:**

| Model | Type | Application | Key Parameters |
|-------|------|-------------|----------------|
| AR(p) | Univariate | Return autocorrelation | p (lags) |
| MA(q) | Univariate | Shock persistence | q (lags) |
| ARIMA(p,d,q) | Univariate | Non-stationary series | p, d, q |
| VAR | Multivariate | Cross-asset dynamics | p (lags) |
| GARCH(p,q) | Volatility | Variance forecasting | p, q |
| EGARCH | Asymmetric vol | Leverage effect | - |

| Day | Notebook | Topic | Key Skills | Time |
|-----|----------|-------|------------|------|
| Mon | `Day_01_Stationarity_Tests.ipynb` | Stationarity | ADF, KPSS, differencing | 4-5h |
| Tue | `Day_02_AR_MA_ARIMA.ipynb` | ARIMA models | ACF, PACF, order selection | 4-5h |
| Wed | `Day_03_VAR_Multivariate.ipynb` | Vector AR | Granger causality, IRF | 4-5h |
| Thu | `Day_04_GARCH_Volatility.ipynb` | GARCH models | Conditional variance | 4-5h |
| Fri | `Day_05_TimeSeries_Forecasting_Strategy.ipynb` | Trading strategy | Forecast-based signals | 4-5h |
| Sat | `Day_06_Practice_TimeSeries.ipynb` | Practice problems | Model selection, forecasting | 6-8h |
| Sun | `Day_07_Interview_TimeSeries_Week10.ipynb` | Interview prep | Time series questions | 4-6h |

**Weekly Project:** `03_Weekly_Projects/Week_10_ARIMA_GARCH_Forecasting_Strategy/`
- ARIMA for return forecasting
- GARCH for volatility forecasting
- Combined signal strategy
- Walk-forward validation

**Interview Questions (5-7):**
- How do you test for stationarity?
- Explain GARCH(1,1) and interpret parameters
- What is Granger causality?

---

### Week 11: Feature Engineering & Explainability

**Theory:** `01_Theory/Core_ML_Weeks_05-12/Week_11_Feature_Engineering_Explainability_SHAP_LIME.md`

**Techniques Covered:**

| Category | Technique | Purpose |
|----------|-----------|---------|
| Feature Engineering | Fractional differentiation | Stationarity with memory |
| Feature Engineering | Lag features | Autocorrelation capture |
| Feature Engineering | Rolling statistics | Dynamic features |
| Explainability | SHAP | Global + local importance |
| Explainability | LIME | Local approximation |
| Explainability | Partial Dependence | Feature effects |

| Day | Notebook | Topic | Key Skills | Time |
|-----|----------|-------|------------|------|
| Mon | `Day_01_Fractional_Differentiation.ipynb` | Fractional diff | Memory preservation | 4-5h |
| Tue | `Day_02_Feature_Engineering_Finance.ipynb` | Finance features | Technical indicators, ratios | 4-5h |
| Wed | `Day_03_SHAP_Deep_Dive.ipynb` | SHAP values | TreeSHAP, KernelSHAP | 4-5h |
| Thu | `Day_04_LIME_Local_Explanations.ipynb` | LIME | Local surrogates | 4-5h |
| Fri | `Day_05_Feature_Selection_Methods.ipynb` | Feature selection | Filter, wrapper, embedded | 4-5h |
| Sat | `Day_06_Practice_FE_Explainability.ipynb` | Practice problems | Feature pipelines | 6-8h |
| Sun | `Day_07_Interview_Explainability_Week11.ipynb` | Interview prep | ML interpretability questions | 4-6h |

**Weekly Project:** `03_Weekly_Projects/Week_11_Feature_Library_with_SHAP_Explainability/`
- Build feature engineering library
- Implement fractional differentiation
- SHAP analysis for all features
- Feature selection pipeline

**Interview Questions (5-7):**
- Explain SHAP values mathematically
- How do you handle non-stationary features?
- What is the difference between global and local explainability?

---

### Week 12: Advanced Backtesting & Cross-Validation

**Theory:** `01_Theory/Core_ML_Weeks_05-12/Week_12_Backtesting_TransactionCosts_CrossValidation_RiskMetrics.md`

**Techniques Covered:**

| Category | Technique | Purpose |
|----------|-----------|---------|
| CV | Purged k-Fold | Remove leakage |
| CV | Combinatorial Purged CV | Multiple paths |
| CV | Walk-Forward | Realistic retraining |
| Costs | Market Impact | Large order costs |
| Costs | Slippage | Execution uncertainty |
| Validation | Deflated Sharpe | Multiple testing |

| Day | Notebook | Topic | Key Skills | Time |
|-----|----------|-------|------------|------|
| Mon | `Day_01_Purged_KFold_CV.ipynb` | Purged CV | Information leakage prevention | 4-5h |
| Tue | `Day_02_CPCV_Implementation.ipynb` | Combinatorial purged CV | Multiple train/test paths | 4-5h |
| Wed | `Day_03_Transaction_Costs.ipynb` | Transaction costs | Spread, impact, slippage | 4-5h |
| Thu | `Day_04_Deflated_Sharpe.ipynb` | Multiple testing | Sharpe haircut | 4-5h |
| Fri | `Day_05_Advanced_Backtesting_Framework.ipynb` | Full framework | Production backtester | 4-5h |
| Sat | `Day_06_Practice_Backtesting.ipynb` | Practice problems | Validation exercises | 6-8h |
| Sun | `Day_07_Interview_Backtesting_Week12.ipynb` | Interview prep | Backtesting pitfalls questions | 4-6h |

**Weekly Project:** `03_Weekly_Projects/Week_12_Advanced_Backtesting_CPCV_DeflatedSharpe_TCA/`
- Full backtesting framework
- Purged and embargoed CV
- Transaction cost analysis
- Deflated Sharpe calculation

**Interview Questions (5-7):**
- How do you prevent overfitting in backtesting?
- Explain the deflated Sharpe ratio
- What is the multiple comparisons problem?

---

## Phase 3: Advanced (Weeks 13-20)

### Week 13: Deep Learning - Feedforward Networks

**Theory:** `01_Theory/Advanced_Weeks_13-20/Week_13_Deep_Learning_MLP_Regularization_Dropout.md`

**Topics Covered:**

| Component | Details |
|-----------|---------|
| Architecture | MLP, layer design, width vs depth |
| Activations | ReLU, tanh, sigmoid, Leaky ReLU |
| Optimization | SGD, Adam, learning rate scheduling |
| Regularization | L1/L2, Dropout, Batch Norm |
| Training | Early stopping, validation curves |

| Day | Notebook | Topic | Key Skills | Time |
|-----|----------|-------|------------|------|
| Mon | `Day_01_MLP_From_Scratch.ipynb` | MLP implementation | Forward pass, backprop | 4-5h |
| Tue | `Day_02_Activation_Functions.ipynb` | Activations | Gradient flow, dead neurons | 4-5h |
| Wed | `Day_03_Optimization_Algorithms.ipynb` | Optimizers | SGD, momentum, Adam | 4-5h |
| Thu | `Day_04_Regularization_Techniques.ipynb` | Regularization | Dropout, batch norm | 4-5h |
| Fri | `Day_05_Deep_Factor_Model.ipynb` | Finance application | Non-linear factors | 4-5h |
| Sat | `Day_06_Practice_Deep_Learning.ipynb` | Practice problems | PyTorch exercises | 6-8h |
| Sun | `Day_07_Interview_DeepLearning_Week13.ipynb` | Interview prep + **MOCK INTERVIEW #1** | Full mock (3 hours) | 4-6h |

**Weekly Project:** `03_Weekly_Projects/Week_13_Deep_MLP_Factor_Prediction/`
- MLP for factor prediction
- Hyperparameter tuning
- SHAP for neural net interpretation
- Comparison with tree ensembles

---

### Week 14: Sequence Models (LSTM, GRU, Attention)

**Theory:** `01_Theory/Advanced_Weeks_13-20/Week_14_Sequence_Models_LSTM_GRU_Attention_Transformers.md`

**Architectures Covered:**

| Model | Key Innovation | Parameters | Use Case |
|-------|----------------|------------|----------|
| RNN | Sequential processing | O(h²) | Short sequences |
| LSTM | Gating, long memory | O(4h²) | Long-term patterns |
| GRU | Simplified gating | O(3h²) | Efficient sequences |
| Attention | Variable focus | O(n²d) | Important timesteps |

| Day | Notebook | Topic | Key Skills | Time |
|-----|----------|-------|------------|------|
| Mon | `Day_01_RNN_Fundamentals.ipynb` | RNN basics | Sequential data, BPTT | 4-5h |
| Tue | `Day_02_LSTM_Implementation.ipynb` | LSTM | Gates, cell state | 4-5h |
| Wed | `Day_03_GRU_Comparison.ipynb` | GRU | Reset/update gates | 4-5h |
| Thu | `Day_04_Attention_Mechanisms.ipynb` | Attention | Self-attention, scoring | 4-5h |
| Fri | `Day_05_Sequence_Trading_Strategy.ipynb` | Finance application | Price prediction | 4-5h |
| Sat | `Day_06_Practice_Sequence_Models.ipynb` | Practice problems | Architecture design | 6-8h |
| Sun | `Day_07_Interview_Sequence_Week14.ipynb` | Interview prep + **MOCK INTERVIEW #2** | Full mock | 4-6h |

**Weekly Project:** `03_Weekly_Projects/Week_14_LSTM_Sequence_Prediction_with_Attention/`
- LSTM price prediction
- Attention visualization
- Walk-forward validation
- Transaction cost impact

---

### Week 15: Reinforcement Learning

**Theory:** `01_Theory/Advanced_Weeks_13-20/Week_15_Reinforcement_Learning_MAB_QLearning_DQN_PPO.md`

**Algorithms Covered:**

| Algorithm | Type | Key Concept | Complexity |
|-----------|------|-------------|------------|
| ε-greedy | Bandit | Simple exploration | Low |
| Thompson Sampling | Bandit | Bayesian exploration | Low |
| Q-Learning | Tabular | Value iteration | Medium |
| DQN | Deep RL | Function approximation | High |
| PPO | Policy gradient | Stable training | High |

| Day | Notebook | Topic | Key Skills | Time |
|-----|----------|-------|------------|------|
| Mon | `Day_01_MultiArmed_Bandits.ipynb` | MAB | Exploration vs exploitation | 4-5h |
| Tue | `Day_02_Thompson_Sampling.ipynb` | Bayesian bandits | Posterior sampling | 4-5h |
| Wed | `Day_03_QLearning_Tabular.ipynb` | Q-learning | Bellman equation | 4-5h |
| Thu | `Day_04_DQN_Implementation.ipynb` | Deep Q-Network | Experience replay, target net | 4-5h |
| Fri | `Day_05_RL_Trading_Agent.ipynb` | Trading agent | Reward design | 4-5h |
| Sat | `Day_06_Practice_RL.ipynb` | Practice problems | RL environments | 6-8h |
| Sun | `Day_07_Interview_RL_Week15.ipynb` | Interview prep + **MOCK INTERVIEW #3** | Full mock | 4-6h |

**Weekly Project:** `03_Weekly_Projects/Week_15_RL_Trading_Agent_DQN_Thompson_Sampling/`
- Thompson Sampling for strategy selection
- DQN trading agent
- Reward shaping experiments
- Comparison with supervised baseline

---

### Week 16: Options & Deep Hedging

**Theory:** `01_Theory/Advanced_Weeks_13-20/Week_16_Options_Pricing_BlackScholes_Greeks_VolSurface_DeepHedging.md`

| Day | Notebook | Topic | Key Skills | Time |
|-----|----------|-------|------------|------|
| Mon | `Day_01_BlackScholes_Derivation.ipynb` | Black-Scholes | PDE, assumptions | 4-5h |
| Tue | `Day_02_Greeks_Implementation.ipynb` | Greeks | Delta, gamma, vega, theta | 4-5h |
| Wed | `Day_03_Implied_Volatility_Surface.ipynb` | Vol surface | Smile, term structure | 4-5h |
| Thu | `Day_04_Delta_Hedging.ipynb` | Delta hedging | Dynamic rebalancing | 4-5h |
| Fri | `Day_05_Deep_Hedging.ipynb` | Deep hedging | NN for hedging | 4-5h |
| Sat | `Day_06_Practice_Options.ipynb` | Practice problems | Pricing, Greeks | 6-8h |
| Sun | `Day_07_Interview_Options_Week16.ipynb` | Interview prep + **MOCK INTERVIEW #4** | Full mock | 4-6h |

**Weekly Project:** `03_Weekly_Projects/Week_16_Options_Pricer_VolSurface_DeepHedging/`
- Options pricer with Greeks
- Vol surface modeling
- Deep hedging implementation
- Market making simulation

---

### Week 17: Portfolio Optimization

**Theory:** `01_Theory/Advanced_Weeks_13-20/Week_17_Portfolio_Optimization_Markowitz_BlackLitterman_RiskParity.md`

| Method | Innovation | Inputs Required |
|--------|------------|-----------------|
| Markowitz | Mean-variance | μ, Σ |
| Black-Litterman | Investor views | μ_mkt, views, uncertainty |
| Risk Parity | Equal risk | Σ only |
| HRP | Correlation clustering | Σ only |

| Day | Notebook | Topic | Key Skills | Time |
|-----|----------|-------|------------|------|
| Mon | `Day_01_Markowitz_MVO.ipynb` | Mean-variance | Efficient frontier | 4-5h |
| Tue | `Day_02_BlackLitterman.ipynb` | Black-Litterman | Views, equilibrium | 4-5h |
| Wed | `Day_03_Risk_Parity.ipynb` | Risk parity | Equal risk contribution | 4-5h |
| Thu | `Day_04_HRP_Implementation.ipynb` | Hierarchical RP | Clustering, allocation | 4-5h |
| Fri | `Day_05_Multi_Strategy_Allocation.ipynb` | Strategy allocation | Combining signals | 4-5h |
| Sat | `Day_06_Practice_Portfolio.ipynb` | Practice problems | Optimization exercises | 6-8h |
| Sun | `Day_07_Interview_Portfolio_Week17.ipynb` | Interview prep | Portfolio theory questions | 4-6h |

**Weekly Project:** `03_Weekly_Projects/Week_17_Multi_Strategy_Portfolio_Optimizer/`
- Compare all optimization methods
- Transaction cost aware rebalancing
- Risk constraints implementation
- Stress testing

---

### Week 18: NLP & Alternative Data

**Theory:** `01_Theory/Advanced_Weeks_13-20/Week_18_Alternative_Data_NLP_Sentiment_ESG_Embeddings.md`

| Method | Type | Output |
|--------|------|--------|
| TF-IDF | Frequency | Sparse vectors |
| Word2Vec | Embedding | Dense vectors |
| FinBERT | Transformer | Sentiment scores |
| NER | Extraction | Entities |

| Day | Notebook | Topic | Key Skills | Time |
|-----|----------|-------|------------|------|
| Mon | `Day_01_Text_Preprocessing_TFIDF.ipynb` | Text processing | Tokenization, TF-IDF | 4-5h |
| Tue | `Day_02_Word_Embeddings.ipynb` | Embeddings | Word2Vec, GloVe | 4-5h |
| Wed | `Day_03_FinBERT_Sentiment.ipynb` | FinBERT | Financial sentiment | 4-5h |
| Thu | `Day_04_News_Trading_Signals.ipynb` | News signals | Event detection | 4-5h |
| Fri | `Day_05_NLP_Alpha_Strategy.ipynb` | Full pipeline | Sentiment-based trading | 4-5h |
| Sat | `Day_06_Practice_NLP.ipynb` | Practice problems | NLP exercises | 6-8h |
| Sun | `Day_07_Interview_NLP_Week18.ipynb` | Interview prep | Alternative data questions | 4-6h |

**Weekly Project:** `03_Weekly_Projects/Week_18_NLP_Sentiment_Trading_BERT_FinBERT/`
- FinBERT sentiment analysis
- News event impact analysis
- Sentiment-factor strategy
- Latency considerations

---

### Week 19: Bayesian Methods

**Theory:** `01_Theory/Advanced_Weeks_13-20/Week_19_Bayesian_Methods_BMA_Kalman_GaussianProcesses.md`

| Method | Application | Key Advantage |
|--------|-------------|---------------|
| Bayesian Linear | Uncertainty | Posterior distribution |
| BMA | Model averaging | Model uncertainty |
| Kalman Filter | State estimation | Online updating |
| Gaussian Process | Non-parametric | Uncertainty bands |

| Day | Notebook | Topic | Key Skills | Time |
|-----|----------|-------|------------|------|
| Mon | `Day_01_Bayesian_Linear_Regression.ipynb` | Bayesian regression | Prior, posterior, credible intervals | 4-5h |
| Tue | `Day_02_Bayesian_Model_Averaging.ipynb` | BMA | Model weights | 4-5h |
| Wed | `Day_03_Kalman_Filter.ipynb` | Kalman filter | State-space, prediction | 4-5h |
| Thu | `Day_04_Gaussian_Processes.ipynb` | GPs | Kernel selection, uncertainty | 4-5h |
| Fri | `Day_05_Bayesian_Trading_Strategy.ipynb` | Finance application | Adaptive portfolio | 4-5h |
| Sat | `Day_06_Practice_Bayesian.ipynb` | Practice problems | Bayesian inference | 6-8h |
| Sun | `Day_07_Interview_Bayesian_Week19.ipynb` | Interview prep | Bayesian questions | 4-6h |

**Weekly Project:** `03_Weekly_Projects/Week_19_Bayesian_Kalman_Adaptive_Portfolio/`
- Kalman filter for signal extraction
- Bayesian portfolio optimization
- Uncertainty-aware position sizing
- Online updating

---

### Week 20: Market Microstructure & HFT

**Theory:** `01_Theory/Advanced_Weeks_13-20/Week_20_Market_Microstructure_HFT_LOB_Execution_Algos.md`

| Topic | Latency | Application |
|-------|---------|-------------|
| LOB Modeling | μs-ms | Order flow prediction |
| Hawkes Processes | ms | Event clustering |
| Optimal Execution | s-min | TWAP/VWAP/IS |
| Market Making | μs-ms | Inventory management |

| Day | Notebook | Topic | Key Skills | Time |
|-----|----------|-------|------------|------|
| Mon | `Day_01_Limit_Order_Book.ipynb` | LOB | Depth, imbalance | 4-5h |
| Tue | `Day_02_Hawkes_Processes.ipynb` | Hawkes | Event intensity | 4-5h |
| Wed | `Day_03_Optimal_Execution.ipynb` | Execution | TWAP, VWAP, IS | 4-5h |
| Thu | `Day_04_Market_Making_Basics.ipynb` | Market making | Inventory, spread | 4-5h |
| Fri | `Day_05_HFT_Signals.ipynb` | HFT signals | Short-term prediction | 4-5h |
| Sat | `Day_06_Practice_Microstructure.ipynb` | Practice problems | LOB exercises | 6-8h |
| Sun | `Day_07_Interview_Microstructure_Week20.ipynb` | Interview prep | HFT questions | 4-6h |

**Weekly Project:** `03_Weekly_Projects/Week_20_HFT_Microstructure_LOB_Analysis/`
- LOB feature engineering
- Order flow imbalance signals
- Execution algorithm comparison
- Latency analysis

---

## Phase 4: Production (Weeks 21-24)

### Week 21: System Design

**Theory:** `01_Theory/Production_Weeks_21-24/Week_21_System_Design_Architecture_Latency_Scalability.md`

| Day | Notebook | Topic | Key Skills | Time |
|-----|----------|-------|------------|------|
| Mon | `Day_01_Research_Platform_Architecture.ipynb` | Architecture | Components, data flow | 4-5h |
| Tue | `Day_02_Database_Design_TickData.ipynb` | Database | Time-series DBs, partitioning | 4-5h |
| Wed | `Day_03_API_Development.ipynb` | APIs | REST, WebSocket | 4-5h |
| Thu | `Day_04_Latency_Optimization.ipynb` | Latency | Profiling, bottlenecks | 4-5h |
| Fri | `Day_05_Scalability_Patterns.ipynb` | Scalability | Horizontal scaling | 4-5h |
| Sat | `Day_06_Practice_SystemDesign.ipynb` | Practice problems | Design exercises | 6-8h |
| Sun | `Day_07_Interview_SystemDesign_Week21.ipynb` | Interview prep | System design questions | 4-6h |

**Weekly Project:** `03_Weekly_Projects/Week_21_Research_Platform_Design_and_Implementation/`
- Design complete research platform
- Database schema for tick data
- API for signal generation
- Documentation

---

### Week 22: Real-Time Systems

**Theory:** `01_Theory/Production_Weeks_21-24/Week_22_Real_Time_Pipelines_Streaming_EventDriven.md`

| Day | Notebook | Topic | Key Skills | Time |
|-----|----------|-------|------------|------|
| Mon | `Day_01_Streaming_Data_Processing.ipynb` | Streaming | Data pipelines | 4-5h |
| Tue | `Day_02_Event_Driven_Architecture.ipynb` | Event-driven | Publishers, subscribers | 4-5h |
| Wed | `Day_03_Message_Queues.ipynb` | Queues | Redis, RabbitMQ concepts | 4-5h |
| Thu | `Day_04_Low_Latency_Python.ipynb` | Performance | NumPy, Cython | 4-5h |
| Fri | `Day_05_RealTime_Trading_System.ipynb` | Full system | Integration | 4-5h |
| Sat | `Day_06_Practice_RealTime.ipynb` | Practice problems | Streaming exercises | 6-8h |
| Sun | `Day_07_Interview_RealTime_Week22.ipynb` | Interview prep | Production questions | 4-6h |

**Weekly Project:** `03_Weekly_Projects/Week_22_Real_Time_Execution_System/`
- Real-time data ingestion
- Signal generation pipeline
- Simulated execution
- Monitoring

---

### Week 23: Production ML

**Theory:** `01_Theory/Production_Weeks_21-24/Week_23_Production_ML_AlphaDecay_Monitoring_OnlineLearning_ABTesting.md`

| Day | Notebook | Topic | Key Skills | Time |
|-----|----------|-------|------------|------|
| Mon | `Day_01_Alpha_Decay_Detection.ipynb` | Alpha decay | Signal degradation | 4-5h |
| Tue | `Day_02_Concept_Drift_Detection.ipynb` | Drift | Distribution shifts | 4-5h |
| Wed | `Day_03_Online_Learning.ipynb` | Online learning | Incremental updates | 4-5h |
| Thu | `Day_04_AB_Testing_Strategies.ipynb` | A/B testing | Statistical comparison | 4-5h |
| Fri | `Day_05_Monitoring_Dashboard.ipynb` | Monitoring | Performance tracking | 4-5h |
| Sat | `Day_06_Practice_ProductionML.ipynb` | Practice problems | MLOps exercises | 6-8h |
| Sun | `Day_07_Interview_ProductionML_Week23.ipynb` | Interview prep | Production ML questions | 4-6h |

**Weekly Project:** `03_Weekly_Projects/Week_23_Production_Monitoring_AlphaDecay_Dashboard/`
- Alpha decay monitoring
- Drift detection pipeline
- Retraining triggers
- Performance dashboard

---

### Week 24: Capstone Integration

**Theory:** `01_Theory/Production_Weeks_21-24/Week_24_Capstone_Integration_Documentation_Deployment.md`

| Day | Notebook | Topic | Key Skills | Time |
|-----|----------|-------|------------|------|
| Mon | `Day_01_Capstone_Final_Integration.ipynb` | Integration | Combining components | 4-5h |
| Tue | `Day_02_Documentation_Standards.ipynb` | Documentation | Sphinx, docstrings | 4-5h |
| Wed | `Day_03_Testing_Coverage.ipynb` | Testing | Unit, integration tests | 4-5h |
| Thu | `Day_04_Presentation_Preparation.ipynb` | Presentation | Slides, talking points | 4-5h |
| Fri | `Day_05_Portfolio_Finalization.ipynb` | Portfolio | GitHub, LinkedIn | 4-5h |
| Sat | `Day_06_Final_Review.ipynb` | Review | All topics | 6-8h |
| Sun | `Day_07_Capstone_Presentation.ipynb` | Presentation | Final delivery | 4-6h |

**Weekly Project:** `03_Weekly_Projects/Week_24_Capstone_Final_Integration/`
- Complete capstone project
- Full documentation
- Presentation materials
- GitHub polish

---

## Interview Preparation Timeline

| Weeks | Focus | Daily Questions | Weekend Activity |
|-------|-------|-----------------|------------------|
| 1-4 | Foundation | 1-2 basic | Review concepts |
| 5-8 | Core ML | 2-3 intermediate | Algorithm practice |
| 9-12 | Advanced ML | 3-4 challenging | Timed exercises |
| **13-16** | **INTENSIVE** | **5+ company-specific** | **Full mock interviews** |
| 17-20 | Specialized | 3-4 advanced | Project explanations |
| 21-24 | Production | 2-3 system design | Capstone practice |

---

## Key Milestones

| Week | Milestone | Deliverable |
|------|-----------|-------------|
| 4 | Foundation Complete | Data pipeline + backtest framework |
| 8 | Core ML Complete | Factor models + classification signals |
| 12 | Validation Complete | Production-grade backtesting |
| 13 | First Mock Interview | Full 3-hour mock |
| 16 | Advanced ML Complete | Deep learning + RL agents |
| 20 | Specialized Models Complete | Options, NLP, Bayesian, HFT |
| 24 | Program Complete | Capstone + portfolio ready |

---

## Daily Checklist Template

```
Date: _______________
Week: ___ / 24
Day: ___ (Mon-Sun)

[ ] Morning: Theory reading (1-1.5 hours)
    - Chapter/section: _______________
    - Key concepts: _______________

[ ] Afternoon: Daily notebook (2-3 hours)
    - Notebook: _______________
    - Completed sections: _______________
    - Timed challenge result: _______________

[ ] Evening: Interview prep (1-2 hours)
    - Questions solved: _______________
    - Project progress: _______________

[ ] Updated PROGRESS_TRACKER.md

Total hours today: ___
Confidence level (1-10): ___
Questions for tomorrow: _______________
```

---

*"A journey of 24 weeks begins with Day 1. Start today."*
