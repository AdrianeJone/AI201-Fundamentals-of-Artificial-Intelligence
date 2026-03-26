# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

AI 201 Programming Assignment 3 — implementing backpropagation from scratch using NumPy. Two Jupyter notebooks make up the full pipeline.

## Running the Notebooks

Open and run cells in order:

1. `Programming_Assignment_3_SMOTE.ipynb` — balances the raw dataset via SMOTE and produces the train/validation CSVs
2. `Programming_Assignment_3_Neural_Network.ipynb` — trains two MLP variants and saves weights + test predictions

Dependencies: `numpy`, `matplotlib`, `imbalanced-learn` (for SMOTE)

## Data Pipeline

```
data.csv + data_labels.csv
        ↓ (SMOTE notebook)
training_set.csv / training_labels.csv
validation_set.csv / validation_labels.csv
        ↓ (Neural Network notebook)
trained_weights_NetworkA.csv  (Tanh hidden layers)
trained_weights_NetworkB.csv  (LeakyReLU hidden layers)
predictions_for_test_tanh.csv
predictions_for_test_leakyrelu.csv
```

- Input: 3486 samples × 354 features, 8 classes (heavily imbalanced)
- After SMOTE: 13000 samples (1625 per class), shuffled, split 12200 train / 800 val
- Labels are one-hot encoded (8 columns) for training; integer labels (1–8) for predictions

## Architecture

All neural network code lives in the Neural Network notebook as plain Python classes (no frameworks):

- **`Activation`** (base) → `Logistic(a=2.0)`, `Tanh(a=1.716, b=2/3)`, `LeakyReLU(slope=0.01)` — each implements `forward(v)` and `backward(y)`
- **`Layer`** — holds weights `W`, biases `b`, momentum terms `dW_prev`/`db_prev`; weight init uses `±2.4/fan_in`
- **`MLP`** — composes layers; `fit()` runs mini-batch SGD with momentum (`alpha=0.9`, `eta=0.001`, `batch_size=8`, `epochs=200`)

**Network A**: Tanh → Tanh → Logistic (354 → 100 → 50 → 8)
**Network B**: LeakyReLU → LeakyReLU → Logistic (354 → 100 → 50 → 8)

Weight update rule: `ΔW = (η × ∇W) + (α × ΔW_prev)`

`evaluate_performance()` computes confusion matrix, accuracy, macro precision/recall/F1, and MCC (Matthews Correlation Coefficient) without using scikit-learn.

## Key Design Notes

- `np.random.seed(42)` is set at the top of the Neural Network notebook for reproducibility
- `backward()` in `Tanh` and `Logistic` takes the **post-activation output** `y` (not the pre-activation `v`), because their derivatives are expressed in terms of the output
- `backward()` in `LeakyReLU` takes the **pre-activation** `v`
- Predictions add 1 to `argmax` output (`+1`) to convert 0-based indices back to class labels 1–8
