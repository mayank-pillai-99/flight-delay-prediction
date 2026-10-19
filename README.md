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
| `report/main.tex`, `report/main.pdf` | Project report in IEEE format (`references.bib` holds the references) |
| `requirements.txt` | Python packages |

## Method (short)

1. **Clean:** drop cancelled/diverted flights; target = arrival delay ≥ 15 min (24.5% of flights).
2. **No leakage:** remove everything only known after departure (actual times, delays, air time).
3. **Features:** day of week, weekend, scheduled departure/arrival hour, distance, carrier, origin, destination,
   scheduled flights per airport per hour/day, and the carrier/origin/destination delay rate over the previous 7 days.
4. **Split by date:** train Jan–Aug, validation Sep–Oct, test Nov–Dec.
5. **Models:** Logistic Regression and XGBoost (tuned with expanding-window time-series validation).
6. **Calibration:** isotonic regression fitted on the validation set.

## Results (test set, Nov–Dec 2013)

| Model | PR AUC | ROC AUC | Recall @ precision 0.5 | Brier (raw → calibrated) |
|-------|--------|---------|------------------------|--------------------------|
| Random guess | 0.258 | 0.500 | – | – |
| Logistic Regression | 0.367 | 0.646 | 0.021 | 0.232 → 0.187 |
| **XGBoost** | **0.384** | **0.648** | **0.106** | 0.225 → 0.188 |

The scheduled departure hour and the carrier's recent delay rate are the most important features.

## Team

| Member | Contribution |
|--------|--------------|
| Member 1 | Data loading and EDA |
| Member 2 | Leakage removal and feature engineering |
| Member 3 | Logistic Regression |
| Member 4 | XGBoost |
| Member 5 | Evaluation, literature review, README |
