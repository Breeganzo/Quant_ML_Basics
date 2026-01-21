# Week 4: Machine Learning Foundations for Finance

## Table of Contents
1. [Machine Learning Overview](#1-machine-learning-overview)
2. [Supervised Learning: Regression](#2-supervised-learning-regression)
3. [Supervised Learning: Classification](#3-supervised-learning-classification)
4. [Model Evaluation](#4-model-evaluation)
5. [Regularization](#5-regularization)
6. [Cross-Validation](#6-cross-validation)
7. [Feature Engineering](#7-feature-engineering)

---

## 1. Machine Learning Overview

### Types of Machine Learning

| Type | Goal | Financial Examples |
|------|------|-------------------|
| **Supervised** | Predict output from labeled data | Price prediction, Default classification |
| **Unsupervised** | Find structure in unlabeled data | Clustering stocks, Dimensionality reduction |
| **Reinforcement** | Learn through trial and error | Algorithmic trading, Portfolio allocation |

### The Prediction Problem

Given features $\mathbf{X}$ and target $y$:

$$y = f(\mathbf{X}) + \epsilon$$

- $f$ = unknown true function
- $\hat{f}$ = our estimated function
- Goal: Find $\hat{f}$ that minimizes prediction error

### Bias-Variance Tradeoff

$$\text{Expected Error} = \text{Bias}^2 + \text{Variance} + \text{Irreducible Error}$$

| Component | Description | Effect |
|-----------|-------------|--------|
| **Bias** | Error from wrong assumptions | Underfitting |
| **Variance** | Error from sensitivity to training data | Overfitting |
| **Irreducible** | Noise in the data | Can't reduce |

**Key Insight:**
- Simple models → High bias, Low variance
- Complex models → Low bias, High variance
- Optimal model balances both

---

## 2. Supervised Learning: Regression

### Linear Regression

$$y = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + ... + \beta_p x_p + \epsilon$$

**Matrix Form:**
$$\mathbf{y} = \mathbf{X}\boldsymbol{\beta} + \boldsymbol{\epsilon}$$

**OLS Solution:**
$$\hat{\boldsymbol{\beta}} = (\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T\mathbf{y}$$

### Cost Function: Mean Squared Error

$$MSE = \frac{1}{n}\sum_{i=1}^{n}(y_i - \hat{y}_i)^2$$

**Gradient:**
$$\frac{\partial MSE}{\partial \beta_j} = -\frac{2}{n}\sum_{i=1}^{n}(y_i - \hat{y}_i)x_{ij}$$

### Gradient Descent

Iteratively update parameters to minimize cost:

$$\beta_j := \beta_j - \alpha \frac{\partial MSE}{\partial \beta_j}$$

Where $\alpha$ = learning rate

**Example: Simple Gradient Descent**
```
Initialize: β = 0, α = 0.01
For each iteration:
    1. Predict: ŷ = Xβ
    2. Calculate error: e = y - ŷ
    3. Calculate gradient: g = -(2/n) × Xᵀe
    4. Update: β = β - α × g
    5. Repeat until convergence
```

### Polynomial Regression

For non-linear relationships:

$$y = \beta_0 + \beta_1 x + \beta_2 x^2 + ... + \beta_d x^d + \epsilon$$

**Warning:** High-degree polynomials overfit easily.

---

## 3. Supervised Learning: Classification

### Logistic Regression

Predicts probability of binary outcome.

**Sigmoid Function:**
$$\sigma(z) = \frac{1}{1 + e^{-z}}$$

**Model:**
$$P(y=1|x) = \sigma(\beta_0 + \beta_1 x_1 + ... + \beta_p x_p)$$

**Properties of Sigmoid:**
- Maps any real number to (0, 1)
- $\sigma(0) = 0.5$
- $\sigma(-\infty) = 0$, $\sigma(\infty) = 1$

### Log-Odds (Logit)

$$\ln\left(\frac{P(y=1)}{1-P(y=1)}\right) = \beta_0 + \beta_1 x_1 + ... + \beta_p x_p$$

**Interpretation:** 
- $e^{\beta_j}$ = odds ratio for unit increase in $x_j$
- $\beta_j > 0$ → increases probability
- $\beta_j < 0$ → decreases probability

### Cost Function: Cross-Entropy Loss

$$L = -\frac{1}{n}\sum_{i=1}^{n}[y_i\ln(\hat{p}_i) + (1-y_i)\ln(1-\hat{p}_i)]$$

Where $\hat{p}_i = P(y_i = 1 | x_i)$

### Decision Boundary

Classify based on threshold (usually 0.5):

$$\hat{y} = \begin{cases} 1 & \text{if } P(y=1|x) \geq 0.5 \\ 0 & \text{if } P(y=1|x) < 0.5 \end{cases}$$

### Example: Predicting Stock Direction

**Problem:** Predict if stock goes up (1) or down (0) based on:
- Yesterday's return ($x_1$)
- Volume change ($x_2$)

**Model:** 
$$P(\text{up}) = \sigma(-0.5 + 2.1 \times x_1 + 0.3 \times x_2)$$

**Example Prediction:**
```
Yesterday's return = 1% = 0.01
Volume change = 20% = 0.20

z = -0.5 + 2.1(0.01) + 0.3(0.20)
  = -0.5 + 0.021 + 0.06
  = -0.419

P(up) = 1/(1 + e^0.419) = 0.397 = 39.7%

Prediction: Down (P < 0.5)
```

### Multi-class Classification

**Softmax Function:**
$$P(y=k|x) = \frac{e^{z_k}}{\sum_{j=1}^{K}e^{z_j}}$$

Where $z_k = \beta_{k0} + \beta_{k1}x_1 + ... + \beta_{kp}x_p$

---

## 4. Model Evaluation

### Regression Metrics

| Metric | Formula | Interpretation |
|--------|---------|----------------|
| **MSE** | $\frac{1}{n}\sum(y_i - \hat{y}_i)^2$ | Average squared error |
| **RMSE** | $\sqrt{MSE}$ | Same units as y |
| **MAE** | $\frac{1}{n}\sum|y_i - \hat{y}_i|$ | Average absolute error |
| **R²** | $1 - \frac{SS_{res}}{SS_{tot}}$ | Variance explained |
| **Adj R²** | $1 - \frac{(1-R^2)(n-1)}{n-p-1}$ | Penalizes more features |

### Classification Metrics

**Confusion Matrix:**

|  | Predicted + | Predicted - |
|--|-------------|-------------|
| **Actual +** | TP | FN |
| **Actual -** | FP | TN |

**Metrics:**

$$\text{Accuracy} = \frac{TP + TN}{TP + TN + FP + FN}$$

$$\text{Precision} = \frac{TP}{TP + FP}$$

$$\text{Recall (Sensitivity)} = \frac{TP}{TP + FN}$$

$$\text{Specificity} = \frac{TN}{TN + FP}$$

$$\text{F1 Score} = \frac{2 \times \text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}$$

### Example: Strategy Classification

**Results:**
- True Positives: 45 (correctly predicted up days)
- False Positives: 15 (predicted up, actually down)
- True Negatives: 30 (correctly predicted down)
- False Negatives: 10 (predicted down, actually up)

**Calculations:**
```
Accuracy = (45 + 30) / (45 + 15 + 30 + 10) = 75/100 = 75%
Precision = 45 / (45 + 15) = 45/60 = 75%
Recall = 45 / (45 + 10) = 45/55 = 81.8%
F1 = 2 × 0.75 × 0.818 / (0.75 + 0.818) = 78.3%
```

### ROC Curve and AUC

**ROC Curve:** Plot of TPR vs FPR at different thresholds
- **TPR (True Positive Rate)** = Recall = TP/(TP+FN)
- **FPR (False Positive Rate)** = FP/(FP+TN)

**AUC (Area Under Curve):**
- AUC = 0.5 → Random classifier
- AUC = 1.0 → Perfect classifier
- AUC > 0.7 → Acceptable
- AUC > 0.8 → Good

---

## 5. Regularization

### Why Regularize?

- Prevent overfitting
- Handle multicollinearity
- Feature selection (L1)

### Ridge Regression (L2)

Add penalty on sum of squared coefficients:

$$\min_\beta \left[\sum_{i=1}^{n}(y_i - \hat{y}_i)^2 + \lambda\sum_{j=1}^{p}\beta_j^2\right]$$

**Solution:**
$$\hat{\boldsymbol{\beta}}_{ridge} = (\mathbf{X}^T\mathbf{X} + \lambda\mathbf{I})^{-1}\mathbf{X}^T\mathbf{y}$$

**Effect:** Shrinks coefficients toward zero, but never exactly zero.

### Lasso Regression (L1)

Add penalty on sum of absolute coefficients:

$$\min_\beta \left[\sum_{i=1}^{n}(y_i - \hat{y}_i)^2 + \lambda\sum_{j=1}^{p}|\beta_j|\right]$$

**Effect:** 
- Shrinks coefficients
- Can set coefficients exactly to zero
- Automatic feature selection

### Elastic Net

Combines L1 and L2:

$$\min_\beta \left[\sum_{i=1}^{n}(y_i - \hat{y}_i)^2 + \lambda_1\sum_{j=1}^{p}|\beta_j| + \lambda_2\sum_{j=1}^{p}\beta_j^2\right]$$

### Regularization Parameter Selection

**λ effect:**
- λ = 0 → Standard OLS
- λ → ∞ → All coefficients → 0
- Optimal λ → Use cross-validation

### Comparison

| Method | Penalty | Feature Selection | Correlated Features |
|--------|---------|-------------------|---------------------|
| Ridge | L2 | No | Keeps all, shrinks |
| Lasso | L1 | Yes | Picks one arbitrarily |
| Elastic Net | L1 + L2 | Yes | Better handling |

---

## 6. Cross-Validation

### Why Cross-Validate?

- Estimate out-of-sample performance
- Avoid overfitting to validation set
- Select hyperparameters

### K-Fold Cross-Validation

1. Split data into K equal folds
2. For each fold k:
   - Train on all folds except k
   - Test on fold k
3. Average performance across all folds

**CV Error:**
$$CV_{(K)} = \frac{1}{K}\sum_{k=1}^{K}MSE_k$$

### Time Series Cross-Validation

**Important:** Standard CV violates temporal order!

**Walk-Forward Validation:**
```
Fold 1: Train [1-100], Test [101-110]
Fold 2: Train [1-110], Test [111-120]
Fold 3: Train [1-120], Test [121-130]
...
```

**Expanding Window:** Training set grows
**Rolling Window:** Training set size fixed

### Blocked Time Series CV

```
Block 1: Train [1-100], Gap [101-105], Test [106-115]
Block 2: Train [50-150], Gap [151-155], Test [156-165]
...
```

Gap prevents data leakage from sequential correlation.

---

## 7. Feature Engineering

### Why Feature Engineering?

Raw data often not suitable for ML:
- Non-linear relationships
- Different scales
- Missing information

### Common Financial Features

| Feature Type | Examples |
|--------------|----------|
| **Price-based** | Returns, Log returns, Price ratios |
| **Volume-based** | Volume change, VWAP, Volume ratios |
| **Technical** | Moving averages, RSI, MACD, Bollinger Bands |
| **Fundamental** | P/E ratio, Book value, ROE |
| **Calendar** | Day of week, Month, Quarter end |
| **Lag features** | Returns t-1, t-2, t-5, t-20 |

### Feature Scaling

**Standardization (Z-score):**
$$x_{scaled} = \frac{x - \mu}{\sigma}$$

**Min-Max Normalization:**
$$x_{scaled} = \frac{x - x_{min}}{x_{max} - x_{min}}$$

### Moving Averages

**Simple Moving Average:**
$$SMA_t = \frac{1}{n}\sum_{i=0}^{n-1}P_{t-i}$$

**Exponential Moving Average:**
$$EMA_t = \alpha P_t + (1-\alpha)EMA_{t-1}$$

Where $\alpha = \frac{2}{n+1}$

### Technical Indicators

**RSI (Relative Strength Index):**
$$RSI = 100 - \frac{100}{1 + RS}$$

Where $RS = \frac{\text{Avg Gain}}{\text{Avg Loss}}$

**Bollinger Bands:**
- Upper: $SMA + 2\sigma$
- Middle: $SMA$
- Lower: $SMA - 2\sigma$

**MACD:**
$$MACD = EMA_{12} - EMA_{26}$$
$$Signal = EMA_9(MACD)$$

### Lag Features

Create features from past values:

| Feature | Formula |
|---------|---------|
| Return t-1 | $r_{t-1}$ |
| Return t-5 | $r_{t-5}$ |
| Rolling volatility | $\sigma_{[t-20:t]}$ |
| Momentum | $\sum_{i=1}^{20}r_{t-i}$ |

**Warning:** Be careful of look-ahead bias!

---

## Key Formulas Summary

| Concept | Formula |
|---------|---------|
| Sigmoid | $\sigma(z) = \frac{1}{1+e^{-z}}$ |
| Cross-Entropy | $-\frac{1}{n}\sum[y\ln(\hat{p}) + (1-y)\ln(1-\hat{p})]$ |
| Ridge | $\min \sum(y-\hat{y})^2 + \lambda\sum\beta^2$ |
| Lasso | $\min \sum(y-\hat{y})^2 + \lambda\sum|\beta|$ |
| F1 Score | $\frac{2 \times P \times R}{P + R}$ |
| CV Error | $\frac{1}{K}\sum_{k=1}^{K}MSE_k$ |
| Standardization | $\frac{x-\mu}{\sigma}$ |

---

## Practice Problems

1. A logistic model predicts P(up) = 0.65. What are the log-odds?

2. Calculate precision, recall, and F1 given: TP=40, FP=20, TN=30, FN=10

3. Ridge regression with λ=1 on 2 features. Original OLS: β₁=2, β₂=3. What happens to coefficients?

4. You have 1000 days of stock data. Design a walk-forward CV scheme with training=200, test=50.

5. Create a feature matrix with: 5-day return, 20-day volatility, RSI(14), and price/SMA(50) ratio.

---

*Next Week: Portfolio Optimization*
