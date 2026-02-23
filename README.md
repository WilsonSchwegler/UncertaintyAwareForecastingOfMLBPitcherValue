# Uncertainty-Aware Forecasting of MLB Pitcher Value

## Overview

This repository contains code for an **in-progress research project** on uncertainty-aware forecasting of Major League Baseball (MLB) pitcher value. The project models **next-season fWAR** as a **distributional prediction problem**, using **quantile regression** and **conformal calibration** to produce calibrated prediction intervals rather than point estimates alone.

The primary research question is:

> *Does incorporating increasingly detailed pitch-level information improve the quality and sharpness of prediction intervals for next-season pitcher value?*

To study this, the project compares models trained on **nested feature sets**, progressing from season-level statistics to basic pitch-level characteristics.

---

## Related Writing

A blog post describing a case study using this project can be found here:

👉 **https://wilsonschwegler.github.io/blogs/uncertainty-war.html**

---

## Methodology

The modeling pipeline consists of two main components:

### 1. Quantile Regression
- Gradient Boosted Regression Trees (GBRT) are trained to estimate conditional quantiles of next-season fWAR.
- Separate models are fit for lower, median, and upper quantiles (e.g., 5th, 50th, 95th percentiles).
- This allows direct modeling of outcome uncertainty rather than relying on parametric assumptions.

### 2. Conformalized Quantile Regression (CQR)
- Conformal calibration is applied to the predicted quantiles using a held-out calibration set.
- This step guarantees **finite-sample marginal coverage** of the prediction intervals under minimal assumptions.
- The conformal procedure widens the raw quantile intervals only as needed to achieve the target coverage level.

---

## Feature Sets

The project evaluates **nested feature sets** to isolate the impact of additional pitch-level information:

1. **Season-level features**
   - Age, prior WAR, innings pitched, strikeout rate, walk rate, HR/9, games started, etc.

2. **Basic pitch-level features**
   - Mean fastball velocity  
   - Pitch mix entropy  
   - Whiff rate  

This structure allows for controlled comparisons of interval width, coverage, and overall interval quality as information increases.

---

## Evaluation Metrics

Model performance is evaluated using metrics appropriate for **distributional forecasts**, including:

- **Empirical coverage** of prediction intervals  
- **Average interval width**  
- **Winkler score**, which balances interval sharpness and coverage penalties  
- **Median absolute error (MAE)** for point prediction performance  

The focus is placed on interval-aware metrics rather than point accuracy alone.

---

## Key Findings (Preliminary)

Preliminary results suggest that:

- Adding basic pitch-level features leads to **narrower prediction intervals**
- **Winkler scores improve**, indicating higher-quality uncertainty estimates
- **Median prediction error improves modestly**, particularly for starting pitchers
- Gains appear primarily in uncertainty calibration rather than large shifts in point estimates

These findings are exploratory and subject to further validation.

---

**Note:**  
**datasets are not included** in this repository.

---

## Status

🚧 **In Progress**

This project is under active development and is intended to evolve into a more comprehensive research study. Feedback, discussion, and suggestions are welcome.

---

## Contact

If you have questions or would like to discuss this work, feel free to reach out via email or LinkedIn.
