# PA2 – Naive Bayes Spam Filter

**Course:** AI201 – Artificial Intelligence
**Semester:** 2nd Semester, AY 2025–2026
**Instructor:** Prospero C. Naval, Jr., Ph.D.
**Author:** Adriane Jone A. Abunda (2025-22450)
**Due Date:** March 13, 2026

---

## Overview

This assignment implements a **Naive Bayes text classifier** from scratch to distinguish spam from legitimate email (ham). The classifier is trained and evaluated on the **TREC06 corpus**, a standard benchmark dataset for spam detection research.

The implementation covers three progressive stages:

1. **Baseline classifier** – Naive Bayes with no smoothing
2. **Lambda smoothing** – Additive (Laplace) smoothing to handle the zero-frequency problem
3. **Feature selection** – Mutual Information ranking following Hovold (2005) to reduce the feature space

All core logic is implemented in pure Python using only the standard library and `matplotlib`. No scikit-learn or external ML frameworks are used.

---

## Dataset

**TREC06 Corpus** (English subset, `trec06p-ai201`)

| Split | Documents |
|---|---|
| Training set (70%) | 26,475 |
| Test set (30%) | 11,347 |
| **Total** | **37,822** |

The dataset was pre-split using a fixed random seed (`seed=42`) for reproducibility. The labels file maps each email to its true class (`spam` or `ham`).

---

## What Was Implemented

### 2.1 – Baseline Naive Bayes (No Smoothing)

- Parses each email into a **set of unique words** (bag-of-words, binary presence)
- Computes prior probabilities P(spam) and P(ham) from training data
- Classifies using **log-probability sums** to avoid floating-point underflow
- **Result:** Precision: 0.9991 | Recall: 0.9218

The high precision but lower recall is explained by the **zero-frequency problem**: if a test email contains a word never seen in spam training documents, its log-probability becomes −∞, causing the model to default to predicting ham (false negative).

### 2.2 – Lambda (Additive) Smoothing

Resolves the zero-frequency problem by adding a smoothing factor λ to all word counts. Lambda values tested: `[2.0, 1.0, 0.5, 0.1, 0.005]`.

| λ | Precision | Recall | F1 |
|---|---|---|---|
| 2.0 | 0.9941 | 0.9815 | 0.9878 |
| **1.0** | **0.9947** | **0.9840** | **0.9893** |
| 0.5 | 0.9949 | 0.9792 | 0.9870 |
| 0.1 | 0.9948 | 0.9582 | 0.9762 |
| 0.005 | 0.9990 | 0.9045 | 0.9494 |

**Best λ = 1.0 (Laplace Smoothing):** F1 score peaks at **0.9893**, recovering recall from 0.9218 to 0.9840 while maintaining precision above 0.99.

### 2.3 – Mutual Information Feature Selection (Hovold 2005)

Reduces the 82,476-word vocabulary to the **200 most informative words** using Mutual Information (MI) ranking, following the methodology of Hovold (2005).

- The top 200 most *frequent* words are first excluded (these are non-discriminative tokens such as stop words and HTML artifacts)
- MI is then computed for all remaining words
- The top 200 MI-ranked words are used as the reduced vocabulary

| Condition | Vocabulary Size | Precision | Recall | F1 |
|---|---|---|---|---|
| Full Vocab (λ=1.0) | 82,476 | 0.9947 | 0.9840 | 0.9893 |
| Reduced Vocab (MI Top 200) | 200 | 0.9731 | 0.9376 | 0.9550 |

**Dimensionality reduction: 99.76%** with only a ~3.4% drop in F1 — validating that a small set of highly discriminative words captures most of the classification signal.

---

## Files

| File | Description |
|---|---|
| `AI201_2SAY25-26 Spam Detection using Naive Bayes.pdf` | Instructions for the assignmen |
| `AI201_Programming_Assignment_2.ipynb` | Main Jupyter Notebook (all cells pre-executed) |
| `PA2_Adriane_Jone_Abunda.pdf` | Written report |
| `train_set.csv` | Training set (26,475 emails, 70% split) |
| `test_set.csv` | Test set (11,347 emails, 30% split) |
| `labels` | TREC06 labels file (spam/ham per email path) |
| `data/` | TREC06 email corpus directory |

> **Note:** The `labels` file and `data/` folder must be in the same directory as the notebook. The notebook reads relative paths from these files.

---

## How to Run

1. Ensure Python 3 is installed with `matplotlib` available.
2. Place the notebook inside the folder that contains the `labels` file and the `data/` directory.
3. Open `AI201_Programming_Assignment_2.ipynb` in Jupyter.
4. Run all cells in order. The first cell regenerates `train_set.csv` and `test_set.csv` using `seed=42`.

> All cells are already pre-executed with outputs visible. You can read the results without re-running.

---

## Key Concepts Demonstrated

- Naive Bayes probabilistic classification
- Text preprocessing and bag-of-words representation
- Log-probability computation for numerical stability
- Zero-frequency problem and additive smoothing
- Mutual Information for text feature selection
- Precision, Recall, F1, and confusion matrix evaluation

---

## References

Hovold, J. (2005). *Naive Bayes Spam Filtering Using Word-Position-Based Attributes*. CEAS 2005.
