# Interview Preparation Section

This folder contains comprehensive interview preparation materials for top quant firms.

## Structure

```
04_Interview_Preparation/
├── README.md                    ← You are here
├── Company_Specific/
│   ├── Jane_Street/
│   ├── Goldman_Sachs/
│   ├── JPMorgan/
│   ├── Citadel/
│   ├── Two_Sigma/
│   ├── DE_Shaw/
│   ├── HRT/
│   ├── Jump_Trading/
│   └── Tower_Research/
├── Topic_Based/
│   ├── Probability_Expected_Value/
│   ├── Statistics_Hypothesis_Testing/
│   ├── Linear_Algebra_Matrix_Ops/
│   ├── ML_Algorithms_Fundamentals/
│   ├── Time_Series_and_Stochastic_Calculus/
│   ├── Portfolio_Theory_Optimization/
│   ├── Options_Derivatives_Greeks/
│   ├── Market_Microstructure/
│   ├── Model_Validation_and_Overfitting/
│   ├── Production_Systems_and_Latency/
│   └── Coding_DSA_Patterns/
├── Daily_Questions/
│   ├── Week_01_Questions.md
│   └── ... [through Week_24]
└── Mock_Interviews/
    ├── Week_13_Full_Mock_Quant_Researcher.md
    ├── Week_14_Full_Mock_Quant_Trader.md
    ├── Week_15_Full_Mock_ML_Engineer.md
    └── Week_16_Full_Mock_Systematic_Trader.md
```

## Interview Timeline

| Weeks | Intensity | Daily Questions | Weekend Focus |
|-------|-----------|-----------------|---------------|
| 1-4 | Low | 1-2 basic | Concept review |
| 5-8 | Medium | 2-3 intermediate | Algorithm practice |
| 9-12 | Medium-High | 3-4 challenging | Timed exercises |
| **13-16** | **INTENSIVE** | **5+ company-specific** | **Full mock interviews** |
| 17-20 | High | 3-4 advanced | Project explanations |
| 21-24 | Medium | 2-3 system design | Capstone practice |

## Company-Specific Strategy

### Jane Street

**Focus Areas:**
- Probability puzzles (mental math, expected value)
- Bayesian inference and updating
- Thompson Sampling and multi-armed bandits
- Kelly criterion and optimal betting
- Trading games and market making
- Think-aloud problem solving

**Interview Style:**
- Collaborative, conversational
- Focus on thought process over final answer
- May involve real-time trading simulations
- Heavy emphasis on probability intuition

**Sample Questions:**
1. You roll two dice. What's the expected value of the higher die?
2. A stock has 60% chance of going up 10%, 40% chance of going down 5%. What fraction should you bet?
3. Design a market making strategy. How do you set bid-ask spread?

---

### Goldman Sachs

**Focus Areas:**
- Quantitative strategies (mean reversion, momentum, stat arb)
- Risk management (VaR, stress testing, Greeks)
- Portfolio optimization
- P&L attribution
- Market knowledge across asset classes

**Interview Style:**
- More formal, structured
- Technical + behavioral rounds
- Division-specific questions (Strats, QR, Trading)
- Focus on practical implementation

**Sample Questions:**
1. Explain how you would implement a pairs trading strategy
2. Calculate the VaR of a portfolio with correlation assumptions
3. How would you stress test a portfolio for a 2008-style event?

---

### Citadel / Two Sigma

**Focus Areas:**
- Large-scale ML systems
- Data engineering and pipelines
- Distributed computing
- Model monitoring and debugging
- Latency optimization
- Feature engineering at scale

**Interview Style:**
- Technical depth on ML and systems
- Coding challenges (algorithm heavy)
- System design questions
- Focus on scalability and production

**Sample Questions:**
1. Design a feature store for a quant research platform
2. How do you detect and handle concept drift in production?
3. Optimize this pandas code to handle 10TB of tick data

---

### HRT / Jump / Tower

**Focus Areas:**
- Market microstructure
- Low-latency systems
- Order book dynamics
- Execution optimization
- Hardware considerations (FPGA, networking)

