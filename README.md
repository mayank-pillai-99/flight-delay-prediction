# Flight Delay Prediction (Project 21)

Predict whether a flight will **arrive 15 or more minutes late**, using only information that is known
**before the flight departs** (schedule, carrier, route, airport congestion and past delay history).

**Dataset:** the Kaggle "Flights 2013" dataset ([nycflights13](https://github.com/tidyverse/nycflights13)):
all ~336k flights that departed from New York City airports (JFK, LGA, EWR) in 2013.

## Project phases

| Phase | Folder | Content | Status |
|-------|--------|---------|--------|
| **Phase 1: Machine Learning** | [`phase1/`](phase1) | EDA, feature engineering, Logistic Regression and XGBoost, report, presentation | ✅ Complete |
| **Phase 2: Deep Learning** | [`phase2/`](phase2) | MLP with learned embeddings, ablation study, calibration, what-if rescheduling, report, presentation | ✅ Complete |

Each folder has its own README with setup steps, method and results.

| Test PR AUC (Nov–Dec 2013) | Random | Logistic Regression | XGBoost | MLP (Phase 2) |
|---|---|---|---|---|
| | 0.258 | 0.376 | **0.391** | 0.386 |

## Repository structure

```
.
├── phase1/            Phase 1 (Machine Learning)
│   ├── flight_delay_prediction.ipynb
│   ├── figures/
│   ├── report/
│   ├── presentation/
│   └── requirements.txt
├── phase2/            Phase 2 (Deep Learning)
│   ├── flight_delay_dl.ipynb
│   ├── figures/
│   ├── report/
│   ├── presentation/
│   └── requirements.txt
└── .gitignore
```

## Team

- Asad Ali
- Divyansh Bhartia
- [Vikrant Yadav](https://github.com/vikgenix)
- Mayank Pillai
- Prashant Raj
