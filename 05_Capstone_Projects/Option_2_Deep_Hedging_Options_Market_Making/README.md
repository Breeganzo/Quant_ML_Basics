# Capstone Option 2: Deep Hedging & Options Market Making

## Project Overview

Build an options pricing and market making system using traditional methods (Black-Scholes) and deep hedging neural networks to demonstrate understanding of derivatives and risk management.

## Target Metrics

| Metric | Target |
|--------|--------|
| P&L Stability | Low variance |
| Hedging Cost | Lower than BS delta hedging |
| Risk Exposure | Delta-neutral at end of day |

## Instruments

- **Underlying:** SPY ETF
- **Options:** Calls and puts across strikes and expirations
- **Data:** Historical options data (OptionMetrics or simulated)

## Algorithm Stack

### Pricing Models
| Model | Purpose |
|-------|---------|
| Black-Scholes | Baseline pricing |
| Binomial Tree | American options |
| SABR/SVI | Vol surface calibration |

### Deep Hedging
- Neural network for optimal hedge ratios
- Reinforcement learning formulation
- Transaction cost aware

### Market Making
- Avellaneda-Stoikov framework
- Inventory management
- Spread optimization

## Project Structure

```
Option_2_Deep_Hedging_Options_Market_Making/
├── Project_Proposal.md
├── Literature_Review.md
├── Data/
├── Notebooks/
│   ├── 01_Black_Scholes_Implementation.ipynb
│   ├── 02_Greeks_Calculation.ipynb
│   ├── 03_Vol_Surface_Modeling.ipynb
│   ├── 04_Deep_Hedging_NN.ipynb
│   ├── 05_Market_Making_Simulation.ipynb
│   └── 06_Risk_Analysis.ipynb
├── src/
│   ├── pricing/
│   ├── hedging/
│   ├── market_making/
│   └── risk/
├── tests/
├── docs/
├── Final_Report.md
└── Presentation.pdf
```

## Deliverables Checklist

- [ ] Black-Scholes implementation with Greeks
- [ ] Volatility surface calibration
- [ ] Deep hedging neural network
- [ ] Comparison: NN vs traditional hedging
- [ ] Market making simulation
- [ ] P&L analysis and risk metrics
- [ ] Complete documentation
- [ ] 20-minute presentation
