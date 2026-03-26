AI201 - Programming Assignment 2: Naive Bayes Spam Filter
Author: Adriane Jone A. Abunda (2025-22450)
Date: March 8, 2026

FILES INCLUDED
--------------
1. PA2_Adriane_Jone_Abunda.pdf           — Written Report
2. AI201_Programming_Assignment_2.ipynb  — Jupyter Notebook (all cells executed)
3. train_set.csv                         — Training set (70%, 26,475 documents)
4. test_set.csv                          — Test set (30%, 11,347 documents)

REPRODUCTION NOTES
------------------
- The notebook was run against the TREC06 corpus with the labels file.
- Random seed is fixed at 42 to ensure reproducibility of the train/test split.
- All cells are pre-executed and outputs are visible in the notebook.
- Running Cell 1 will generate a new train_set.csv and test_set.csv.
- The notebook must be placed in the same folder that contains the labels file and the data folder. Failure to do so will result in file path errors when loading the corpus.