# DA5401 A8: Ensemble Learning for Complex Regression Modeling
## Bike Share Demand Prediction

## 🧑‍🎓 Student Information

* **Name:** Khushi Gatwar
* **Roll Number:** DA25S004

---

## 🚀 Project Overview

This project applies and compares three primary ensemble techniques (**Bagging, Boosting, and Stacking**) to solve a complex, time-series-based **regression** problem. The task is to act as a data scientist for a city's bike-sharing program and build a model to accurately forecast the total hourly count of rented bikes (`cnt`).

A critical aspect of this project is the use of a **chronological train-test split**, which correctly simulates forecasting the future and avoids data leakage. The primary goal is to minimize the prediction error (RMSE) by diagnosing the bias-variance trade-off and applying the correct ensemble strategy, including hyperparameter tuning.

The project compares the following models:
* Decision Tree (Baseline)
* Linear Regression
* Bagging Regressor
* Gradient Boosting Regressor (Default)
* **Gradient Boosting Regressor (Tuned)**
* Stacking Regressor

---

## 📁 Folder Structure & Essential Files

For a complete evaluation of this submission, the following files must be present in the root directory:
```
├── Assignment_8.ipynb 
├── hour.csv 
├── README.md
```

* **Assignment\_8.ipynb:** This is the main Jupyter Notebook containing all Python code, visualizations, and detailed markdown explanations for the entire project.
* **hour.csv:** The hourly data file for the Bike Sharing Demand Dataset, required to run the notebook.
* **README.md:** This documentation file.

---

## ⚙️ How to Run the Code

1.  **Prerequisites:** Ensure you have a Python environment with the following libraries installed. You can install them using `pip`:
    ```bash
    pip install pandas numpy scikit-learn seaborn matplotlib jupyterlab
    ```

2.  **Execution:**
    * Place the `hour.csv` dataset file in the same folder as the `Assignment_8.ipynb` notebook.
    * Launch a Jupyter environment (e.g., Jupyter Lab, Jupyter Notebook).
    * Open `Assignment_8.ipynb`.
    * Run all the cells sequentially from top to bottom. The `random_state` has been set to 42 where necessary to ensure reproducible results.

---

## 📊 Summary of Findings & Key Insights

* **Critical Insight: Chronological Split:** Using a chronological split (training on the "past," testing on the "future") was essential. It provided realistic, honest error scores and correctly revealed the models' true performance.

* **Best Model:** The **Tuned Gradient Boosting Regressor** was the undisputed winner, achieving the lowest Test RMSE of **67.45**. This was a **50.08% improvement** over the baseline.

* **The Power of Tuning:** The final tuning step was critical. The *default* Gradient Boosting model was good (Test RMSE 85.96), but the *tuned* version was **21.5% better**, proving that tuning is essential for optimizing performance.

* **Baseline Analysis:** The **Decision Tree (depth=6)** was the best baseline (Test RMSE: **135.12**). The Linear Regression model (Test RMSE: 183.28) performed terribly, proving the problem was highly non-linear.

* **The Bias-Variance Story:**
    1.  **Diagnosis:** The baseline Decision Tree (RMSE 135.12) suffered from **high variance (overfitting)**.
    2.  **Bagging (Variance-Fix):** We applied Bagging (a variance-reduction tool). It worked, improving the RMSE slightly to **130.48**.
    3.  **Boosting (Bias-Fix):** This showed the main problem was **high bias**. We applied a *default* Gradient Boosting model, which was the correct technique, slashing the RMSE to **85.96**.
    4.  **Tuning (Optimization):** This default model, while strong, was overfitting. A final **hyperparameter tuning** step solved this, achieving the winning RMSE of **67.45** and explaining over 90% of the variance (R² 0.906).
    5.  **Stacking (Failed):** The Stacking Regressor (Test RMSE 91.48) *failed* to beat even the default Boosting model, confirming it was not the right approach.

---

## 🏆 Final Recommendation

* **Recommended Model:** **Tuned Gradient Boosting Regressor**. It is the clear winner, providing the best predictive accuracy by a wide margin (Test RMSE 67.45). It successfully solved the high-bias nature of the problem and, after tuning, produced an exceptionally accurate model explaining over **90% of the variance** (R² 0.906).

* **Actionable Insight:** This project proves that a multi-step process is critical. We first diagnosed the problem (bias & variance), applied the correct tool (Boosting), and then **optimized that tool (Tuning)** to achieve the final, winning result.
