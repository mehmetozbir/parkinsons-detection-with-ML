
# 🧠 Parkinson's Disease Prediction using Voice Biometrics

This project aims to **predict the severity of Parkinson's disease** based on voice measurements using machine learning and explainable AI methods.

## 🎯 Objective

To build a predictive model that estimates:
- `motor_UPDRS` score
- `total_UPDRS` score

...using biomedical voice features collected from patients.

## 📊 Dataset

- **Source**: Parkinson's Telemonitoring dataset
- **Samples**: 5,875 voice recordings from 42 patients
- **Features**: 16 biomedical voice measurements (e.g., jitter, shimmer, HNR)

## 🧰 Tools & Libraries

- Python
- Scikit-learn
- Pandas, NumPy
- SHAP (Explainable AI)
- Matplotlib / Seaborn

## 🤖 Model

- **Random Forest Regressor**
- Evaluation metrics: MAE, RMSE, R²
- Feature importance via **SHAP values**

## 🧪 How to Run This Project

Follow the steps below to set up and run this project on your local machine.

---

### 📥 1. Clone the Repository

Download the project to your computer using Git:

```bash
git clone https://github.com/mehmetozbir/parkinsons-detection-with-ML.git
cd parkinsons-detection-with-ML
