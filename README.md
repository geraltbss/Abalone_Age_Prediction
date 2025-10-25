# Abalone Age Prediction    

This repository contains the descriptive and advanced analytical work conducted, focusing on predicting the **age of abalones** using physical measurements and machine learning techniques.

---

## Project Overview  

Abalone is a valuable marine mollusk whose **age** is traditionally determined by counting the number of **rings** in its shell - a method that is both **time-consuming** and **invasive**.  
This project aims to develop efficient, non-invasive models to predict abalone age (number of rings) based on measurable physical attributes using **statistical** and **machine learning techniques**.

---

## Objectives  
- Conduct descriptive and inferential analysis on the abalone dataset.  
- Identify key physical features correlated with abalone age.  
- Build and compare predictive models for ring count (age).  
- Evaluate and select the most accurate and efficient model.  

---

## Dataset Details  
**Source:** UCI Machine Learning Repository  
**Records:** 4,177  
**Variables:** 9  

| Variable | Description |
|-----------|--------------|
| Sex | M (Male), F (Female), I (Infant) |
| Length | Longest shell measurement (mm) |
| Diameter | Measurement perpendicular to length (mm) |
| Height | Height with meat in shell (mm) |
| Whole weight | Whole abalone weight (grams) |
| Shucked weight | Weight of meat (grams) |
| Viscera weight | Gut weight after bleeding (grams) |
| Shell weight | After drying (grams) |
| Rings | Number of shell rings (Age indicator) |

*Age is approximately calculated as: `Rings + 1.5` years.*

---

## Data Preprocessing  
- Removed invalid or erroneous records (e.g., height = 0 or >1).  
- Standardized or normalized features depending on model requirements:  
  - **Normalization:** for MLR and ANN.  
  - **Standardization:** for PLS and Random Forest.  
- Encoded categorical variable **Sex** numerically.  

---

## Descriptive Analysis  

- **Rings Distribution:** Positively skewed, with most abalones being younger (fewer rings).  
- **Gender Effect:** No strong difference between male and female; infants have fewer rings.  
- **Correlation:**  
  - Length, diameter, and height are strongly correlated.  
  - Multicollinearity detected among weight-related features.  
- **Kruskal–Wallis Test:** Significant differences in ring distribution across sexes.  

---

## Advanced Statistical Techniques  

### **Partial Least Squares (PLS) Analysis**
- 1st component explains **73.68%** of total variance.  
- Indicated **multicollinearity** among predictor variables.  
- No strong linear relationship between predictors and target — suggesting non-linear modeling may improve performance.

### **Cluster Analysis**
- Performed using **K-Prototypes** to handle both categorical and numeric features.  
- Optimal number of clusters: **2**.  
  - Cluster 1: Predominantly **male/female** abalones (larger and older).  
  - Cluster 2: Predominantly **infant** abalones (smaller and younger).  
- Mean silhouette score: **0.47** → weak clustering tendency.

---

## Predictive Modeling  

### **A. Multiple Linear Regression (MLR)**
- Baseline model: Predicting `Rings` using all physical features.  
- **Training RMSE:** 2.23 | **Test RMSE:** 2.10  
- **MAPE:** 15.7% | **Correlation:** 0.73  
- Some model assumptions (normality, independence, constant variance) violated.  
- **Multicollinearity** present — `Whole weight` VIF ≈ 107.  

---

### **B. Regularization Techniques**

| Model | Train RMSE | Test RMSE | R² | MAPE | Notes |
|--------|-------------|-----------|----|------|-------|
| Ridge | 2.21 | 2.23 | 0.54 | 16.3% | Best among linear models |
| LASSO | 3.21 | 3.29 | < 0 | 27.3% | Poor fit |
| Elastic Net | 3.21 | 3.29 | < 0 | 27.3% | Poor fit |

> Ridge regression produced the most stable and accurate results among linear models, though predictive power remained limited.

---

### **C. Random Forest Regression**
- Applied **Grid Search CV** to tune parameters (`n_estimators`, `max_depth`, etc.).  
- **Train RMSE:** 1.74 | **Test RMSE:** 2.03  
- **Train R²:** 0.715 | **Test R²:** 0.559  
- **MAPE:** 14.4%  
> Random Forest delivered the **best performance** among all regression-based models.

---

### **D. Artificial Neural Network (ANN)**

- Built using both **Python** (TensorFlow) and **JNN Tool**.  
- **Architecture:**  
  - Input Layer (8 nodes)  
  - Hidden Layers: [5, 1, 7 nodes]  
  - Output Layer (1 node)  
- **Hyperparameters:**  
  - Learning Rate = 0.06 | Momentum = 0.08  
  - Epochs = 500 | Batch normalization applied  
- **Results:**  
  - Training RMSE = 2.18 | Testing RMSE = 2.22  
  - Training R² = 0.54 | Testing R² = 0.51  
  - MAPE = 15% | Accuracy ≈ **85%**

> The ANN achieved a high predictive accuracy, demonstrating its ability to capture complex nonlinear patterns in abalone growth.

---

## Model Comparison Summary  

| Model | RMSE | R² | MAPE | Accuracy | Remarks |
|--------|------|----|------|-----------|----------|
| MLR | 2.10 | 0.54 | 15.78% | 73% | Baseline |
| Ridge | 2.23 | 0.54 | 16.31% | 77% | Best regularized |
| LASSO | 3.29 | - | 27.34% | - | Poor |
| Elastic Net | 3.29 | - | 27.34% | - | Poor |
| Random Forest | **2.04** | **0.56** | **14.4%** | **76%** | Best overall |
| ANN | 2.22 | 0.51 | 15% | **85%** | Best nonlinear |

---

## Tools & Technologies  
- **Languages:** Python, R  
- **Libraries:**  
  - `pandas`, `numpy`, `scikit-learn`, `matplotlib`, `seaborn`, `tensorflow`, `keras`  
  - `factoextra`, `cluster`, `caret` (for R analysis)  
- **Techniques Used:**  
  - Descriptive Statistics & Visualization  
  - PLS & Cluster Analysis  
  - Regression & Regularization  
  - Ensemble Learning (Random Forest)  
  - Neural Networks (ANN)  

---
**## Key Insights  
- **Physical dimensions** (length, diameter, height) are strong age indicators.  
- **Random Forest and ANN** outperform linear models due to non-linear patterns.  
- Predicting abalone age through measurable features can **save time and preserve specimens**.  
- Future research could integrate **environmental and regional variables** to enhance model accuracy.

---

## References & Resources  
- Dataset: [UCI Machine Learning Repository – Abalone Dataset](https://archive.ics.uci.edu/ml/datasets/abalone)  
