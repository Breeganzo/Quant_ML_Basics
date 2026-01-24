# Week 1 Project: Market Data Pipeline with Quality Checks

## 🎯 Project Overview

Build a production-ready market data pipeline that downloads, validates, and stores financial data with comprehensive quality checks.

## 📊 Business Problem

Hedge funds lose millions annually due to bad data. This project implements:
- Automated data download from multiple sources
- Data quality validation (missing values, outliers, corporate actions)
- Clean data storage with versioning

## 🔧 Technologies Used

- **Data Sources**: yfinance, pandas-datareader
- **Storage**: Parquet files with date partitioning
- **Validation**: Statistical tests, business rule checks
- **Visualization**: Matplotlib, Plotly

## 📁 Project Structure

```
Week_01_Market_Data_Pipeline/
├── README.md
├── requirements.txt
├── data_pipeline.ipynb       # Main notebook with full implementation
├── src/
│   ├── __init__.py
│   ├── downloaders.py        # Data download functions
│   ├── validators.py         # Quality check functions
│   └── storage.py            # Data storage utilities
└── tests/
    └── test_validators.py
```

## 🚀 Quick Start

```bash
pip install -r requirements.txt
jupyter notebook data_pipeline.ipynb
```

## 📈 Key Features

1. **Multi-Source Download**: yfinance with fallback to alternative sources
2. **Quality Checks**:
   - Missing value detection and imputation
   - Outlier detection using IQR and Z-scores
   - Volume spike detection
   - Price jump validation (corporate actions)
3. **Data Storage**: Parquet format with compression
4. **Logging**: Comprehensive logging for debugging

## 🎓 Skills Demonstrated

- Python data engineering
- Financial data handling
- Quality assurance processes
- Production-ready code structure