**Interview Style:**
- Highly technical on systems
- Speed and latency focused
- May include C++ questions
- Focus on understanding market mechanics

**Sample Questions:**
1. What's the difference between maker and taker strategies?
2. How do you minimize latency in a trading system?
3. Explain order book imbalance and how to use it as a signal

---

## Topic-Based Preparation

### Probability & Expected Value (Jane Street favorite)

| Question Type | Example | Time Limit |
|--------------|---------|------------|
| Dice/Cards | Expected value of max of two dice | 5 min |
| Betting | Kelly criterion application | 10 min |
| Bayesian | Update probability given new information | 10 min |
| Games | Optimal strategy in trading game | 15 min |

### ML Algorithms (All firms)

| Topic | Must Know | Nice to Know |
|-------|-----------|--------------|
| Linear Models | OLS derivation, Ridge vs Lasso | Elastic Net path |
| Trees | Gini vs entropy, bagging vs boosting | SHAP math |
| Neural Nets | Backprop, vanishing gradients | Attention mechanism |
| Time Series | ARIMA, GARCH | State space models |

### Overfitting Prevention (Critical topic)

**10+ techniques you must articulate:**
1. Train/validation/test split
2. Cross-validation (k-fold, purged, CPCV)
3. Regularization (L1, L2, dropout)
4. Early stopping
5. Feature selection
6. Ensemble methods
7. Walk-forward validation
8. Out-of-sample testing
9. Multiple testing correction (deflated Sharpe)
10. Embargo periods
11. Backtesting with realistic costs
12. Paper trading / shadow mode

---

## Mock Interview Structure

### Full Mock (3 hours)

**Round 1: Technical Screen (45 min)**
- 2-3 probability/math questions
- 1 coding question (live)
- ML algorithm deep-dive

**Round 2: Quantitative Finance (45 min)**
- Portfolio theory
- Options/derivatives
- Risk management
- Market structure

**Round 3: ML/Coding (60 min)**
- Algorithm implementation
- System design
- Code review

**Round 4: Project Discussion (30 min)**
- Walk through a project
- Technical deep-dive
- Extensions and improvements

---

## Daily Question Format

Each daily question file includes:

```markdown
## Question 1: [Title]

**Company**: Jane Street / Citadel / etc.
**Difficulty**: Easy / Medium / Hard
**Time Limit**: X minutes
**Type**: Probability / ML / Coding / etc.

### Problem Statement
[Clear problem description]

### Hints (reveal after attempting)
<details>
<summary>Hint 1</summary>
[First hint]
</details>

### Solution
<details>
<summary>Show Solution</summary>
[Complete solution with explanation]
</details>

### Follow-up Questions
1. [Extension 1]
2. [Extension 2]

### Interview Tips
- What interviewers look for
- Common mistakes
- How to communicate your thinking
```

---

## Preparation Checklist

### Before Interviews (2-4 weeks out)
- [ ] Complete at least 200 practice questions
- [ ] Do 2-4 full mock interviews
- [ ] Prepare 3-5 minute project walkthrough
- [ ] Research specific company (recent news, strategies, culture)
- [ ] Prepare questions to ask interviewers

### Day Before
- [ ] Review key formulas and concepts
- [ ] Get good sleep
- [ ] Prepare quiet environment (if virtual)
- [ ] Test technology (camera, mic, internet)

### During Interview
- [ ] Think aloud
- [ ] Ask clarifying questions
- [ ] Start with simple approach, then optimize
- [ ] Discuss trade-offs
- [ ] Be honest about what you don't know

---

## Resources

### Books
- *Heard on the Street* - Timothy Crack
- *A Practical Guide to Quantitative Finance Interviews* - Xinfeng Zhou
- *Quant Job Interview Questions and Answers* - Mark Joshi

### Online
- Glassdoor interview reviews
- Blind (company-specific discussions)
- QuantNet forums
- LeetCode (for coding)

### Practice Platforms
- LeetCode (algorithms)
- BrainStellar (probability puzzles)
- QuantGuide (quant-specific)
