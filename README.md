# kickstarter-success-prediction
Machine learning pipeline predicting Kickstarter campaign success using Day-Zero features.

# Kickstarter Campaign Success Prediction 🚀

This repository contains a machine learning pipeline designed to predict the success of Kickstarter campaigns based exclusively on 'Day-Zero' (launch day) features. The project approaches the problem as a binary classification task.

## 📌 Project Overview
Entrepreneurs often set unrealistic funding goals. This project aims to provide a data-driven decision support system that evaluates a project's likelihood of success before the campaign goes live.

* **Problem Type:** Binary Classification (1 = Successful, 0 = Failed)
* **Dataset:** [Kickstarter Projects on Kaggle](https://www.kaggle.com/datasets/kemical/kickstarter-projects) (300,000+ records)
* **Key Features:** `main_category`, `country`, `goal` (Budget), `duration_days` (calculated from launch and deadline)

## 🛠️ Engineering Highlights & Data Leakage Prevention
To ensure the model performs realistically in a real-world scenario, **Data Leakage** was strictly prevented. Features that accumulate during the campaign lifecycle, such as `pledged` (collected money) and `backers`, were permanently dropped before training. The model relies solely on initial inputs.

**Preprocessing Steps:**
* **Feature Engineering:** Created `duration_days` metric from datetime objects.
* **Data Cleaning:** Isolated and removed invalid strings forced into numeric columns using `pd.to_numeric` with coercion.
* **Encoding & Scaling:** Applied One-Hot Encoding to categorical data and `StandardScaler` to continuous numerical data.

## 🚀 Models & Performance
Three different algorithms were trained and evaluated using 5-Fold Cross Validation. Hyperparameter tuning was applied to control variance and prevent overfitting.

| Model | Accuracy |
| :--- | :--- |
| Logistic Regression (Baseline) | 64.93% |
| Random Forest | 63.56% |
| **XGBoost (Best Model)** | **66.68%** |

### ROC Curve & AUC
*(AUC = 0.71 for XGBoost, demonstrating the highest capability in distinguishing between successful and failed projects.)*

![ROC Curve](https://github.com/senaGurok/kickstarter-success-prediction/blob/main/images/roc_curve.png)

### Confusion Matrix (XGBoost)
The model shows high precision in identifying projects destined to fail (True Negatives), providing a reliable risk-averse metric.

![Confusion Matrix](https://github.com/senaGurok/kickstarter-success-prediction/blob/main/images/confusion_matrix.png)

## 💡 Key Business Insight (Feature Importance)
The analysis revealed a counter-intuitive insight regarding campaign success. As seen in the Feature Importance chart below, the amount of money requested (`goal`) is not the primary driver of success. 

Instead, community-driven and artistic categories such as **Theater, Music, and Dance** hold the highest predictive weight. These categories rely on strong, pre-existing fan bases and organic community support, which mathematically outweighs the impact of the budget target itself.

![Feature Importance](https://github.com/senaGurok/kickstarter-success-prediction/blob/main/images/feature_importance.png)
