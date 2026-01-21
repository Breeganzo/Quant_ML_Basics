# Week 8: Machine Learning for Trading

## Table of Contents
1. [Overview of ML in Trading](#1-overview-of-ml-in-trading)
2. [Tree-Based Models](#2-tree-based-models)
3. [Ensemble Methods](#3-ensemble-methods)
4. [Support Vector Machines](#4-support-vector-machines)
5. [Feature Importance and Selection](#5-feature-importance-and-selection)
6. [Hyperparameter Tuning](#6-hyperparameter-tuning)
7. [Model Deployment Considerations](#7-model-deployment-considerations)

---

## 1. Overview of ML in Trading

### The ML Trading Pipeline

```
Data → Features → Train/Test Split → Model → Backtest → Deploy → Monitor
```

### Key Challenges in Finance

| Challenge | Description | Solution |
|-----------|-------------|----------|
| Non-stationarity | Relationships change over time | Rolling windows, regime detection |
| Low signal-to-noise | Markets are efficient | Feature engineering, ensembles |
| Look-ahead bias | Using future information | Careful cross-validation |
| Overfitting | Too many parameters | Regularization, simpler models |
| Transaction costs | Erode profits | Include in objective function |

### Prediction Tasks

| Task Type | Target Variable | Example |
|-----------|-----------------|---------|
| Regression | Continuous | Return prediction |
| Classification | Discrete | Direction (up/down) |
| Ranking | Relative order | Best stocks to buy |
| Probability | Calibrated probability | P(crash) > 5% |

### The Fundamental Equation

For a trading signal $s_t$:

$$\text{Strategy Return}_t = s_{t-1} \times r_t - c|s_t - s_{t-1}|$$

Where:
- $s_{t-1}$ = Position at time t-1
- $r_t$ = Asset return at time t
- $c$ = Transaction cost

---

## 2. Tree-Based Models

### Decision Trees

A tree splits data recursively based on feature thresholds.

**Structure:**
```
                [Feature₁ < 0.5?]
                 /              \
              Yes                No
              /                    \
    [Feature₂ < 0.3?]          [Leaf: Class B]
       /         \
     Yes          No
      /             \
[Leaf: A]      [Leaf: B]
```

### Splitting Criteria

**For Classification - Gini Impurity:**
$$Gini = 1 - \sum_{k=1}^{K} p_k^2$$

Where $p_k$ = proportion of class k in node.

**For Classification - Entropy:**
$$Entropy = -\sum_{k=1}^{K} p_k \log_2(p_k)$$

**Information Gain:**
$$IG = Entropy_{parent} - \sum_{i} \frac{n_i}{n} Entropy_{child_i}$$

**For Regression - MSE:**
$$MSE = \frac{1}{n}\sum_{i=1}^{n}(y_i - \bar{y})^2$$

### Example: Gini Calculation

**Node with 100 samples:** 70 Class A, 30 Class B

$$Gini = 1 - (0.7)^2 - (0.3)^2 = 1 - 0.49 - 0.09 = 0.42$$

**After split:**
- Left: 60 A, 10 B → Gini = 1 - 0.86² - 0.14² = 0.24
- Right: 10 A, 20 B → Gini = 1 - 0.33² - 0.67² = 0.44

**Weighted Gini:**
$$Gini_{split} = \frac{70}{100}(0.24) + \frac{30}{100}(0.44) = 0.168 + 0.132 = 0.30$$

**Gini Reduction:** 0.42 - 0.30 = 0.12 ✓

### Tree Hyperparameters

| Parameter | Effect | Too Small | Too Large |
|-----------|--------|-----------|-----------|
| max_depth | Tree depth | Underfit | Overfit |
| min_samples_split | Min samples to split | Overfit | Underfit |
| min_samples_leaf | Min samples in leaf | Overfit | Underfit |
| max_features | Features per split | Underfit | Overfit |

### Decision Tree for Trading

**Features:**
- 5-day momentum
- 20-day volatility
- Volume ratio

**Target:** Next day direction (Up=1, Down=0)

**Example Tree:**
```
[Momentum > 2%?]
    Yes → [Vol < 15%?]
              Yes → Buy (70% win rate)
              No → Hold (55% win rate)
    No → [Volume Ratio > 1.5?]
              Yes → Sell (65% win rate)
              No → Hold (50% win rate)
```

---

## 3. Ensemble Methods

### Why Ensembles?

Combine multiple models to reduce variance and improve predictions.

$$\text{Ensemble Prediction} = f(\text{Model}_1, \text{Model}_2, ..., \text{Model}_n)$$

### Bagging (Bootstrap Aggregating)

**Algorithm:**
1. Create B bootstrap samples
2. Train tree on each sample
3. Average predictions (regression) or vote (classification)

**Variance Reduction:**
$$Var(\bar{X}) = \frac{\sigma^2}{n}$$ (for independent models)

### Random Forest

Bagging + Feature Randomization

**Key Difference:** Each split considers random subset of features.

$$m = \sqrt{p}$$ (typical for classification)
$$m = p/3$$ (typical for regression)

**Random Forest Prediction:**
$$\hat{y} = \frac{1}{B}\sum_{b=1}^{B} T_b(x)$$ (regression)

$$\hat{y} = \text{mode}\{T_1(x), T_2(x), ..., T_B(x)\}$$ (classification)

### Out-of-Bag (OOB) Error

Each tree trained on ~63.2% of data. Remaining 36.8% used for validation.

$$P(\text{not selected}) = \left(1 - \frac{1}{n}\right)^n \approx e^{-1} \approx 0.368$$

### Gradient Boosting

Build trees sequentially, each correcting errors of previous.

**Algorithm:**
1. Initialize $F_0(x) = \bar{y}$
2. For m = 1 to M:
   - Compute pseudo-residuals: $r_{im} = y_i - F_{m-1}(x_i)$
   - Fit tree $h_m$ to residuals
   - Update: $F_m(x) = F_{m-1}(x) + \nu \cdot h_m(x)$

**Learning Rate ($\nu$):** Controls step size (0.01 - 0.1 typical)

### XGBoost Objective

$$\mathcal{L} = \sum_{i=1}^{n} l(y_i, \hat{y}_i) + \sum_{k=1}^{K} \Omega(f_k)$$

**Regularization:**
$$\Omega(f) = \gamma T + \frac{1}{2}\lambda\sum_{j=1}^{T}w_j^2$$

Where:
- $T$ = number of leaves
- $w_j$ = leaf weights
- $\gamma, \lambda$ = regularization parameters

### Comparison Table

| Method | Trees | Training | Feature Sampling |
|--------|-------|----------|------------------|
| Bagging | Parallel | Fast | No |
| Random Forest | Parallel | Fast | Yes (per split) |
| Gradient Boosting | Sequential | Slower | Optional |
| XGBoost | Sequential | Optimized | Yes |

---

## 4. Support Vector Machines

### Linear SVM

Find hyperplane that maximizes margin between classes.

**Decision Boundary:**
$$f(x) = w^T x + b = 0$$

**Optimization:**
$$\min_{w,b} \frac{1}{2}||w||^2$$

Subject to: $y_i(w^T x_i + b) \geq 1$ for all i

**Margin:**
$$\text{Margin} = \frac{2}{||w||}$$

### Soft Margin SVM

Allow some misclassifications:

$$\min_{w,b,\xi} \frac{1}{2}||w||^2 + C\sum_{i=1}^{n}\xi_i$$

Subject to:
- $y_i(w^T x_i + b) \geq 1 - \xi_i$
- $\xi_i \geq 0$

**C Parameter:**
- Large C: Stricter margin, risk overfitting
- Small C: Softer margin, more regularization

### Kernel Trick

For non-linear boundaries, map to higher dimensions:

$$K(x_i, x_j) = \phi(x_i)^T \phi(x_j)$$

**Common Kernels:**

| Kernel | Formula | Use Case |
|--------|---------|----------|
| Linear | $x_i^T x_j$ | Linearly separable |
| Polynomial | $(x_i^T x_j + c)^d$ | Polynomial boundaries |
| RBF (Gaussian) | $\exp(-\gamma||x_i - x_j||^2)$ | Complex, local patterns |

### RBF Kernel Parameter

$$K(x_i, x_j) = \exp\left(-\gamma||x_i - x_j||^2\right)$$

**γ (gamma):**
- Large γ: Tight decision boundary, overfitting
- Small γ: Smooth boundary, underfitting

### SVM for Trading

**Classification:** Predict Up/Down
**Features:** Technical indicators, scaled to [0,1] or [-1,1]

**Important:** SVMs require feature scaling!

$$x_{scaled} = \frac{x - \mu}{\sigma}$$

---

## 5. Feature Importance and Selection

### Why Feature Selection?

- Reduce overfitting
- Improve interpretability
- Decrease training time
- Handle multicollinearity

### Impurity-Based Importance (Trees)

$$Importance_j = \sum_{nodes\ using\ j} \frac{n_{node}}{n_{total}} \times (\text{Impurity Reduction})$$

### Permutation Importance

1. Train model, get baseline score
2. For each feature j:
   - Shuffle feature j values
   - Compute score decrease
3. Importance = average score decrease

$$Importance_j = Score_{baseline} - Score_{permuted_j}$$

**Advantage:** Works for any model, captures interactions

### SHAP Values (SHapley Additive exPlanations)

Based on game theory - fair attribution of prediction.

$$\phi_j = \sum_{S \subseteq N \setminus \{j\}} \frac{|S|!(|N|-|S|-1)!}{|N|!}[f(S \cup \{j\}) - f(S)]$$

**Properties:**
- Sum of SHAP values = prediction - baseline
- Features with zero impact have zero SHAP
- Fair distribution among correlated features

### Feature Selection Methods

| Method | Type | Description |
|--------|------|-------------|
| Variance Threshold | Filter | Remove low variance features |
| Correlation Filter | Filter | Remove highly correlated |
| Mutual Information | Filter | Keep high MI with target |
| Recursive Feature Elimination | Wrapper | Iteratively remove worst |
| L1 Regularization | Embedded | Lasso sets coefficients to 0 |

### Recursive Feature Elimination (RFE)

**Algorithm:**
1. Fit model with all features
2. Rank features by importance
3. Remove least important
4. Repeat until desired number reached

---

## 6. Hyperparameter Tuning

### Grid Search

Exhaustive search over parameter grid.

**Example Grid:**
```python
param_grid = {
    'n_estimators': [100, 200, 500],
    'max_depth': [3, 5, 7, 10],
    'learning_rate': [0.01, 0.05, 0.1]
}
# Total combinations: 3 × 4 × 3 = 36
```

### Random Search

Sample random combinations.

**Advantage:** More efficient for large search spaces.

$$P(\text{finding good params}) = 1 - (1-p)^n$$

Where p = probability of good region, n = number of trials

### Bayesian Optimization

Use probabilistic model to guide search.

**Steps:**
1. Build surrogate model of objective function
2. Use acquisition function to select next point
3. Evaluate, update surrogate
4. Repeat

**Common Acquisition Functions:**
- Expected Improvement (EI)
- Upper Confidence Bound (UCB)

### Time Series Cross-Validation

**Walk-Forward:**
```
Fold 1: Train [1:100],    Test [101:110]
Fold 2: Train [1:110],    Test [111:120]
Fold 3: Train [1:120],    Test [121:130]
...
```

**Purged CV:** Add gap between train and test to prevent leakage.

```
Fold 1: Train [1:100], Gap [101:105], Test [106:115]
```

### Combinatorial Purged CV

For strategies with overlapping returns:

$$\text{Train periods and test periods should not overlap}$$

---

## 7. Model Deployment Considerations

### From Research to Production

| Stage | Considerations |
|-------|---------------|
| Training | Historical data, feature engineering |
| Validation | Out-of-sample performance |
| Paper Trading | Live data, no real money |
| Deployment | Real trades, monitoring |
| Maintenance | Retraining, drift detection |

### Model Monitoring

**Concept Drift:** Distribution of features changes
**Target Drift:** Distribution of outcomes changes

**Detection:**
- Track feature statistics over time
- Monitor prediction distribution
- Compare rolling performance to benchmark

### Position Sizing

**Kelly Criterion:**
$$f^* = \frac{p(b+1) - 1}{b}$$

Where:
- $f^*$ = fraction of capital to bet
- $p$ = probability of winning
- $b$ = odds (win amount / loss amount)

**Example:**
```
Win rate: 55% (p = 0.55)
Win/Loss ratio: 1.5 (b = 1.5)

f* = (0.55 × 2.5 - 1) / 1.5 = 0.375 / 1.5 = 25%
```

### Transaction Cost Modeling

**Components:**
- Commission: Fixed per trade
- Spread: Bid-ask spread
- Slippage: Price movement during execution
- Market Impact: Large orders move price

**Total Cost:**
$$TC = \text{Commission} + \frac{\text{Spread}}{2} + \text{Slippage} + \text{Impact}$$

### Regime Detection

Markets behave differently in different regimes:

| Regime | Characteristics | Strategy Adjustment |
|--------|-----------------|---------------------|
| Trending | Low volatility, momentum | Trend following |
| Mean-reverting | Range-bound | Mean reversion |
| Crisis | High volatility | Reduce exposure |

**Detection Methods:**
- Hidden Markov Models
- Rolling volatility thresholds
- Clustering

---

## Key Formulas Summary

| Concept | Formula |
|---------|---------|
| Gini Impurity | $1 - \sum_k p_k^2$ |
| Entropy | $-\sum_k p_k \log_2 p_k$ |
| RF Prediction | $\frac{1}{B}\sum_b T_b(x)$ |
| SVM Margin | $\frac{2}{||w||}$ |
| RBF Kernel | $\exp(-\gamma||x_i - x_j||^2)$ |
| Kelly Criterion | $\frac{p(b+1)-1}{b}$ |

---

## Practice Problems

1. **Gini Calculation:** Node has 80 samples (50 positive, 30 negative). Calculate Gini impurity.

2. **Random Forest:** Why does feature randomization reduce correlation between trees?

3. **SVM:** Data: X=[[1,2], [2,3], [3,3], [4,5]], Y=[0,0,1,1]. What is the margin for weight vector w=[1,1], b=-4?

4. **Kelly Criterion:** Strategy has 60% win rate, average win $200, average loss $100. What fraction to allocate?

5. **Walk-Forward CV:** Design a CV scheme for 500 days of data with train=200, test=20, gap=5.

---

*Next Week: Deep Learning Fundamentals*
