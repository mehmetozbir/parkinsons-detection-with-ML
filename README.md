# 🧠 Parkinson’s Disease Prediction Using Voice Biometrics

This project aims to **predict the severity of Parkinson’s disease** using non-invasive voice biometrics and machine learning. The model estimates `motor_UPDRS` and `total_UPDRS` scores based on biomedical voice features from diagnosed individuals.

---

## 🎯 Project Objective

Parkinson’s disease is a progressive neurological disorder that affects motor and non-motor functions. Traditional diagnosis often occurs late and involves costly and invasive methods.  
Our goal is to use **machine learning** to provide an **early, low-cost, and real-time prediction** method using patients' voice recordings.

## 💡 What This Project Does (Detailed Explanation)

Parkinson’s disease is a progressive neurological disorder that affects motor and non-motor abilities. One of the major challenges is that symptoms become noticeable only in advanced stages, making early detection difficult with conventional methods like brain imaging and clinical observation.

This project tackles that problem by offering a **non-invasive and rapid screening method**:  
➡️ It uses **biomedical voice features** (such as jitter, shimmer, and noise ratios) extracted from patients' speech recordings.  
➡️ These features are analyzed by a **machine learning model** — specifically a Random Forest Regressor — to predict the severity of Parkinson’s symptoms.  
➡️ The output is two clinically recognized scores:
- `motor_UPDRS`: severity of motor symptoms (e.g., tremor, rigidity)
- `total_UPDRS`: overall disease severity including motor and non-motor symptoms

In short:

> **A patient's voice is recorded → features are extracted → the model predicts how severe the patient’s Parkinson’s symptoms are.**

This can support neurologists in:
- Making **earlier diagnoses**
- Tracking **disease progression**
- Reducing the need for invasive or expensive procedures

This technology could evolve into a tool where patients simply speak into a microphone and receive a clinical severity assessment in real time.

---

---

## 📊 Dataset Overview

- **Source**: [UCI Machine Learning Repository – Parkinson’s Telemonitoring Dataset](https://archive.ics.uci.edu/dataset/189/parkinsons+telemonitoring)
- **Format**: CSV (tabular data)
- **Samples**: 5,875 voice recordings from 42 patients
- **Features**: 16 biomedical voice features + demographic and time info
- **Targets**: 
  - `motor_UPDRS` (motor-related severity)
  - `total_UPDRS` (overall symptom severity)

> ⚠️ Due to licensing, the dataset is not included in this repository.  
> Download and place the following files in the root project folder:
> - `parkinsons_updrs.data.csv`
> - `parkinsons_updrs.names.csv`

---

## 🧹 Data Processing

- No missing values
- 80/20 train-test split by patient (to avoid data leakage)
- All features normalized using Min-Max scaling
- Gender encoded as binary
- No duplicate records found

---

## 🧠 Models Used

We tested multiple regression models using 5-fold cross-validation:

| Model                   | Motor R² | Total R² |
|------------------------|----------|----------|
| Linear Regression       | 0.74     | 0.77     |
| Support Vector Regressor| 0.80     | 0.83     |
| Random Forest Regressor | **0.88** | **0.91** |
| Gradient Boosting       | 0.86     | 0.89     |
| XGBoost                 | 0.87     | 0.90     |
| KNN                     | 0.78     | 0.81     |

➡️ **Random Forest Regressor** was the best performing model and selected for deployment.

---

## 🧪 Hyperparameter Tuning (GridSearchCV)

- `n_estimators = 200`
- `max_depth = 20`
- `min_samples_split = 2`

---

## 📈 Final Test Performance

- **Motor UPDRS**:  
  - R²: 0.88  
  - MAE: 2.37  
  - RMSE: 3.12  

- **Total UPDRS**:  
  - R²: 0.91  
  - MAE: 2.01  
  - RMSE: 2.88  

---

## 🔍 Explainability with XAI

To ensure model transparency and clinical trust, the following Explainable AI methods were used:

- **SHAP (SHapley values)** for local/global feature impact
- **Random Forest Feature Importance**
- **Partial Dependence Plots (PDP)**
- **Residual Plots & Error Analysis**

**Top features** influencing predictions:
- Jitter (local, absolute, RAP)
- Shimmer
- NHR / HNR
- DFA (voice complexity)

### Case Studies:
- Accurate case: SHAP highlighted strong jitter + shimmer
- Error case: Model missed jitter; caused underprediction

### Subgroup Analysis:
- Gender-based SHAP analysis showed minor differences in feature impact
- No bias detected, but further clinical feature integration is recommended

---

## ⚠️ Limitations & Next Steps

- SHAP is computationally expensive and assumes feature independence
- PDPs may mislead when features are highly correlated
- Consider LSTM or CNN for time-series or audio-signal modeling
- Add more clinical features like medication state or fatigue level

---

## 📦 How to Run

1. **Clone the repository**:
```bash
git clone https://github.com/mehmetozbir/parkinsons-detection-with-ML.git
cd parkinsons-detection-with-ML
