<picture><source media="(prefers-color-scheme: dark)" srcset="assets/banner-dark.png"><img alt="TARDIS — Forecasting French long-distance train delays per route and month, with an interactive dashboard." src="assets/banner-light.png"></picture>

**Epitech Bachelor · Year 1 · Data module (B-DAT-200) · Feb 2026**
Source code is private under Epitech's academic policy. Happy to walk you through it or demo the dashboard → **imran.nogueira@gmail.com**

## Overview

Using SNCF monthly statistics for TGV and Intercités routes (7,648 rows after cleaning), TARDIS estimates the average arrival delay for a given route and month, and shows the estimate next to the route's history in a dashboard anyone can query.

## Stack

| Layer | Tech |
|---|---|
| Data | Python, pandas, NumPy, matplotlib, seaborn, Jupyter |
| Model | scikit-learn RandomForestRegressor (500 trees), 5-fold cross-validation, joblib |
| Dashboard | Streamlit |

## Pipeline

1. **Cleaning** — encoding issues, type conversion, invalid and negative values removed, outliers above 60 minutes filtered.
2. **Exploration** — delay distributions, most delayed stations, monthly trends, trip duration vs delay.
3. **Feature engineering** — cancellation rate, share of late trains, per-station historical delay, route complexity, one-hot encoded routes.
4. **Model** — RandomForestRegressor, evaluated on a held-out test set and with 5-fold cross-validation.
5. **Dashboard** — pick a route and a month, get the estimated delay with its historical context.

## Results

| | RMSE (min) | MAE (min) | R² |
|---|---|---|---|
| Baseline (always predict the mean) | 4.85 | — | 0.00 |
| Random Forest | 3.48 | 1.67 | 0.48 |

5-fold cross-validation: R² 0.47 ± 0.21.

## What I'd do differently

Some features are computed from the same month's outcomes (share of trains late at arrival) or from the target over the whole dataset (historical delay per arrival station, computed before the train/test split). That makes the model closer to *explaining* a month than *forecasting* it, and the per-station average leaks a little of the test set. Next time: compute historical features on past months only, and split by time instead of at random.

## Contact

Walkthrough or dashboard demo on request → **imran.nogueira@gmail.com** · [Portfolio](https://imran-nogueira.github.io)
