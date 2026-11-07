# Flight Delay Prediction (Project 21) — Phase 2: Deep Learning

> **Status:** in progress. This folder will hold all Phase 2 work.

Phase 2 adds a **deep learning model** to the same problem as Phase 1: predict whether a flight will
**arrive 15 or more minutes late**, using only information known **before departure**.

## Plan

1. **DL model:** a compact MLP (neural network) with **learned embeddings** for carrier, origin and destination,
   as required by the Project 21 brief. A temporal model (e.g. a small GRU over recent flight history) is optional.
2. **Fair comparison:** same data, same leakage rules, same date split (train Jan–Aug, validation Sep–Oct,
   test Nov–Dec) and same metrics (PR AUC, ROC AUC, recall at precision 0.5, Brier score) as Phase 1, so the
   results can be compared directly with Logistic Regression and XGBoost from [`../phase1`](../phase1).
3. **Calibration:** temperature scaling or isotonic regression on the validation set.
4. **Ablation studies:** e.g. with vs without embeddings, history features or regularisation.
5. **Hybrid approach (optional, extra marks):** only if it is technically justified and actually improves results.

## What Phase 2 is evaluated on

- Architecture Logic
- Hybrid Innovation
- Ablation Studies
- Deep Learning Literature Review
- DL Dataset & Regularization
- Technical Validation
- Theoretical Rigor
- GitHub Repository & Code Quality
- Project Presentation
- Viva Voce
- Project Report (LaTeX/IEEE format)

## Planned folder structure

| File / Folder | Description |
|---------------|-------------|
| `flight_delay_dl.ipynb` | All Phase 2 code |
| `figures/` | Plots saved by the notebook |
| `report/` | Phase 2 report in IEEE format |
| `presentation/` | Phase 2 viva presentation |
| `requirements.txt` | Python packages for Phase 2 (Phase 1 packages plus PyTorch) |
