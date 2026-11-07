# Flight Delay Prediction (Project 21) — Phase 2: Deep Learning

Phase 2 adds a **deep learning model** to the same problem as [Phase 1](../phase1): predict whether a flight will
**arrive 15 or more minutes late**, using only information known **before departure**.

The model is a compact **multilayer perceptron (MLP) with learned embeddings** for carrier, origin and destination,
trained on exactly the Phase 1 data, features, date split and metrics, so the comparison is fair.

## How to run

Run these from the repository root:
```bash
cd phase2
python3 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
jupyter notebook flight_delay_dl.ipynb
```

Then run all cells (Kernel → Restart & Run All). The whole notebook runs in about 1–2 minutes on a laptop CPU.

## Folder structure

| File / Folder | Description |
|---------------|-------------|
| `flight_delay_dl.ipynb` | All Phase 2 code: data pipeline, Phase 1 baselines, MLP, ablation, calibration, what-if |
| `figures/` | Plots saved by the notebook (used in the report and slides) |
| `report/main.tex`, `report/main.pdf` | Phase 2 report in IEEE format (`references.bib` holds the references) |
| `presentation/` | Phase 2 viva presentation (`.pptx` with speaker notes, and `.pdf`) |
| `requirements.txt` | Python packages for Phase 2 (Phase 1 packages plus PyTorch) |

## Method (short)

1. **Data and features:** same as Phase 1 (leakage-free, cyclic time encoding, congestion on the full schedule,
   7-day delay history for carrier, origin, destination and route). Split by date: train Jan–Aug, validation Sep–Oct,
   test Nov–Dec.
2. **Preprocessing for the network:** categories → integer ids (id 0 = never seen in training), numeric features
   standardised with training statistics, no class weights.
3. **Architecture:** embeddings (carrier 8-d, origin 2-d, destination 16-d) + 14 numeric features → Dense 128 →
   Dense 64 → 1 output, ReLU and dropout 0.3. 15,361 parameters.
4. **Training:** AdamW (learning rate 0.001, weight decay 0.0001), batch size 1,024, early stopping on validation
   PR AUC (patience 5).
5. **Validation:** 5 random seeds, ablation study (5 variants × 5 seeds), calibration (temperature scaling).
6. **What-if rescheduling:** re-score the riskiest 10% of test flights at departure times ±1–2 hours.

No hybrid ML + DL model was used, and the optional temporal model was left out.

## Results (test set, Nov–Dec 2013)

| Model | PR AUC | ROC AUC | Recall @ precision 0.5 | Brier |
|-------|--------|---------|------------------------|-------|
| Random guess | 0.258 | 0.500 | – | – |
| Logistic Regression (Phase 1) | 0.376 | 0.645 | 0.059 | 0.228 |
| XGBoost (Phase 1) | **0.391** | **0.656** | **0.111** | 0.219 |
| **MLP with embeddings** | 0.386 | 0.653 | 0.094 | **0.182** |

- **Stable across seeds:** test PR AUC 0.3845 ± 0.0027 over 5 seeds.
- **Best probabilities:** the raw MLP has the lowest Brier score. Temperature scaling (T = 0.785) made it slightly
  worse (0.185), because the validation months were calmer than the test months.
- **Ablation:** removing the 7-day history features drops PR AUC to 0.3575; embeddings perform on par with one-hot
  encoding; regularisation halves the seed-to-seed spread.
- **What-if:** 92.7% of the riskiest flights have a lower-risk slot (mostly 2 hours earlier); mean predicted risk
  falls from 0.488 to 0.441. This is a model-based estimate, not a causal effect.

## Team (Phase 2 contributions)

| Member | Contribution |
|--------|--------------|
| Asad Ali | Data preparation for the network (ids, standardisation, tensors) |
| Divyansh Bhartia | MLP architecture and entity embeddings |
| [Vikrant Yadav](https://github.com/vikgenix) | Training loop, regularisation, early stopping and seed stability |
| Mayank Pillai | Ablation study and comparison with Phase 1 |
| Prashant Raj | Evaluation, calibration and what-if rescheduling analysis |
