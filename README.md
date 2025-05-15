# 🛡️ Insurance Claim Prediction Project

## 📌 Objective

This project aims to accurately predict:

1. **ClaimFlag** – Whether an insurance policy will result in a claim (Binary Classification).
2. **ClaimAmount_Binned_Encoded** – The binned category of the claim amount (Multiclass Classification).

These predictions will enable insurers to:
- Minimize losses via targeted interventions.
- Tailor pricing and coverage per customer risk.
- Identify high-risk customers for early risk mitigation.

---

## 📁 Dataset Overview

The dataset contains:
- **Customer Demographics**: Age, Credit Score, ZIP code information.
- **Vehicle Details**: Age of vehicle, number of vehicles, prior accident history.
- **Geographic & Economic Context**: ZIP-level income, home values, population, and coordinates.

---

## ⚙️ Workflow Summary

### 1. **Data Preprocessing**
- Missing value handling.
- Encoding of categorical and ordinal features.
- Feature engineering including interaction terms.

### 2. **Feature Selection**
- **Statistical Hypothesis Testing**:
  - T-test, ANOVA for continuous variables.
  - Chi-Square for discrete and categorical variables.
- **Random Forest Feature Importance**:
  - Features with importance ≥ 0.043 selected.
- **Correlation Analysis**:
  - Spearman correlation for multicollinearity checks.

Final selected features were compiled from all three methods.

---

## 📊 Hypothesis Testing Results Summary

### ClaimFlag (Binary Target)
- Most features showed **significant mean differences** between claim and no-claim groups.
- Indicates strong predictive power for ClaimFlag.

### ClaimAmount_Binned_Encoded (Multiclass Target)
- Fewer features showed significance via ANOVA.
- Indicates ClaimAmount categories are harder to differentiate by traditional means.

### Discrete & Categorical Features
- **NumberOfVehicles** and **State_NY**, **State_TX**, **State_VA**, and **Encoded_CoverageGap** were statistically significant for ClaimFlag.

---

## 📦 Models Used

### 🔹 Baseline Models
- Logistic Regression (with L2 Regularization & Class Weights)
- Decision Tree Classifier
- K-Nearest Neighbors

### 🔸 Advanced Models
- Random Forest Classifier
- XGBoost Classifier

---

## 🧪 Model Evaluation Strategy

- **Cross-Validation**: Stratified 10-Fold CV.
- **Imbalance Handling**: SMOTE (Synthetic Minority Oversampling).
- **Evaluation Metrics**:
  - Accuracy
  - Precision, Recall
  - F1-Score

---

## ✅ Results Overview

| Model                 | Accuracy | F1-Score (Class 1) | Notes                         |
|----------------------|----------|--------------------|-------------------------------|
| Logistic Regression  | ~57%     | ~0.49              | Struggles with class imbalance |
| Decision Tree        | ~93%     | ~0.89              | Strong performance, interpretable |
| KNN                  | ~86%     | ~0.82              | Good balance, sensitive to scaling |
| **Random Forest**     | **97–98%** | **0.96**           | Best performer overall       |
| XGBoost (ClaimFlag)  | ~94%     | ~0.89              | Strong and scalable          |
| XGBoost (ClaimAmount)| ~93%     | varies by class     | Good for multiclass prediction |

---

## 📈 Feature Highlights (Top Predictors)

- `CreditScore_ZIP_AverageIncome_Interaction`
- `Age_CreditScore_Interaction`
- `NumberOfVehicles_NewestVehicleAge_Interaction`
- `ZIP_AverageIncome_Age_Interaction`
- `TimeInsured`, `CreditScore`, `NewestVehicleAge`

---

## 🔍 Key Takeaways

- **Random Forest** outperformed all models in both precision and recall.
- **Interaction terms** added substantial predictive value.
- **SMOTE and stratified k-fold CV** ensured model robustness on imbalanced classes.
- The pipeline is modular, scalable, and ready for production deployment.
