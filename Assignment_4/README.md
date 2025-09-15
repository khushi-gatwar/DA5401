# DA5401 Assignment 4: GMM-Based Synthetic Sampling for Imbalanced Data

This repository contains the submission for Assignment 4 of the DA5401 course.

- **Student Name**: Khushi Gatwar
- **Roll Number**: DA25S004

---

## 1. Project Objective

This project addresses the critical challenge of class imbalance in a credit card fraud detection dataset using a sophisticated, model-based approach. The primary objective is to implement and evaluate a synthetic data generation pipeline using a **Gaussian Mixture Model (GMM)**. The goal is to create a more representative training set for the minority (fraudulent) class, thereby improving a classifier's ability to detect fraud without significant drawbacks like a high false positive rate.

The effectiveness of this GMM-based approach is compared against a baseline model trained on the original, imbalanced data.

---

## 2. Methodology

The analysis follows a systematic pipeline to build, evaluate, and compare the fraud detection models.

### Part A: Baseline Model
1.  **Data Analysis**: The `creditcard.csv` dataset was loaded and analyzed, confirming a severe class imbalance where fraudulent transactions constitute less than 0.2% of the data.
2.  **Model Training**: The data was split into training and testing sets, with the test set retaining the original imbalanced distribution. A baseline Logistic Regression classifier was trained on the imbalanced training data.
3.  **Baseline Evaluation**: The baseline model was evaluated using **Precision, Recall, and F1-score**, as these metrics are more informative than accuracy for imbalanced problems.

### Part B: GMM for Synthetic Sampling
1.  **GMM Implementation**: A Gaussian Mixture Model was fitted exclusively to the minority (fraud) class data from the training set. The optimal number of components (`k=3`) was determined using the **Bayesian Information Criterion (BIC)** to ensure the model best captured the underlying data distribution without overfitting.
2.  **Synthetic Data Generation**: Two balanced training datasets were created using the fitted GMM:
    * **GMM Oversampling**: New synthetic fraud samples were generated to match the number of non-fraud samples in the original training set.
    * **Hybrid (CBU+GMM)**: A combination approach where the majority class was first reduced using **Clustering-Based Undersampling (CBU)**, and then the minority class was oversampled with GMM to create a smaller, 1:1 balanced training set.

### Part C: Performance Evaluation
1.  **Model Comparison**: Two new Logistic Regression classifiers were trained on the GMM-balanced datasets. Their performances were evaluated on the **original, imbalanced test set** and compared against the baseline model.
2.  **Conclusion**: The results were analyzed to determine the impact of GMM-based sampling on the classifier's ability to detect fraud.

---

## 3. File Structure

The submission is organized as follows. For a complete evaluation, all files listed below are essential.

```
.
├── Assignment_4.ipynb      # The Jupyter Notebook with all code, analysis, and explanations.
├── creditcard.csv          # The dataset required to run the notebook.
└── README.md               # This documentation file.
```

---

## 4. How to Run the Analysis

To reproduce the results, please follow these instructions:

1.  **Prerequisites**:
    * Python 3.x
    * Jupyter Notebook or JupyterLab

2.  **Install Required Libraries**:
    The analysis requires several Python libraries. They can be installed via pip:
    ```bash
    pip install pandas numpy matplotlib seaborn scikit-learn
    ```

3.  **Execution Steps**:
    * Ensure the `creditcard.csv` file is located in the same directory as the `Assignment_4.ipynb` notebook.
    * Open `Assignment_4.ipynb` in a Jupyter environment.
    * Run the notebook cells sequentially from top to bottom. The notebook is self-contained and will execute the entire pipeline, from data loading to generating the final performance comparison plots and conclusions.

---

## 5. Key Findings and Recommendation

The analysis demonstrates that using GMM for synthetic data generation is a highly effective technique for this context.

* **Impact**: Both GMM-based resampling models significantly improved **Recall** (from 0.64 to over 0.88) compared to the baseline, proving their ability to better detect fraudulent transactions.
* **Best Model**: The **GMM Oversampling** approach yielded the most effective performance. It achieved the highest **Recall (0.91)** and the highest **F1-Score (0.15)**. The Hybrid (CBU+GMM) model, while also improving recall, suffered from significant information loss during the undersampling phase, which ultimately degraded its precision and overall performance.
* **Recommendation**: It is recommended that the financial institution adopt the **GMM Oversampling strategy**. This approach provides a powerful tool for enhancing security by ensuring the maximum number of fraudulent transactions are identified. While the precision is low, it offers the strongest starting point for a multi-stage fraud detection system where precision can be improved with subsequent models or rule-based filters.
