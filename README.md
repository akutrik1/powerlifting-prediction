# Powerlifting Meet Total Predictor

Can we predict a powerlifter's next competition total from their history?

This project explores that question using data from over **835,000 meet results** sourced from [OpenPowerlifting](https://openpowerlifting.gitlab.io/opl-csv/) — one of the most comprehensive open-source records of competitive powerlifting worldwide.

---

## The Question

> *Given a lifter's previous total, bodyweight, and the time between meets, how accurately can we predict their next competition total?*

---

## What's in This Repo

```
powerlifting-predictor/
├── powerlifting_predictor.ipynb   # Full analysis notebook
├── database_v1.csv                # Filtered & cleaned base dataset
├── compared_data.csv              # Engineered feature dataset (model input)
└── README.md
```

---

## Methodology

### Data Pipeline

Starting from the raw OpenPowerlifting dataset (~2M+ entries), the data was narrowed to a consistent, comparable population:

- **Raw equipment only** — removes equipped lifters (single-ply, multi-ply) whose totals aren't directly comparable
- **Full power (SBD)** — squat + bench + deadlift events only
- **Valid total required** — excludes disqualifications and bomb-outs
- **2+ meets per lifter** — required to compute meet-to-meet changes

This produced **835,473 meet entries** across a multi-meet lifter population.

### Feature Engineering

For each consecutive pair of meets per lifter, the following features were derived:

| Feature | Description |
|---|---|
| `PrevTotalKg` | Lifter's total at their previous meet |
| `PrevBodyweightKg` | Lifter's bodyweight at their previous meet |
| `DaysSinceLastMeet` | Days elapsed between the two meets (capped at 1–1,000) |
| `CurrTotalKg` | Target — the actual total at the current meet |

Final comparison dataset: **356,955 meet transitions**

### Models

| Model | MAE | RMSE |
|---|---|---|
| Baseline (average change) | 22.79 kg | 42.65 kg |
| Linear Regression | 23.08 kg | 41.85 kg |

---

## Key Finding

Linear regression offers only a marginal improvement over the naive baseline. Inspecting the coefficients reveals why:

| Feature | Coefficient |
|---|---|
| Previous Total (kg) | 0.9617 |
| Previous Bodyweight (kg) | 0.0967 |
| Days Since Last Meet | 0.0122 |

**Previous total dominates almost entirely.** This makes the model a reasonable forecasting tool — but it means bodyweight fluctuation and rest time contribute very little to predicting the *absolute* total.

This finding reframed the original question: rather than predicting the total itself, the more meaningful target may be the *change* in total — and whether bodyweight fluctuation + time between meets can explain that delta. That follow-up is the next phase of this project.

---

## Tools

- Python 3
- pandas
- NumPy
- scikit-learn
- Matplotlib

---

## Data Source

[OpenPowerlifting](https://openpowerlifting.gitlab.io/opl-csv/) — Public domain dataset, updated regularly. Download the latest CSV and place it in the project directory as `openpowerlifting-latest.csv` to reproduce the full pipeline from scratch.

---

## Limitations

- Lifters sharing the same name may be incorrectly grouped
- Weight class changes between meets are not accounted for
- Unobserved factors (injury, programming, coaching) introduce irreducible noise
- Male and female lifters are pooled — splitting by sex would likely improve accuracy
