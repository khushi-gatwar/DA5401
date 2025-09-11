# Assignment 2: Dimensionality Reduction with PCA

## Student Information

- **Name:** Khushi Gatwar
- **Roll Number:** DA25S004

---

## Project Overview

This project explores the application of **Principal Component Analysis (PCA)** on the Mushroom Dataset to reduce its dimensionality. The primary goal is to assess how this reduction impacts the performance of a **Logistic Regression** classifier. The analysis involves preprocessing the categorical data, applying PCA to identify the optimal number of components, and comparing the performance of a classifier trained on the original data versus the PCA-transformed data.

---

## Folder Structure

The submission is contained within a single folder. The key files for evaluation are:

- **`Assignment_2.ipynb`**: This is the main Jupyter Notebook containing the complete Python code, visualizations, and detailed analysis for the assignment. All steps, from data loading to model evaluation and conclusion, are documented within this file.
- **`mushrooms.csv`**: The dataset used for this analysis. It must be in the same directory as the notebook for the code to run correctly.
- **`README.md`**: This file, providing an overview and documentation for the submission.

---

## How to Run the Code

To reproduce the analysis, please follow these steps:

### 1. Prerequisites
Ensure you have Python installed, along with the following libraries:
   - `pandas`
   - `numpy`
   - `matplotlib`
   - `seaborn`
   - `scikit-learn`



### 2. Execution
- Place the `Assignment_2.ipynb` notebook and the `mushrooms.csv` dataset in the same folder.
- Open and run the Jupyter Notebook `Assignment_2.ipynb` from top to bottom. The notebook is self-contained and will generate all outputs and visualizations.

---

### Summary of Analysis and Findings
The analysis is structured into three main parts, as detailed in the notebook:

#### Part A: Exploratory Data Analysis & Preprocessing
- The dataset, which is entirely categorical, was loaded and prepared.
- **One-hot encoding** was performed, which expanded the feature set from 22 to 117 features. This step was necessary to convert categorical data into a numerical format suitable for PCA.
- The data was then **standardized** using `StandardScaler` to ensure that all features contribute equally to the PCA, as PCA is sensitive to feature variance.

#### Part B: Principal Component Analysis (PCA)
- PCA was applied to the preprocessed data.
- A **scree plot** was generated to visualize the explained variance. It was determined that **59 components** were sufficient to retain 95% of the variance.
- Visualizations of the first few principal components showed excellent **separability** between the edible and poisonous mushroom classes, indicating that PCA effectively captured the distinguishing features of the data.

#### Part C: Performance Evaluation
- A baseline **Logistic Regression model** trained on the full 117 features achieved a perfect accuracy of **1.0**.
- A second model trained on the **59 PCA-transformed components** achieved an accuracy of **0.9988**.
- The comparison demonstrated that PCA reduced the feature space by nearly **50%** with a negligible drop in performance. This highlights the trade-off between dimensionality reduction and information loss, proving PCA to be a highly effective technique for this dataset.
- The analysis also discussed how PCA helps mitigate **multicollinearity** introduced by one-hot encoding, leading to a more robust model.
