# Powerlifting Competition Total Prediction

## The Question

Can bodyweight and time between competitions reliably predict an athlete's future competition total? And if so, how much do these variables actually matter compared to other factors driving performance?

---

## Motivation

Powerlifting competition results vary between meets, sometimes minimally, sometimes drastically. Understanding what drives those changes helps influence programming, competition planning, and competition time decisions. This project tests whether two simple, easy-to-measure variables (bodyweight and time between meets) carry predictive power, or whether competition performance is shaped by more complex factors.

---

## Findings

**Neither variable showed meaningful correlation with future competition totals.**

Bodyweight and time between meets did not produce a reliable, significant regression model for predicting performance outcomes. MAE and RMSE indicated poor predictive accuracy, and residual analysis confirmed the model was not capturing the underlying patterns in the data.

This is itself a meaningful result — it suggests that competition performance cannot be explained by these surface-level variables alone, and points toward more complex factors (training quality, peaking strategy, technical consistency, day-of conditions) as the real drivers of meet outcomes. This shows that choosing a weight class and or time to compete in a future meet should not be driving factors for athlete programming and coaching decisisons.

---

## Methodology

1. Collected historical powerlifting competition data
2. Engineered features: bodyweight at time of meet, days elapsed since previous competition
3. Built a baseline model and a linear regression model using scikit-learn
4. Evaluated with MAE (Mean Absolute Error) and RMSE (Root Mean Squared Error)
5. Visualized predictions vs. actuals and residual distributions to diagnose model behavior

---

## Tools

- Python
- pandas
- NumPy
- scikit-learn
- Matplotlib
- Jupyter Notebook

---

## Repository Structure

```
powerlifting-prediction/
│
├── data/
│   └── powerlifting_data.csv         # Historical meet data
├── notebooks/
│   └── powerlifting_prediction.ipynb # Full analysis notebook
└── README.md
```

---

## Key Takeaway

Knowing that bodyweight and inter-meet rest time don't reliably predict performance is useful information — it rules out a hypothesis and points toward more nuanced modeling approaches.
