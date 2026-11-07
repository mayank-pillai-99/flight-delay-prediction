# Flight Delay Prediction (Project 21)

Predict whether a flight will **arrive 15 or more minutes late**, using only information that is known
**before the flight departs** (schedule, carrier, route, airport congestion and past delay history).

**Dataset:** the Kaggle "Flights 2013" dataset ([nycflights13](https://github.com/tidyverse/nycflights13)):
all ~336k flights that departed from New York City airports (JFK, LGA, EWR) in 2013.

## Project phases

| Phase | Folder | Content | Status |
|-------|--------|---------|--------|
| **Phase 1: Machine Learning** | [`phase1/`](phase1) | EDA, feature engineering, Logistic Regression and XGBoost, report, presentation | ✅ Complete |
| **Phase 2: Deep Learning** | [`phase2/`](phase2) | Neural network with learned embeddings, compared with the Phase 1 models | 🚧 In progress |

Each folder has its own README with setup steps, method and results.

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
└── .gitignore
```

## Team

- Asad Ali
- Divyansh Bhartia
- [Vikrant Yadav](https://github.com/vikgenix)
- Mayank Pillai
- Prashant Raj
