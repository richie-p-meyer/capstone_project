# NHL Totals Betting — MoneyPuck-Based Predictive Modeling

## Overview

This project develops an end-to-end data science pipeline to model **NHL game total goals** with the explicit goal of supporting **real-money sports bettors** who wager on **over/under (totals) markets**.

Using publicly available **MoneyPuck advanced statistics**, the project builds a fully reproducible workflow covering:

- data acquisition  
- feature engineering  
- exploratory data analysis  
- supervised modeling  
- unsupervised team-style clustering  
- model diagnostics and validation  
- production-ready visualization outputs  

The emphasis throughout is **pre-game information only**, avoiding data leakage and maintaining realism for betting applications.

---

## Stakeholder

**Primary stakeholder:**  
Sports bettors attempting to **profitably model NHL totals markets** using data-driven approaches rather than heuristics.

Design decisions prioritize:

- interpretability  
- stability across seasons  
- realistic generalization  
- alignment with real-world betting constraints  

---

## Data Source

- **MoneyPuck** — NHL team-level advanced statistics  
  https://moneypuck.com  

> Betting odds were explored via an API during development but are **not included in the final modeling dataset** to maintain focus on totals prediction using hockey performance signals alone.

---

## Dataset Summary

- **Unit of observation:** One NHL game  
- **Rows:** ~22,000 games  
- **Columns:** 448 features  
- **Target variable:** `total_goals` (home goals + away goals)  

The dataset includes:

- raw team game statistics  
- rolling averages (3 / 7 / 15 / 30 games)  
- exponentially weighted moving averages (fast & slow)  
- momentum / trend features  
- strength-of-schedule proxies  
- home–away differential features  

---

## Feature Engineering Highlights

All engineered features are **lagged or rolling** to avoid look-ahead bias.

Key feature families include:

- scoring & defensive leakage  
- shot volume and pace proxies  
- expected-goals quality measures  
- possession and share metrics (xG%, Corsi%, Fenwick%)  
- short-term vs long-term momentum  
- matchup differentials (home − away)  

---

## Exploratory Data Analysis

EDA focuses on understanding:

- the distribution of total goals  
- long-term league scoring trends  
- relationships between total goals and expected-goals environments  
- volatility and variance drivers relevant to totals markets  

All EDA figures are automatically generated and saved to `/figures`.

---

## Modeling Approach

### Supervised Models

- **Linear Regression** (final model)  
- **XGBoost Regressor** (tuned, benchmark comparison)  

Models are trained using:

- chronological train/test splits  
- time-series cross-validation  
- strict leakage controls  

The **linear regression model** is selected as the final model due to:

- strong generalization  
- minimal overfitting  
- stable performance across seasons  
- superior interpretability for betting contexts  

### Diagnostics

- MAE, RMSE, R²  
- train/test generalization gaps  
- Durbin–Watson test  
- Breusch–Pagan test  
- residual plots and QQ plots  

---

## Unsupervised Learning

A **K-Means clustering model (k = 2)** is used to segment teams into persistent **style archetypes** based on rolling performance metrics.

This identifies:

- high-event teams  
- low-event teams  

providing contextual insight into scoring environments that are not captured by single coefficients.

Dimensionality reduction and interpretation are supported via:

- silhouette analysis  
- PCA visualization  
- cluster-mean heatmaps  

---

## Reproducibility

All results can be reproduced by running the notebook:


The notebook:

- downloads data (MoneyPuck)  
- cleans and engineers features  
- runs EDA  
- fits supervised and unsupervised models  
- saves all figures to disk  

---

## Key Takeaways

- NHL total goals exhibit strong temporal structure and moderate variance.  
- Expected-goals environments explain part, but not all, scoring variability.  
- Simple, well-regularized models generalize better than complex models in this setting.  
- Team style segmentation provides useful contextual structure for totals betting.  

---

## Limitations & Next Steps

- Betting odds are not directly modeled in this version.  
- No explicit market-edge or ROI backtesting is performed here.  
- Future extensions could integrate:
  - bookmaker lines  
  - closing-line comparisons  
  - calibration to implied probabilities  
  - bankroll-aware evaluation metrics  

---

## References

MoneyPuck. (2024). *NHL advanced statistics and expected goals data*.  
https://moneypuck.com  

Hockey-Reference. (2024). *National Hockey League historical statistics*.  
https://www.hockey-reference.com  

---

## Author

**Richard Wilders**  
M.S. Data Science — Capstone Project




