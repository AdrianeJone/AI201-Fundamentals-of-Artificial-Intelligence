# PA3-B – Neural Network with Backpropagation

**Course:** AI201 – Artificial Intelligence
**Semester:** 2nd Semester, AY 2025–2026
**Instructor:** Prospero C. Naval, Jr., Ph.D.
**Author:** Adriane Jone A. Abunda (2025-22450)
**Due Date:** March 27, 2026

---

## Overview

This assignment implements a **2-layer Multilayer Perceptron (MLP)** entirely from scratch using **NumPy**, trained with the **Backpropagation algorithm** and **momentum-based Stochastic Gradient Descent** (Generalized Delta Rule).

Two networks are trained and compared on the same 8-class classification task:
- **Network A** — Tanh hidden activations
- **Network B** — Leaky ReLU hidden activations

The dataset is preprocessed in a companion notebook using **SMOTE** (Synthetic Minority Oversampling Technique) to address class imbalance before training.

No scikit-learn, PyTorch, TensorFlow, or other ML frameworks are used for the core neural network logic — only NumPy.

---

## Dataset

| Property | Value |
|---|---|
| Training samples | 12,200 (SMOTE-balanced) |
| Validation samples | 800 |
| Features | 354 |
| Classes | 8 |

The dataset was balanced prior to training using SMOTE (see `Programming_Assignment_3_SMOTE.ipynb`), which generates synthetic samples for underrepresented classes to prevent the network from being biased toward majority classes.

---

## Architecture

Both networks share the same structure:

```
Input (354) → Hidden Layer 1 (100) → Hidden Layer 2 (50) → Output (8)
```

This architecture was selected through **hyperparameter tuning**: 30-epoch experiments were run across different hidden layer sizes `[64×32, 100×50, 128×64, 200×100]`, learning rates `[0.01, 0.001]`, and batch sizes `[8, 16, 32]`. The configuration with the lowest validation SSE was selected.

---

## Network Configurations

### Network A – Tanh–Tanh–Logistic

| Parameter | Value |
|---|---|
| Architecture | 354 → 100 → 50 → 8 |
| Hidden activations | Tanh (a = 1.716, b = 2/3) |
| Output activation | Logistic (a = 2.0) |
| Learning rate (η) | 0.001 |
| Momentum (α) | 0.9 |
| Batch size | 16 |
| Epochs | 200 |

### Network B – LeakyReLU–LeakyReLU–Logistic

| Parameter | Value |
|---|---|
| Architecture | 354 → 100 → 50 → 8 |
| Hidden activations | Leaky ReLU (slope = 0.01) |
| Output activation | Logistic (a = 2.0) |
| Learning rate (η) | 0.001 |
| Momentum (α) | 0.9 |
| Batch size | 16 |
| Epochs | 200 |

Weights are initialized using the **Haykin heuristic**: uniform distribution in `[-2.4/fan_in, 2.4/fan_in]`.

---

## Results

### Network A (Tanh) — Validation Set Performance

| Metric | Value |
|---|---|
| Accuracy | 98.88% |
| Macro Precision | ~0.99 |
| Macro Recall | ~0.99 |
| Macro F1 Score | 0.9886 |
| MCC | 0.9871 |

Training SSE dropped from ~5,496 to ~56 over 200 epochs. Validation SSE decreased from ~350 to ~7.1, with occasional momentum-induced spikes that recover quickly — confirming no persistent overfitting.

### Key Observations

- Classes 5 and 7 are classified perfectly (F1 = 1.0)
- Lowest per-class performance on Classes 6 and 8 (F1 ≈ 0.96), which share the most similar feature representations
- MCC close to 1.0 confirms strong multiclass discrimination across all classes, not driven by any dominant class

---

## Files

| File | Description |
|---|---|
| `AI201-2S25-26-PA3_Neural_Network.pdf`  | Instructions for the assignment |
| `Programming_Assignment_3_Neural_Network.ipynb` | Main notebook — MLP training, evaluation, and comparison |
| `Programming_Assignment_3_SMOTE.ipynb` | Data preprocessing — SMOTE oversampling |
| `PA3_Adriane_Jone_Abunda.pdf` | Written report |
| `training_set.csv` / `training_labels.csv` | SMOTE-balanced training data |
| `validation_set.csv` / `validation_labels.csv` | Validation data |
| `test_set.csv` | Unlabeled test set for final predictions |
| `trained_weights_NetworkA.csv` | Saved weights for Network A |
| `trained_weights_NetworkB.csv` | Saved weights for Network B |
| `train_sse_A.csv` / `train_sse_B.csv` | Training SSE per epoch |
| `val_log_A.csv` / `val_log_B.csv` | Validation metrics per epoch |
| `metrics_A.csv` / `metrics_B.csv` | Final evaluation metrics |
| `confusion_matrix_A.png` / `confusion_matrix_B.png` | Confusion matrix plots |
| `learning_curves_A.png` / `learning_curves_B.png` | Learning curve plots |
| `predictions_for_test_leakyrelu.csv` | Test set predictions from Network B |
| `predictions_for_test_tanh.csv` | Test set predictions from Network A |

---

## How to Run

1. Ensure Python 3 is installed with `numpy` and `matplotlib`.
2. **Run `Programming_Assignment_3_SMOTE.ipynb` first** to generate the balanced training and validation CSV files (if not already present).
3. Open `Programming_Assignment_3_Neural_Network.ipynb` in Jupyter and run all cells in order.

> All cells are pre-executed with outputs visible. The trained weight files are included, so the notebook can also be used to load and verify weights without re-training.

---

## Key Concepts Demonstrated

- Multilayer Perceptron architecture and design
- Forward pass and backpropagation from scratch
- Momentum-based SGD (Generalized Delta Rule)
- Activation functions: Tanh, Leaky ReLU, Logistic
- Haykin weight initialization
- Hyperparameter tuning with validation experiments
- Class imbalance handling with SMOTE
- Accuracy, Precision, Recall, F1, MCC evaluation
- Save/load of trained model weights
