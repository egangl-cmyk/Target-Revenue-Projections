# Target-Revenue-Projections
# Target Corporation Quarterly Revenue Forecasting

A time-series regression analysis of Target Corp (TGT) quarterly sales from 2001–2024, demonstrating how seasonal dummy variables improve revenue forecasting accuracy.

## Overview

This notebook forecasts Target's quarterly revenue using OLS regression. It compares a baseline trend model against an enhanced model that accounts for Target's seasonal revenue patterns — specifically the holiday quarter (FQ4) and the back-to-school/summer quarter (FQ2).

## Data

**Source:** `qSales_2024.csv` — quarterly financial data sourced from Compustat, covering multiple companies (Apple, Target, Nintendo, and others) from 2001 to 2024.

**Target subset:** 93 quarters of Target Corp data (ticker: TGT), including quarterly revenue (`saleq`) and fiscal quarter identifiers.

## Methods

### 1. Baseline OLS Model
A simple linear regression of revenue on a sequential time variable:

```
Revenue = β₀ + β₁ × time
```

Estimated coefficients: intercept = 10,503.75, slope = 139.30 (i.e., ~$139M revenue growth per quarter on average).

### 2. Seasonal Dummy Model
An extended OLS model that adds dummy variables and interaction terms to capture quarterly seasonality:

```
Revenue = 9400.42 + 136.09×time + 4077.03×summer_dv + 14.33×summer_dinteraction + 210.90×winter_dv − 3.59×winter_dinteraction
```

- `summer_dv` — flags FQ4 (holiday quarter, Target's highest-revenue period)
- `winter_dv` — flags FQ2 (back-to-school quarter, second-highest revenue period)
- Interaction terms (`time × dummy`) allow the seasonal premium to shift over time

### Train/Test Split
Data is split 75/25 chronologically — the first 69 quarters for training, the final 24 quarters (2018–2024) for out-of-sample evaluation.

## Results

The baseline model achieved a mean absolute percentage error of ~14% on the test set. The seasonal dummy model visually tracks Target's quarterly revenue swings much more closely, with 80% prediction intervals reported for each quarter.

## Repository Structure

```
.
├── AFM244- July 24 Quiz.ipynb   # Main analysis notebook
└── qSales_2024.csv              # Input data (Compustat quarterly sales)
```

## Requirements

```
pandas
numpy
matplotlib
statsmodels
```

Install with:
```bash
pip install pandas numpy matplotlib statsmodels
```

## Usage

1. Place `qSales_2024.csv` in the same directory as the notebook.
2. Run all cells in order.
3. The notebook outputs:
   - A time-series plot of Target's quarterly revenue (2001–2024)
   - OLS model summaries and coefficient estimates
   - An actual vs. predicted revenue chart for the test period
   - 80% prediction intervals for the seasonal dummy model

## Key Concepts Demonstrated

- Time-series regression with a linear trend
- Dummy variable encoding for seasonality
- Interaction terms to model time-varying seasonal effects
- Train/test splitting for out-of-sample model evaluation
- Prediction intervals using `statsmodels` `get_prediction()`
