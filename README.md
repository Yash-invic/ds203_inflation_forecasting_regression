# DS203 Project: Forecasting U.S. Inflation

> 🎥 **Project video:** _(add video link or embed here)_

## Introduction

Inflation is affected by many things, like jobs, interest rates, production, oil prices and how people feel about the economy. In this project we use monthly U.S. data from FRED to predict inflation **1, 3, 6 and 12 months ahead**, using regression models from class.

## What we do

1. Load 11 FRED series and make them monthly.
2. Pick the common time period and build the features and targets. Inflation is the year-over-year change in CPI.
3. Explore the data (inflation over time, distributions, correlations, lead-lag).
4. Split the data by time into train, validation and test (no shuffling).
5. Train Linear Regression, Ridge and Lasso for each horizon. Tune on the validation set and score once on the test set with MAE, RMSE and R². A simple baseline (train mean) is used for comparison.
6. Find which features matter most (coefficients and a run without current inflation).

## Key formulas and metrics

We measure inflation as the year-over-year change in the CPI, in percent. It compares the CPI of a month with the CPI of the same month one year earlier:

```
inflation(t) = 100 * (CPI(t) / CPI(t-12) - 1)
```

For each month t, the target is the inflation n months later, where n is 1, 3, 6 or 12. So the model sees the data of month t and has to predict inflation at month t+n.

Some series (like industrial production, payrolls, producer prices, oil and M2) keep going up over time, so we use their year-over-year growth instead of the raw values:

We check each model on the test set with three numbers:
* **MAE:** the average size of the error, in percentage points of inflation.
* **RMSE:** similar to MAE, but big mistakes are punished more.
* **R²:** how much of the ups and downs of inflation the model explains. 1 is perfect, and 0 or below means it is no better than guessing the average.

To see if the models are actually useful, we compare them with a very simple forecast:
* **Train mean:** always predict the average inflation of the training period.

## Data

We use these series from [FRED](https://fred.stlouisfed.org/): `T10Y2Y`, `UNRATE`, `INDPRO`, `FEDFUNDS`, `PAYEMS`, `PPIACO`, `HOUST`, `DCOILWTICO`, `M2SL`, `UMCSENT` and `CPIAUCSL` (used to calculate inflation).

## How to run

1. Install the libraries:
   ```
   pip install numpy pandas matplotlib scikit-learn
   ```
2. Put the 11 CSV files in the same folder as the notebook.
3. Open `DS203_Project.ipynb` and click **Run all**. On Colab, upload the CSV files first.

## Group members

1. Raunak Roy, 25B2254
2. Fulsundar Yash Shrikant, 25B2165
3. Dhruv Deorah, 25B2275
