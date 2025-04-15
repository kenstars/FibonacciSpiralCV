# Fibonacci‑Spiral Hyper‑Parameter Search

### A Non‑Linear Alternative to GridSearchCV

IEEE Working Paper – "Leveraging the Fibonacci Spiral for Efficient Hyper‑Parameter Exploration"

## 📚 Overview
This repository accompanies the experiments and analysis presented in our upcoming IEEE paper.  We introduce Fibonacci‑Spiral Search CV – a lightweight, model‑agnostic hyper‑parameter tuner that traverses the search space along a Fermat spiral (golden‑angle spiral) rather than the axis‑aligned lattice used by GridSearchCV.

Why?  A spiral sweep covers the domain quasi‑uniformly in far fewer steps, reducing evaluation cost while still locating performant regions.  In many cases we observe Grid‑level accuracy with ≤ 50 % of the model fits.

## 🔬 Key Contributions

 Feature 

 Description 

FibonacciSpiralSearchCV

Drop‑in scikit‑learn compatible class (fit, predict, score).

Golden‑Angle Sampling

Successive points rotate by φ ≈ 137.5 °, producing a low‑discrepancy sequence that fills space evenly.

Any Estimator / Metric

Works with classifiers & regressors, any scoring string or callable.

Benchmark Notebook

Colab notebook reproduces all tables & plots in the paper (Titanic → RandomForest).

## 🗂️ Repository Layout

.
├── notebooks/
│   └── fibonacci_spiral_vs_gridsearchcv.ipynb   # Main Colab notebook (open in Google Colab badge)
├── src/
│   └── fibspiral_search.py                      # Implementation of FibonacciSpiralSearchCV
├── data/
│   └── titanic_cleaned.csv                      # Example dataset (Kaggle Titanic, pre‑cleaned)
├── docs/
│   └── img/                                     # Figures used in paper / README
├── tests/
│   └── test_fibspiral.py                        # Basic unit tests
└── requirements.txt                             # Python ≥3.9 dependencies

Quick start: If you only want to run the experiment, open the notebook directly in Colab:


## ⚡ Installation (local)

# 1. Clone the repo
$ git clone https://github.com/your‑user/your‑repo.git && cd your‑repo

# 2. Create env & install deps
$ python -m venv .venv && source .venv/bin/activate
$ pip install -r requirements.txt

# 3. Run unit tests (optional)
$ pytest

## 🚀 Usage Example

from sklearn.ensemble import RandomForestClassifier
from fibspiral_search import FibonacciSpiralSearchCV

param_bounds = {
    "n_estimators": (50, 300),
    "max_depth":    (3, 10)
}

fib_cv = FibonacciSpiralSearchCV(
    RandomForestClassifier(random_state=42),
    param_bounds=param_bounds,
    n_iter=25,
    scoring="accuracy",
    cv=5,
    random_state=42
)

fib_cv.fit(X_train, y_train)
print(f"Best params → {fib_cv.best_params_};  CV score = {fib_cv.best_score_:.4f}")

## 📈 Reproducing the Results
| Fold | Method | Accuracy | Macro‑F1 | ROC AUC | Wall
