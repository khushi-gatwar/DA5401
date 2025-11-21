# DA5401 End-Semester Data Challenge Report
## Metric Learning for AI Evaluation System

## 🧑‍🎓 Student Information

* **Name:** Khushi Gatwar
* **Roll Number:** DA25S004

---

## 🚀 Project Overview

This project develops a **Metric Learning Model** to predict a "fitness score" (0.0 to 10.0) representing the semantic alignment between an **AI Evaluation Metric Definition** and a **Prompt-Response Pair**. The challenge involves handling multilingual data, severe class imbalance, and high-dimensional text embeddings.

The core innovation is the use of **Deep Learning Embeddings (Gemma-300M)** combined with a **Multi-Layer Perceptron (MLP)** regressor. We engineered specific features like **Cosine Similarity** and applied a **Log1p Target Transformation** to handle the skewed score distribution. The primary goal is to minimize the prediction error (RMSE).

The project compares the following approaches:
* TF-IDF + HistGradientBoosting (Baseline)
* TF-IDF + Categorical Features
* Stacking Regressor (TF-IDF based)
* Gemma Embeddings + HistGradientBoosting
* **Gemma Embeddings + MLP (Final Model)**

---

## 📁 Folder Structure & Essential Files

For a complete evaluation of this submission, the following files must be present in the root directory:

```text
├── Data_challenge.ipynb             # Main Notebook with code & analysis
├── train_data.json                  # Training dataset
├── test_data.json                   # Test dataset (for submission)
├── metric_names.json                # List of metric names
├── metric_name_embeddings.npy       # Pre-computed embeddings for metrics
├── train_text_embeddings_gemma.npy  # Cached Gemma embeddings (Train)
├── test_text_embeddings_gemma.npy   # Cached Gemma embeddings (Test)
├── last_submission.csv              # Final output predictions
├── README.md                        # Project documentation
```

### File Descriptions:
* **Data_challenge.ipynb:** The main Jupyter Notebook containing all code for EDA, feature engineering, model training, and evaluation.
* **train_data.json / test_data.json:** The primary dataset files containing prompts, responses, and scores.
* **metric_name_embeddings.npy:** Pre-computed embeddings for the metric definitions.
* **README.md:** This documentation file.

---

## ⚙️ How to Run the Code

### 1. Prerequisites
Ensure you have a Python environment with the following libraries installed:

```bash
pip install pandas numpy scikit-learn matplotlib seaborn sentence-transformers torch
```

### 2. Execution Steps
1.  **Setup:** Place all data files (`.json`, `.npy`) in the same directory as the notebook.
2.  **Launch:** Open `Data_challenge.ipynb` in Jupyter Lab, Jupyter Notebook, or Google Colab.
3.  **Embeddings Note:** The notebook utilizes caching for Gemma embeddings. The first run will take longer to generate these embeddings and save them as `.npy` files. Subsequent runs will load them from disk automatically.
4.  **Run:** Execute all cells sequentially from top to bottom.

---

## 📊 Summary of Findings & Key Insights

* **Critical Insight: Multilingual Challenge:** The baseline TF-IDF model (RMSE ~3.7) failed because it could not handle the semantic meaning of non-English text (Hindi, Bengali, Tamil). Switching to **Gemma Embeddings** provided an immediate performance jump because the model understands semantics across languages.

* **Best Model:** The **Gemma Embeddings + MLP Regressor** was the clear winner, achieving a Cross-Validation RMSE of **1.844** and a Leaderboard Score of **2.668**. This represents a **28.3% improvement** over the baseline.

* **The Power of Target Transformation:** The score distribution was heavily skewed (91% of scores > 9.0). Applying a **Log1p transformation** to the target variable was a crucial hack. It expanded the numerical distance between the rare low scores (0-5), forcing the model to pay more attention to "bad" responses.

* **Feature Engineering Wins:** Explicitly calculating the **Cosine Similarity** between the metric embedding and the text embedding gave the model a direct signal of "relevance," further boosting accuracy.

* **Error Analysis:**
    * **High Scores (8-10):** The model is extremely accurate here, correctly identifying high-quality responses.
    * **Low Scores (0-5):** The model exhibits "regression to the mean," often predicting scores around 5-6 for very bad responses. This is due to the extreme scarcity of negative training examples.

---

## 🏆 Final Recommendation

* **Recommended Model:** **Gemma-300M Embeddings + MLP Regressor**. It effectively bridges the semantic gap for multilingual data and uses a lightweight, regularized neural network (256 -> 128 neurons) to map those embeddings to a continuous score.

* **Actionable Insight:** Future improvements should focus on data augmentation. Generating synthetic "bad" responses (scores 0-5) using LLMs would balance the dataset and likely fix the model's hesitation to predict very low scores.

