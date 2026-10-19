# Flight Delay Prediction (Project 21) — Phase 1: Machine Learning

Predict whether a flight will **arrive 15 or more minutes late**, using only information that is known
**before the flight departs** (schedule, carrier, route, airport congestion and past delay history).

Phase 1 covers the Machine Learning part: data quality checks, EDA, feature engineering,
Logistic Regression and XGBoost models, and their evaluation.

## Dataset

The Kaggle "Flights 2013" dataset, which is the [nycflights13](https://github.com/tidyverse/nycflights13) data: all ~336k flights that departed
from New York City airports (JFK, LGA, EWR) in 2013. It is loaded directly with the `nycflights13`
Python package, so no manual download is needed.

## How to run

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter notebook flight_delay_prediction.ipynb
```

Then run all cells (Kernel → Restart & Run All).

## Repository structure

| File | Description |
|------|-------------|
| `flight_delay_prediction.ipynb` | All code: data loading, EDA, features, models, evaluation |
| `figures/` | Plots saved by the notebook (used in the report) |
| `report/main.tex` | Project report in IEEE format |
| `requirements.txt` | Python packages |

## Team

| Member | Contribution |
|--------|--------------|
| Member 1 | Data loading and EDA |
| Member 2 | Leakage removal and feature engineering |
| Member 3 | Logistic Regression |
| Member 4 | XGBoost |
| Member 5 | Evaluation, literature review, README |
