# Public-Utility-Company-Regression-Model
# Revenue Regression Analysis (Hotazel Steam Dataset)

## Overview
This notebook builds and compares two simple linear regression models to forecast monthly revenue for `dt4training`, using a hold-out `dt4testing` set for validation.

## Data
- **Source file:** `AICPA_regressionAnalysisData.csv`
- **Fields:** `type` (training/testing split), `date`, `revenue`, `production`, `coolDD` (cooling degree days), `heatDD` (heating degree days)
- **Training period:** Jan 2011 – Dec 2013 (36 rows)
- **Testing period:** Jan 2014 – Dec 2014 (12 rows)

## Workflow
1. **Import & clean** — Load the CSV with `pandas`, convert `date` to datetime, disable scientific notation for display.
2. **Exploratory analysis** — Plot revenue over time; compute a correlation matrix across `revenue`, `production`, `coolDD`, and `heatDD`.
3. **Train/test split** — Split the data by the `type` column into `dt4training` and `dt4testing`.
4. **Model 1: Revenue ~ Production**
   - Fit with `statsmodels.OLS`
   - Resulting equation: `revenue = 18.99 × production + 4,897,663.26`
   - Applied to the test set, then evaluated with percentage error per row
   - **MAPE ≈ 25.4%**
5. **Model 2: Revenue ~ heatDD**
   - Fit with `statsmodels.OLS`
   - Resulting equation: `revenue = 9,991.26 × heatDD + 10,333,861.28`
   - Applied to the test set, then evaluated the same way
   - **MAPE ≈ 21.6%**
6. **Visualization** — Line plots comparing actual vs. predicted revenue for each model over the testing period.

## Results Summary
| Model | Predictor | MAPE |
|---|---|---|
| Model 1 | `production` | ~25.4% |
| Model 2 | `heatDD` | ~21.6% |

Model 2 (heatDD) produced a lower mean absolute percentage error than Model 1 (production) on the 2014 testing data, suggesting heating degree days was the somewhat stronger single-variable predictor of revenue in this dataset.

## Notes
- Both models are simple (single-predictor) OLS regressions; no multivariate model was built in this notebook.
- MAPE values are taken directly from the notebook output — you may want to double-check these against your final submitted version in case any cells were re-run with different data.
