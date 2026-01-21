# Capstone Option 3: Alternative Data NLP Alpha Research

## Project Overview

Build an alpha research platform using NLP on financial text data (earnings calls, news, SEC filings) to demonstrate ability to extract signals from alternative data.

## Target Metrics

| Metric | Target |
|--------|--------|
| Alpha | > 3% annual (risk-adjusted) |
| IC | > 0.03 (Information Coefficient) |
| Fama-French Correlation | < 0.20 |
| Signal Decay | > 5 days half-life |

## Data Sources

- **Earnings Calls:** Transcripts from public sources
- **SEC Filings:** 8-K, 10-K via EDGAR
- **News:** Financial news headlines

## Algorithm Stack

### Text Processing
| Method | Purpose |
|--------|---------|
| Tokenization | Text preprocessing |
| NER | Entity extraction |
| TF-IDF | Baseline features |

### Sentiment Models
| Model | Purpose |
|-------|---------|
| FinBERT | Financial sentiment |
| Custom BERT | Domain fine-tuning |
| Ensemble | Combining signals |

### Alpha Generation
- Sentiment-based long/short
- Event-driven signals
- Combination with price factors

## Project Structure

```
Option_3_Alternative_Data_NLP_Alpha_Research/
├── Project_Proposal.md
├── Literature_Review.md
├── Data/
│   ├── earnings_calls/
│   ├── sec_filings/
│   └── news/
├── Notebooks/
│   ├── 01_Text_Data_Collection.ipynb
│   ├── 02_Preprocessing_EDA.ipynb
│   ├── 03_FinBERT_Sentiment.ipynb
│   ├── 04_Signal_Construction.ipynb
│   ├── 05_Backtesting.ipynb
│   └── 06_Factor_Attribution.ipynb
├── src/
│   ├── data_collection/
│   ├── preprocessing/
│   ├── sentiment/
│   └── signals/
├── tests/
├── docs/
├── Final_Report.md
└── Presentation.pdf
```

## Deliverables Checklist

- [ ] Text data pipeline (earnings, news, filings)
- [ ] NLP feature extraction
- [ ] FinBERT sentiment model
- [ ] Alpha signal construction
- [ ] Backtested long-short strategy
- [ ] Factor attribution analysis
- [ ] Real-time processing architecture design
- [ ] Complete documentation
- [ ] 20-minute presentation
