# Diabetes Prediction Pipeline 🩺📊

An end-to-end **Machine Learning project** for predicting diabetes using the **Pima Indians Diabetes Dataset**.  
This project focuses on professional-level preprocessing, feature engineering, and building a medically optimized classification model.

---

## Project Overview
The goal of this project is to predict whether a patient has diabetes (`Outcome = 1`) or not (`Outcome = 0`) based on medical attributes.

### Dataset
- **Rows:** 768  
- **Columns:** 9  
- **Target Variable:** `Outcome`
  - `0` → No Diabetes  
  - `1` → Diabetes  

---

# Problem Statement
Early diabetes detection is important in healthcare because delayed diagnosis can lead to severe complications.

This project aims to build a machine learning model that can identify diabetic patients with high recall so fewer actual patients are missed.

---

# Dataset Features
- Pregnancies  
- Glucose  
- BloodPressure  
- SkinThickness  
- Insulin  
- BMI  
- DiabetesPedigreeFunction  
- Age  
- Outcome  

---

# Project Pipeline

## 1. Data Cleaning
### Hidden Missing Values
Some columns had invalid zero values which were medically impossible.

Fixed by:
- Replacing zeros with `NaN`
- Performing proper imputation

Affected columns:
- Glucose  
- BloodPressure  
- SkinThickness  
- Insulin  
- BMI  

---

## 2. Missing Value Handling
Heavy missing values were handled carefully:

- Insulin → **48.7% missing**
- SkinThickness → Missing values handled
- Created missing flags before imputation

Methods used:
- Median imputation
- Missing indicators

---

## 3. Outlier Treatment
### IQR Capping
Applied on:
- Pregnancies  
- BloodPressure  
- BMI  
- DiabetesPedigreeFunction  
- Age  

### Percentile Capping
Used for heavily imputed columns:
- Insulin  
- SkinThickness  

Reason:
IQR failed because median imputation compressed the distribution.

---

## 4. Feature Transformation
Skewed features were normalized using:

- Square Root Transformation  
- Log Transformation (`log1p`)  

This improved feature distributions.

---

## 5. Feature Engineering
Created new features:

- `Metabolic_risk`
- `Insulin_resistance`
- `BMI_category`
- `Glucose_category`
- `Age_risk`
- `Preg_age_risk`
- `high_risk_flag`

### Best engineered features:
🥈 Metabolic_risk → 2nd most important  
🥉 Insulin_resistance → 3rd most important  

---

## 6. Encoding
Used direct numeric labels instead of `OrdinalEncoder`.

Why?
- Simpler
- More reliable
- Avoids category mismatch issues

---

## 7. Train-Test Split
- Train: **80%**
- Test: **20%**
- Used `stratify=y`

---

## 8. Feature Scaling
Used:
```python
RobustScaler

Why?
Because it handles outliers better than StandardScaler.

9. Feature Selection

Started with 17 features

Removed low importance features:

BMI_category
high_risk_flag
Insulin_missing
SkinThickness_missing

Final features:
✅ 13 features retained

Final Model
Logistic Regression (class_weight="balanced")

Chosen because:

Handles class imbalance
Interpretable for healthcare problems
Model Performance
Metric	Score
Accuracy	74.68%
Precision	61.19%
Recall	75.93%
F1 Score	67.77%
Medical Impact

✅ Correctly detects 76% diabetic patients
❌ Misses only 24%

In healthcare, Recall is prioritized because missing diabetic patients is riskier than false alarms.

Key Challenges Solved
Hidden missing values
Heavy missing data
Outlier issues after imputation
Feature engineering mistakes
Encoding problems
Class imbalance
Tech Stack
Python
Pandas
NumPy
Matplotlib
Seaborn
Scikit-learn
Project Structure
├── EDA_Model.ipynb
├── dataset.csv
└── README.md
Future Improvements
Try XGBoost / Random Forest
Hyperparameter tuning
Deploy with Flask/Streamlit
Add explainability using SHAP
Author

Muhammad Saleh
Aspiring Data Scientist | Machine Learning Enthusiast
