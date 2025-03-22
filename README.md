# 🌍 Life Expectancy Prediction Using Machine Learning

**This Project is part of a MATH 444 class at CSUN - Project 2**

This project analyzes global life expectancy data using various statistical and machine learning techniques. Our goal is to identify key socio-economic and health factors influencing life expectancy and build accurate models to predict it.

---

## 👨‍👩‍👧‍👦 Team Members

- Brandon Ismalej  
- Jittapatana (Patrick) Prayoonpruk  
- Mishek Sambahangphe  

---

## 📊 Dataset Overview

- **Source:** World Health Organization (WHO) - Global Health Observatory (GHO)
- **Period:** 2000–2015  
- **Countries:** 193  
- **Size:** 2938 rows, 22 columns  
- **Target Variable:** Life Expectancy (continuous)

### 🔍 Features Include:

- **Health Indicators:** BMI, HIV/AIDS, Immunization rates  
- **Socioeconomic Indicators:** GDP, Population, Schooling, Income composition of resources  
- **Demographic Data:** Adult Mortality, Infant Deaths, Under-five Deaths  

---

## ⚙️ Preprocessing

- **Training Set:** Data from 2014  
- **Testing Set:** Data from 2015  
- **Missing Value Handling:**  
  - Imputed using `missForest` (non-parametric Random Forest-based method)  
  - 10 iterations, 100 trees per forest  

- **Post-Imputation Size:**  
  - Training: 183×22  
  - Testing: 183×22

---

## 📐 Feature Engineering

### 📌 Stepwise Feature Selection (using AIC/BIC)

Selected Predictors:
- Income Composition of Resources  
- HIV/AIDS  
- Adult Mortality  
- Total Expenditure  

### 🔄 Box-Cox Transformation
- Applied to the **target variable** to stabilize variance  
- Optimal λ (lambda): 1.0303  

---

## 🧪 Model Evaluation

| Model                                | Adjusted R² | RMSE     | Key Features                                 |
|-------------------------------------|-------------|----------|----------------------------------------------|
| Linear Regression (Baseline)        | 0.796       | —        | Adult Mortality, HIV/AIDS, Income Composition |
| Stepwise Regression                 | 0.8666      | —        | + Total Expenditure                           |
| Box-Cox Transformed Regression      | 0.8664      | 2.99     | Same as stepwise                              |
| Generalized Least Squares (GLS)     | —           | **2.63** | Improved residual handling                    |
| CatBoost with PCA                   | 0.8849      | 2.75     | Dimensionality reduction (90% variance kept)  |
| **CatBoost without PCA**            | **—**       | **1.92** | Best performance overall                      |

---

## 🤖 Machine Learning: CatBoost

- **Algorithm:** Gradient Boosting (handles categorical & continuous)
- **Feature Selection:** All-Subset Regression  
- **PCA:** Used in one version to reduce dimensionality  
- **Performance:** CatBoost without PCA achieved the **lowest RMSE and highest R²** across all models

---

## 🧠 Principal Component Analysis (PCA)

- Applied before CatBoost (in one model)  
- Retained 90% of original variance  
- However, the non-PCA CatBoost model outperformed it

---

## 🏁 Conclusion

- Generalized Least Squares was the best linear model
- **CatBoost without PCA** delivered the **most accurate** life expectancy predictions
- PCA, while helpful for dimensionality reduction, did not enhance CatBoost performance in this case

---

## 📁 Project Files

- `life_expectancy_model.ipynb`: Jupyter notebook with all code and analysis
- `data/`: Cleaned and imputed dataset
- `models/`: Trained model outputs and diagnostics
- `plots/`: Visualizations for EDA and model diagnostics

---

## 💡 Future Work

- Include more recent data post-2015  
- Experiment with ensemble stacking and deep learning methods  
- Explore regional and continent-based subgroup modeling  
- Add interpretable ML tools (e.g., SHAP, LIME) for feature impact explanations

---
