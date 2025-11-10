# Telecom Churn Prediction (DL_2025_Group_35)

## Overview
Predict customer churn for a telecom dataset. The project explores multiple modeling approaches, data drift monitoring, and an inference pipeline, all orchestrated in `main.ipynb`.

Colab Link : https://colab.research.google.com/github/TheJojoJoseph/DL_2025_Group_35/blob/main/main.ipynb#scrollTo=dfgRwRObhOW5

Github: github/TheJojoJoseph/DL_2025_Group_35

## Executive Summary
This project successfully developed, trained, and compared deep learning models (ANN and 1D CNN) to predict customer churn in the telecom sector using US telecom data (653,753 rows × 74 columns). The goal was to identify customers likely to discontinue service to enable targeted retention campaigns. Despite a severe class imbalance (4.57% churn rate), the Artificial Neural Network (ANN) achieved the best overall performance, with 95.9% accuracy and a Recall of 0.1441, indicating superior ability to detect actual churners compared to the CNN. Key business insights highlight high ARPU customers and specific data usage patterns as major churn risk factors.

## Project Details
### Team
- Abdul Kuddus (M24DE3002)(G23AI2044)
- Ritik Sharma (M24DE3065)(G23AI2024)
- Mohit Mathur (M24DE3050)(G23AI2034)
- Jojo Joseph (M24DE3041)(G23AI2100)

## Data
- The notebook loads a CSV with customer usage and account features and the target `Churn Value`.
- Data source priority:
  - Local file if available: `Telecom_Data.csv` or `./data/Telecom_Data.csv`.
  - Fallback public S3 link: `https://s3.amazonaws.com/projex.dezyre.com/telecom-machine-learning-project-for-customer-churn/materials/Telecom_data.csv`.

## Approaches (Brief)
- **Logistic Regression**
  - Linear baseline for binary classification.
  - Pros: fast, interpretable coefficients. Cons: limited on non-linear patterns.

- **Random Forest**
  - Ensemble of decision trees using bagging.
  - Handles mixed feature types, robust to noise, captures non-linearities.

- **XGBoost**
  - Gradient boosted trees with strong regularization and efficient handling of large, sparse one-hot inputs.
  - Often strong performance on tabular churn problems.

- **Neural Network (Keras)**
  - Dense network with dropout and early stopping.
  - Useful to benchmark against tree ensembles; requires careful preprocessing and tuning.

- **Histogram Gradient Boosting (scikit-learn) — Added**
  - Fast, memory-efficient gradient boosting (`HistGradientBoostingClassifier`).
  - Pipeline includes: one-hot encoding for categoricals (unknown-safe), passthrough for numerics.
  - Evaluates Accuracy, Precision, Recall, F1, ROC AUC. Optional downsample for speed on very large data.

- **Data Drift Monitoring (deepchecks)**
  - Checks for feature/label drift across time or splits to maintain model reliability over time.

- **Inference Pipeline**
  - Applies the chosen preprocessing and model to new data.
  - Handles missing labels and triggers retraining logic when drift or degraded metrics are detected.

## How to Run
### 1) Directly execute the notebook (recommended)
```
jupyter nbconvert --execute --ExecutePreprocessor.timeout=1800 \
  --to notebook --output churn_modeling.executed.ipynb churn_modeling.ipynb
```
Notes:
- Requires internet if the local CSV is absent (uses the S3 fallback).
- Timeout (30 min) covers training for larger models.

### 2) Open in Jupyter/Colab
- Jupyter: open `churn_modeling.ipynb` and Run All.
- Colab: the notebook guards the Drive mount and will work if you mount and place the CSV accordingly.

## Requirements
- Python 3.8+
- Key packages: pandas, numpy, scikit-learn, xgboost, tensorflow (for the NN cells), deepchecks, jupyter.
- Install with pip, for example:
```
pip install pandas numpy scikit-learn xgboost tensorflow deepchecks jupyter
```

## Repository Structure
- `churn_modeling.ipynb` — main end-to-end workflow.
- `README.md` — this document.
- `Telecom_Data.csv` (optional) — local data file if you place it in the repo.
- `comparison_of_approaches.md` — qualitative and quantitative comparison of approaches.

## Notes
- The notebook auto-selects a local CSV if present, else pulls from the public S3 link.
- Large data can slow training; the added HistGB approach includes an optional downsample for quicker iteration.

## Requirement
numpy
pandas
matplotlib
seaborn
scikit-learn
tensorflow
torch
tqdm
h5py
Pillow
kagglehub
ultralytics
wandb
pytorch-tabnet