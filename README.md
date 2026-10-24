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

### Prerequisites
- Python 3.9 to 3.11 recommended.

### Setup and Execution
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
jupyter notebook flight_delay_prediction.ipynb
```

Then run all cells (Kernel → Restart & Run All).


## Repository structure

| File | Description |
|------|-------------|
| `flight_delay_prediction.ipynb` | All code: data loading, EDA, features, models, evaluation |
| `figures/` | Plots saved by the notebook (used in the report) |
| `report/main.tex`, `report/main.pdf` | Project report in IEEE format |
| `requirements.txt` | Python packages |

## Method (short)

1. **Clean:** drop cancelled/diverted flights; target = arrival delay ≥ 15 min (24.5% of flights).
2. **No leakage:** remove everything only known after departure (actual times, delays, air time).
3. **Features:** weekend flag, day of week and scheduled departure/arrival hour (cyclic sin/cos encoding), distance,
   carrier, origin, destination,
   scheduled flights per airport per hour/day (counted on the full schedule, including later-cancelled flights),
   and the carrier/origin/destination/route delay rate over the previous 7 calendar days.
4. **Split by date:** train Jan–Aug, validation Sep–Oct, test Nov–Dec.
5. **Models:** Logistic Regression and XGBoost (tuned with expanding-window time-series validation).
6. **Calibration:** isotonic regression fitted on the validation set.

## Results (test set, Nov–Dec 2013)

| Model | PR AUC | ROC AUC | Recall @ precision 0.5 | Brier (raw → calibrated) |
|-------|--------|---------|------------------------|--------------------------|
| Random guess | 0.258 | 0.500 | – | – |
| Logistic Regression | 0.376 | 0.645 | 0.059 | 0.228 → 0.190 |
| **XGBoost** | **0.391** | **0.656** | **0.111** | 0.219 → 0.188 |

The scheduled departure hour and the carrier's recent delay rate are the most important features.

## Team

| Member | Contribution |
|--------|--------------|
| Asad Ali | Data loading and EDA |
| Divyansh Bhartia | Leakage removal and feature engineering |
| Vikrant Yadav | Logistic Regression |
| Mayank Pillai | XGBoost |
| Prashant Raj | Evaluation, literature review, README |
