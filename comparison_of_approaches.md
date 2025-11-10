# Comparison of Approaches

This document compares the modeling approaches used in the churn prediction project across methodology, strengths/weaknesses, and evaluation metrics.

## Qualitative Comparison

- **Neural Network (ANN)**
  - Strengths: Flexible function approximator; can model complex interactions.
  - Weaknesses: Requires careful preprocessing; sensitive to class imbalance; longer training.
  - Use when: You can invest in architecture/tuning and want a deep learning benchmark.

- **1D CNN**
  - Strengths: Can learn local patterns if features are ordered meaningfully.
  - Weaknesses: Tabular features do not always have spatial locality; may underperform tree models.
  - Use when: Feature ordering conveys locality or you engineer embeddings/blocks for structure.

- **Transformer (Self-Attention)**
  - Strengths: Captures long-range feature interactions via attention; flexible architecture.
  - Weaknesses: Requires careful design for tabular data; may need more data/tuning; compute heavier than ANN.
  - Use when: You want to model global interactions beyond local patterns with a modern deep architecture.

- **TabNet (Google AI, 2021)**
  - Strengths: Designed specifically for tabular data; built-in feature selection via sequential attention; interpretable feature importance masks; competitive with gradient boosting; handles both categorical and continuous features natively.
  - Weaknesses: More hyperparameters to tune (decision steps, attention dimensions); slower training than tree-based models; requires careful regularization (sparsity coefficient).
  - Use when: You need interpretability with deep learning performance on tabular data; want to understand which features drive predictions; have mixed feature types.

## Quantitative Comparison (Metrics)

Note: Metrics depend on train/validation splits, preprocessing, and class imbalance handling. Regenerate to fill the table below after executing `churn_modeling.ipynb`.

| Model | Accuracy | Precision | Recall | F1 | ROC AUC |
|------|----------|-----------|--------|----|---------|
| ANN (Keras) | 0.9590 | TBD | 0.1441 | TBD | TBD |
| 1D CNN | TBD | TBD | TBD | TBD | TBD |
| Transformer | TBD | TBD | TBD | TBD | TBD |
| TabNet | TBD | TBD | TBD | TBD | TBD |

References:
- The ANN accuracy (95.9%) and recall (0.1441) are from the project’s current Executive Summary.

## Class Imbalance Considerations

- Churn rate is ~4.57% (highly imbalanced). Consider:
  - Threshold tuning on predicted probabilities to raise recall.
  - Class weights or focal loss (for NN) to emphasize minority class.
  - Calibrating probabilities (Platt/Isotonic) for decisioning.
  - Using recall/PR AUC as primary optimization criteria for retention targeting.

## Reproducing Metrics

- Execute the notebook to populate metrics:
```
jupyter nbconvert --execute --ExecutePreprocessor.timeout=1800 \
  --to notebook --output churn_modeling.executed.ipynb churn_modeling.ipynb
```
- Extract printed metrics from the model sections and update the table above.
