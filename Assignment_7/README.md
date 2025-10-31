# DA5401 Assignment 7: Multi-Class Model Selection using ROC and Precision-Recall Curves

## 🧑‍🎓 Student Information

* **Name:** Khushi Gatwar
* **Roll Number:** DA25S004

---

## 🚀 Project Overview

This project applies and interprets **Receiver Operating Characteristic (ROC)** curves and **Precision-Recall Curves (PRC)** for model selection in a multi-class classification environment. The task is to act as a machine learning scientist classifying land cover types using the **UCI Landsat Satellite dataset**, which is a 6-class problem.

The primary goal is to perform model selection by comparing a diverse set of six classifiers. The analysis uses **ROC-AUC** and **PRC-AP (Average Precision)** metrics, adapted for the multi-class setting using a One-vs-Rest (OvR) approach, to determine the best- and worst-performing models.

The project compares the following models:
* K-Nearest Neighbors (KNN)
* Decision Tree
* Dummy Classifier (Baseline)
* Logistic Regression
* Gaussian Naive Bayes
* Support Vector Machine (SVM)

Additionally, two "brownie point" ensemble models, **Random Forest** and **XGBoost**, are evaluated. The analysis concludes by comparing model rankings across four metrics (Accuracy, F1-Score, ROC-AUC, PRC-AP) and providing a final recommendation.

---

## 📁 Folder Structure & Essential Files

For a complete evaluation of this submission, the following files must be present in the root directory:
```
├── Assignment_7.ipynb 
├── sat.trn 
├── sat.tst 
├── README.md
```

* **Assignment\_7.ipynb:** This is the main Jupyter Notebook containing all Python code, visualizations, and detailed markdown explanations for the entire project.
* **sat.trn & sat.tst:** The training and testing data files for the Landsat Satellite dataset, required to run the notebook.
* **README.md:** This documentation file.

---

## ⚙️ How to Run the Code

1.  **Prerequisites:** Ensure you have a Python environment with the following libraries installed. You can install them using `pip`:
    ```bash
    pip install pandas numpy scikit-learn seaborn matplotlib xgboost jupyterlab
    ```

2.  **Execution:**
    * Place the `sat.trn` and `sat.tst` dataset files in the same folder as the `Assignment_7.ipynb` notebook.
    * Launch a Jupyter environment (e.g., Jupyter Lab, Jupyter Notebook).
    * Open `Assignment_7.ipynb`.
    * Run all the cells sequentially from top to bottom. The `random_state` has been set where necessary to ensure reproducible results.

---

## 📊 Summary of Findings & Key Insights

* **Ranking Consistency:** The model rankings were **highly consistent** across all four metrics (Accuracy, F1-Score, ROC-AUC, and PRC-AP). This gives high confidence that the identified "best" model is truly the most robust.

* **Top Performers (Required):**
    * **KNN** and **SVM** were the top performers, tying for the best **Macro-AUC (0.980)**.
    * **KNN** had the single highest **Macro-Average AP (0.9215)**, making it the most robust model for handling the dataset's moderate class imbalance.

* **Top Performers (Bonus):**
    * The ensemble models, **XGBoost** (AUC: 0.989, AP: 0.946) and **Random Forest** (AUC: 0.986, AP: 0.935), **outperformed all** of the original six models.

* **Baseline Analysis:**
    * The `DummyClassifier(strategy='prior')` correctly scored a **ROC-AUC of 0.5000** and a **PRC-AP of 0.1667** (approx. 1/6), perfectly representing a "no-skill" random guesser and validating the evaluation setup.
    * A custom **`PerverseClassifier`** (an inverted SVM) was successfully implemented to demonstrate an "anti-skill" model, achieving a Macro-AUC of **0.0203** (where 0.0 is perfectly wrong).

* **Difficulty Analysis:** The per-class analysis in both ROC and PRC calculations consistently identified **Class 4** (original label) as the most difficult class for all models to classify, yielding the lowest individual AUC and AP scores.

---

## 🏆 Final Recommendation

* **Recommended Model (Required List):** **K-Nearest Neighbors (KNN)**. It ranked #1 in Accuracy, F1-Score, and PRC-AP, and tied for #1 in ROC-AUC. This comprehensive dominance makes it the best choice from the required list.

* **Best Overall Model:** **XGBoost**. When including the bonus models, XGBoost provided the highest performance across all four metrics.

* **Alternative Recommendations:**
    * **SVM:** An excellent alternative to KNN with nearly identical performance (and likely faster prediction times).
    * **Logistic Regression:** The best choice if model interpretability is required, as it still achieved a very strong Macro-AUC (0.972) and AP (0.864).

