# AI201 – Artificial Intelligence: Programming Assignments

**Course:** AI201 – Artificial Intelligence
**Program:** Master of Engineering in Artificial Intelligence (MEng AI)
**Semester:** 2nd Semester, AY 2025–2026
**Instructor:** Prospero C. Naval, Jr., Ph.D.

---

## About

I am Adriane Jone A. Abunda, a graduate student in the Master of Engineering in Artificial Intelligence program. My undergraduate background is in BS Chemical Engineering, and these programming assignments represent my hands-on work as I build a foundation in AI and machine learning from the ground up.

This repository contains the three programming assignments I completed for AI201. Each assignment required implementing a core AI algorithm from scratch in Python, without relying on high-level ML libraries for the core logic, only NumPy, standard Python, and `matplotlib` were used.

---

## Assignments

### [PA1 - A* Search Algorithm](.PA1_A_star/)

Implemented the A\* informed search algorithm to solve the classic 8-puzzle problem, following the pseudocode from the course lectures. Compared three heuristic functions: Misplaced Tiles, Manhattan Distance, and Nilsson's Sequence Score, in terms of solution quality and search efficiency.

**Key skills:** Search algorithms, heuristic design, state-space search, path reconstruction

---

### [PA2 – Naive Bayes Spam Filter](.PA2_Spam_Filter/)

Implemented a Naive Bayes text classifier from scratch to detect spam emails using the TREC06 corpus (~37,800 emails). Explored the zero-frequency problem, additive (lambda) smoothing, and Mutual Information-based feature selection following the methodology of Hovold (2005).

**Key skills:** Probabilistic classification, text preprocessing, log-probability arithmetic, feature selection, confusion matrix analysis

---

### [PA3 – Neural Network (Backpropagation)](.PA3_Neural_Network/)

Built a 2-layer Multilayer Perceptron (MLP) from scratch using only NumPy, trained using the Backpropagation algorithm with momentum-based SGD (Generalized Delta Rule). Trained and compared two networks, one using Tanh activations and one using LeakyReLU, on an 8-class classification dataset with 354 features.

**Key skills:** Neural network architecture, forward/backpropagation, activation functions, hyperparameter tuning, class imbalance handling (SMOTE)

---

## Tools & Languages

- **Language:** Python 3
- **Environment:** Jupyter Notebook
- **Libraries:** NumPy, matplotlib, csv, math, re (no scikit-learn or deep learning frameworks for core logic)

---

## Notes

All notebooks were developed and submitted as part of the AI201 course requirements. Core algorithms were implemented from scratch following course-specified pseudocode and methodologies to ensure a deep understanding of the underlying concepts.
