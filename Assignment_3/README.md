# DA5401 Assignment 3: Addressing Class Imbalance with Clustering and Resampling

This repository contains the submission for Assignment 3 of the DA5401 course.

- **Student Name**: Khushi Gatwar
- **Roll Number**: DA25S004

---

## Project Overview

This project tackles the common challenge of class imbalance within a credit card fraud detection dataset. The primary goal is to leverage unsupervised learning (K-Means clustering) to perform intelligent resampling—specifically **Clustering-Based Oversampling (CBO)** and **Clustering-Based Undersampling (CBU)**. The effectiveness of these techniques is evaluated by comparing the performance of a Logistic Regression classifier trained on the resampled data against a baseline model and a model trained using the naive SMOTE oversampling method.

The entire analysis, including data exploration, model implementation, evaluation, and conclusion, is documented in the accompanying Jupyter Notebook (`Assignment_3.ipynb`).

---

## Methodology

The analysis follows a structured approach to address the problem statement:

1.  **Data Exploration & Baseline Model**: The `creditcard.csv` dataset is loaded and analyzed to identify the severe class imbalance. A baseline Logistic Regression model (Model 1) is trained on the original, imbalanced data to establish a performance benchmark.

2.  **Resampling Techniques**: Three different resampling methods were applied **only to the training data** to create balanced datasets:
    * **SMOTE (Synthetic Minority Over-sampling Technique)**: A naive oversampling method to generate synthetic fraud samples.
    * **Clustering-Based Oversampling (CBO)**: A custom implementation where the minority (fraud) class is clustered with K-Means, and then each cluster is oversampled to preserve the data's internal structure.
    * **Clustering-Based Undersampling (CBU)**: A custom implementation where the majority (non-fraud) class is clustered with K-Means, and each cluster is proportionally undersampled to maintain a representative sample while reducing its size.

3.  **Model Comparison & Evaluation**: Four Logistic Regression models were trained on the different datasets and evaluated on the **original, imbalanced test set** to simulate real-world performance. The key metrics for comparison were **Precision, Recall, and F1-Score** for the minority (fraud) class.

---

## File Structure

For evaluation, the following files are essential and should be present in the submission folder:

```
.
├── Assignment_3.ipynb      # The main Jupyter Notebook containing all code and analysis.
├── creditcard.csv          # The dataset required to run the notebook.
└── README.md               # This documentation file.
```

---

## How to Run the Code

To reproduce the analysis, please follow these steps:

1.  **Prerequisites**:
    * Python 3.x
    * Jupyter Notebook or JupyterLab

2.  **Install Libraries**:
    Ensure all required Python libraries are installed. You can install them using pip:
    ```bash
    pip install pandas numpy matplotlib seaborn scikit-learn imbalanced-learn
    ```

3.  **Execution**:
    * Place the `creditcard.csv` dataset in the same directory as the `Assignment_3.ipynb` notebook.
    * Open the `Assignment_3.ipynb` notebook in Jupyter.
    * Run all cells sequentially from top to bottom. The notebook is self-contained and includes all necessary steps for data loading, preprocessing, model training, and evaluation.

---

## Key Findings & Conclusion

The analysis confirmed that resampling is critical for improving the recall of fraud detection models. While all resampling techniques successfully increased the model's ability to identify fraudulent transactions, **Clustering-Based Oversampling (CBO) provided the most effective balance**.

The CBO model (Model 3) achieved a high recall of **90.8%** while maintaining a precision of **12.8%**, resulting in the highest **F1-Score (0.22)** among all models. This demonstrates its superiority over naive methods like SMOTE, which suffered from extremely low precision due to the generation of noisy samples.

**Final Recommendation**: The company should adopt the **Clustering-Based Oversampling (CBO)** strategy to train its fraud detection models. This approach offers the best trade-off between maximizing fraud detection and minimizing false positives, thereby enhancing security without severely impacting legitimate customer transactions.
