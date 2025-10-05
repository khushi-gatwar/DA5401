# DA5401 Assignment 5: Visualizing Data Veracity Challenges in Multi-Label Classification

This repository contains the submission for Assignment 5 of the DA5401 course.

- **Student Name**: Khushi Gatwar
- **Roll Number**: DA25S004

---

## 1. Project Objective

This project aims to explore the inherent challenges of real-world datasets by visualizing a multi-label biological dataset using non-linear dimensionality reduction techniques. The primary objective is to apply **t-SNE** and **Isomap** to the Yeast gene expression dataset to visually identify and analyze data veracity issues such as **noisy labels**, **outliers**, and **hard-to-learn samples**.

The goal is not to build a classifier, but to perform a deep visual inspection to understand the data's underlying structure and the potential difficulties a classification model would face.

---

## 2. Methodology

The analysis follows a systematic pipeline to preprocess the data, generate visualizations, and interpret the results.

### Part A: Preprocessing and Initial Setup
1.  **Data Loading**: The `yeast.arff` dataset was loaded, and the data was separated into a feature matrix `X` (103 features) and a multi-label target matrix `Y` (14 labels).
2.  **Label Simplification**: To create a clear visualization, the 14 labels were simplified into a 4-category coloring scheme. This was achieved by identifying the most frequent single-label class, the two most frequent multi-label combinations, and grouping all other patterns into an "Other" category.
3.  **Scaling**: The feature matrix `X` was standardized using `StandardScaler`. This is a critical step for distance-based algorithms like t-SNE and Isomap to ensure all features contribute equally to the analysis.

### Part B: t-SNE and Veracity Inspection
1.  **t-SNE Implementation**: The t-SNE algorithm was applied to the scaled data. A range of `perplexity` values (5, 10, 20, 30, 40, 50, 60) were tested to find the most informative visualization. A perplexity of 30 was chosen as it provided the best balance between local and global structure.
2.  **Veracity Inspection**: The final t-SNE plot was analyzed to visually identify:
    * **Noisy/Ambiguous Labels**: Points of one color found deep within clusters of another color.
    * **Outliers**: Isolated points and small, distant clusters.
    * **Hard-to-Learn Samples**: Regions where different categories were heavily mixed with no clear separation.
3.  **Quantitative Validation**: In addition to visual inspection, a quantitative analysis using k-Nearest Neighbors was performed on the t-SNE embedding to numerically identify and validate the locations of potentially noisy labels and outliers.

### Part C: Isomap and Manifold Learning
1.  **Isomap Implementation**: The Isomap algorithm was applied to the scaled data to generate a complementary 2D embedding.
2.  **Comparative Analysis**: The Isomap plot was compared to the t-SNE plot. The analysis concluded that t-SNE is better for visualizing local cluster separation, while Isomap is superior for revealing the overall global structure (the data manifold).
3.  **Manifold Discussion**: The Isomap visualization suggested that the data lies on a highly curved and complex manifold, explaining why simple linear classifiers would struggle with this dataset.

---

## 3. Key Findings

The analysis successfully used t-SNE and Isomap to reveal significant data veracity challenges:

* **t-SNE** effectively highlighted distinct clusters, outliers, and areas of high class-overlap, confirming the presence of noisy labels and hard-to-learn samples.
* **Isomap** revealed that the data lies on a complex, non-linear manifold, providing a clear reason why classification on this dataset is a difficult task that would require advanced, non-linear models.
* Together, the visualizations provide a deep understanding of the data's structure and the inherent challenges a machine learning model would face, underscoring the importance of exploratory visualization before model building.

---

## 4. File Structure

For evaluation, the following files are essential and should be present in the submission folder:

```
.
├── Assignment_5.ipynb      # The Jupyter Notebook with all code, analysis, and explanations.
├── yeast.arff              # The dataset required to run the notebook.
└── README.md               # This documentation file.
```

---

## 5. How to Run the Analysis

To reproduce the analysis, please follow these instructions:

1.  **Prerequisites**:
    * Python 3.x
    * Jupyter Notebook or JupyterLab

2.  **Install Required Libraries**:
    The analysis requires several Python libraries. They can be installed via pip:
    ```bash
    pip install pandas numpy matplotlib seaborn scikit-learn scipy
    ```

3.  **Execution Steps**:
    * Ensure the `yeast.arff` file is located in the same directory as the `Assignment_5.ipynb` notebook.
    * Open `Assignment_5.ipynb` in a Jupyter environment.
    * Run the notebook cells sequentially from top to bottom. The notebook is self-contained and will execute the entire pipeline, from data loading to generating the final visualizations and conclusions.

