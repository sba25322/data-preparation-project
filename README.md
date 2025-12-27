# data-preparation-project
# Student Data Analysis and PCA Implementation

## Introduction
This project analyzes the `student_data.csv` dataset to identify factors influencing the target variable: whether a student **enrolled, dropped out, or graduated successfully**.  

The study involves:  
- Data exploration and cleaning  
- Exploratory Data Analysis (EDA)  
- Dimensionality reduction using **Principal Component Analysis (PCA)**  
- Evaluation of PCA's impact on model performance  

The goal is to investigate if the dataset suffers from the **curse of dimensionality** and whether PCA improves training performance and reduces overfitting.

---

## Dataset Overview
- **Categorical features:** 6  
- **Numerical features:** 32 (12 float, 20 integer)  
- **Rows and columns after cleaning:** 4411 rows, 37 columns  

**Notes:**  
- Categorical variables require encoding before analysis.  
- Numerical features are suitable for scaling, PCA, and model training.

---

## Data Preparation and Cleaning

### Missing Values Handling
- Investigated null values using unique values in each column.  
- Null references included: `"Unknown"`, `"NA"`, `"Na"`, `"?"`.  
- Removed rows with missing values using `dropna()`.  
- Result: **4411 rows remain**, 13 rows removed.  

### Target Feature Cleaning
- Original target had inconsistent labels (`drop`, `grad`, different capitalizations).  
- Standardized target to: `enrolled`, `dropout`, `graduate`.

---

## Exploratory Data Analysis (EDA)
- Visualizations for **Target distribution**, **Age**, and **Marital Status**.  
- Explored relationships between features and the target.  

---

## Scaling Numeric Features
- Standardized numeric features to prevent bias in PCA due to differing scales.  
- Used `StandardScaler()` on the entire dataset.  

> **Note:** Scaling was applied before separating categorical and numerical features to test PCA performance on fully numeric representations.

---

## PCA Analysis

### Overview
- PCA reduces dimensionality while retaining variance (Abdi & Williams, 2010).  
- Helps mitigate the **curse of dimensionality** by reducing noisy features, lowering computational cost, and improving model performance.

### First PCA Implementation
- Input: 36 features (all scaled numerically)  
- Output: Reduced to 33 features  
- Observation: Minimal reduction due to numeric representation of categorical data.

### Second PCA Implementation
- Separated **categorical** and **numeric** features  
- Encoded categorical features using `OneHotEncoder()`  
- Features increased to **260 distinct features** after encoding  
- PCA reduced features to **103**, achieving significant dimensionality reduction (~1.5× reduction)

### PCA Visualization
- Graph shows the relationship between **number of features** and **explained variance**.  
- Retained features capture sufficient variance while reducing noise.

---

## Curse of Dimensionality
- High-dimensional data increases sparsity, model overfitting, and training cost.  
- PCA mitigates these issues by reducing features while preserving variance.

---

## Model Evaluation: Original vs PCA Features

Three models were trained on both the **original dataset** and **PCA-reduced dataset**:  

| Model | Original Dataset | PCA Features | Observation |
|-------|----------------|--------------|-------------|
| Logistic Regression | Accuracy / F1 similar | Accuracy / F1 similar | PCA maintains performance |
| Random Forest | Slightly lower F1, +1% accuracy | Slightly lower F1, +1% accuracy | Minor change |
| SVC | Accuracy / F1 similar | Accuracy / F1 similar | PCA preserves model performance |

**Conclusion:**  
- PCA did **not significantly increase accuracy** but reduced training cost and noise.  
- Proper preprocessing (scaling numeric, encoding categorical) is essential for effective PCA.

---

## Key Takeaways
- Correct data preprocessing is critical for PCA effectiveness.  
- PCA reduces feature dimensionality, helping mitigate computational cost and noisy features.  
- For this dataset, PCA maintained performance across multiple models while reducing feature space.

---

## References
1. Abdi, H. & Williams, L.J. (2010). *Principal component analysis*. Wiley Interdisciplinary Reviews: Computational Statistics, 2(4), 433–459. https://doi.org/10.1002/wics.101  
2. Poggio, T., Mhaskar, H., Rosasco, L., Miranda, B., & Liao, Q. (2017). *Why and when can deep-but not shallow-networks avoid the curse of dimensionality: A review*. Int. J. of Automation and Computing, 14(5), 503–519. https://doi.org/10.1007/s11633-017-1054-2  
3. Domínguez-Almendros, S., Benítez-Parejo, N., & Gonzalez-Ramirez, A.R. (2011). *Logistic regression models*. Allergologia et Immunopathologia, 39(5), 295–305. https://doi.org/10.1016/j.aller.2011.05.002
