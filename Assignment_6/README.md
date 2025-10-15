# DA5401 Assignment 6: Imputation via Regression for Missing Data

## Student Information

- **Name:** Khushi Gatwar
- **Roll Number:** DA25S004

---

## Project Overview

This project addresses a common challenge in data science: handling missing data within a dataset. As a machine learning engineer working on a credit risk assessment project, the primary goal is to implement and evaluate different strategies for imputing missing values in the **UCI Credit Card Default Clients Dataset**.

The effectiveness of each strategy is not judged on the imputed values alone, but on the performance of a downstream **Logistic Regression classification model** trained on the cleaned data. This approach provides a practical measure of which imputation technique is most beneficial for the end goal of predicting customer default.

Four distinct strategies were implemented and compared:
1.  **Simple Imputation (Baseline):** Using the median to fill missing values.
2.  **Regression Imputation (Linear):** Using a linear regression model to predict and fill missing values.
3.  **Regression Imputation (Non-Linear):** Using a K-Nearest Neighbors (KNN) regressor to predict and fill missing values.
4.  **Listwise Deletion:** Removing all rows containing any missing values.

---

## Folder Structure & Essential Files

For a complete evaluation of this submission, the following files must be present in the root directory:

```
.
├── Assignment_6.ipynb
├── UCI_Credit_Card.csv
└── README.md
```

- **`Assignment_6.ipynb`**: This is the main Jupyter Notebook containing all the Python code, visualizations, and detailed markdown explanations for the entire project. All steps, from data preprocessing and imputation to model training and comparative analysis, are documented within this file.

- **`UCI_Credit_Card.csv`**: The dataset required to run the notebook. It must be located in the same directory as the notebook file.

- **`README.md`**: This documentation file.

---

## How to Run the Code

To reproduce the results, please follow these steps:

**1. Prerequisites:**
Ensure you have a Python environment with the following libraries installed. You can install them using pip:
```bash
pip install pandas numpy scikit-learn seaborn matplotlib jupyterlab
```

**2. Execution:**
1.  Place the `UCI_Credit_Card.csv` dataset file in the same folder as the `Assignment_6.ipynb` notebook.
2.  Launch a Jupyter environment (e.g., Jupyter Lab, Jupyter Notebook, or VS Code with the Jupyter extension).
3.  Open `Assignment_6.ipynb`.
4.  To ensure reproducibility, run all the cells sequentially from top to bottom. The `random_state` has been set where necessary to guarantee consistent results.

---

## Summary of Findings & Key Insights

The analysis yielded a clear and somewhat counter-intuitive conclusion:

- **Performance Equivalence:** Despite the fact that regression-based imputation methods (Linear and KNN) created more realistic and varied imputed values that better preserved the original data's distribution, they offered **no significant performance improvement** over the simple baseline median imputation in the final classification task.

- **Underlying Reason:** An exploratory analysis using a correlation heatmap revealed that the imputed feature (`AGE`) had a very weak linear relationship with the other predictor variables. This lack of a strong signal meant that the sophisticated models had little information to learn from, making their predictions no more useful than a simple central tendency measure.

- **Final Recommendation:** Based on the results, the recommended strategy for this specific scenario is **Simple Median Imputation**. It achieves virtually identical performance to the more complex models while being significantly simpler and more computationally efficient. This highlights a key principle: the simplest effective solution is often the best.
