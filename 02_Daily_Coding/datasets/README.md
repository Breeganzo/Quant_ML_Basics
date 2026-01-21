# Datasets README

## Data Sources

### Primary Sources

| Source | Data Type | Cost | API |
|--------|-----------|------|-----|
| yfinance | Stock prices, indices | Free | Yes |
| FRED | Macroeconomic | Free | Yes |
| Quandl | Alternative data | Free tier | Yes |
| SEC EDGAR | Filings, 8-K, 10-K | Free | Yes |

### Data Quality Principles

1. **Point-in-time**: Only use data available at decision time
2. **Survivorship bias**: Include delisted stocks when possible
3. **Corporate actions**: Adjust for splits, dividends
4. **Missing data**: Document and handle appropriately

---

## Download Instructions

### Setup Environment
```bash
pip install yfinance pandas-datareader fredapi
```

### Quick Start
```python
# Run download script
python download_data.py

# Verify data quality
python data_quality_checks.py
```

---

## Data Files

After running download scripts:

```
datasets/
├── prices/
│   ├── sp500_daily.parquet
│   ├── etf_daily.parquet
│   └── fx_daily.parquet
├── fundamentals/
│   ├── quarterly_financials.parquet
│   └── earnings_dates.parquet
├── macro/
│   ├── fed_rates.parquet
│   ├── treasury_yields.parquet
│   └── economic_indicators.parquet
└── metadata/
    ├── sp500_constituents.csv
    └── ticker_mapping.csv
```

---

## Usage in Notebooks

```python
import pandas as pd
from pathlib import Path

DATA_DIR = Path("../datasets")

# Load price data
prices = pd.read_parquet(DATA_DIR / "prices/sp500_daily.parquet")

# Ensure point-in-time
as_of_date = "2020-01-15"
available_data = prices[prices.index <= as_of_date]
```

---

## Data Quality Checks

The `data_quality_checks.py` script verifies:
- [ ] No future data leakage
- [ ] Proper date alignment
- [ ] Missing value handling
- [ ] Split/dividend adjustments
- [ ] Ticker consistency
