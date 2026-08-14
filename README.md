# Bank Customer Churn Prediction & Retention Analytics

An end-to-end machine learning pipeline to predict retail bank customer attrition, detect high-risk customer segments, and provide data-driven insights for proactive retention.

---

## 📌 Problem Statement
Customer attrition (churn) directly impacts a bank's recurring revenue and customer lifetime value. The solution builds a supervised binary classification system to predict whether a customer will leave the bank (`Exited = 1`) or stay (`Exited = 0`), leveraging demographic, transactional, and product engagement features across a dataset of 15,000 customer records.
* The goal is to predict the probability of customer attrition (`Exited`: `1` for churn, `0` for retained) for 10,000 test cases and generate an evaluation-ready submission file formatted for the competition output requirements. *
---

## 💼 Business Motivation
* **Cost Efficiency:** Acquiring new banking customers costs 5x to 7x more than retaining existing ones.
* **Targeted Retention:** Identifying high-propensity churners enables relationship managers to intervene with customized offers, fee waivers, or targeted financial advisory services.
* **Revenue Protection:** Pinpointing root causes (e.g., product saturation, inactive membership, regional variations) allows product teams to refine service design.

---

## 📊 Key Metrics & Contributions

### Model Performance (Validation Set — 3,000 records)
Evaluated on a stratified 20% validation split with a tuned **Random Forest Classifier** (`n_estimators=200`, `max_depth=10`):

| Metric | Score / Value |
| :--- | :--- |
| **ROC-AUC Score** | **0.9286** |
| **Overall Accuracy** | **90.0%** |
| **Churn Precision (Class 1)** | **0.82** |
| **Churn Recall (Class 1)** | **0.64** |
| **Churn F1-Score (Class 1)** | **0.72** |
| **Non-Churn F1-Score (Class 0)** | **0.94** |

### Core Technical Contributions
* **Data Leakage & Integrity Fixes:** Discovered that `CustomerId` was non-unique with 1,696 conflicting target labels across multiple records; eliminated `CustomerId`, `Surname`, and `id` to prevent target leakage.
* **Anomaly Treatment:** Capped spurious `Tenure` values (> 10 years) to align with standard banking tenure scales without distorting sample distributions.
* **Production-Grade Preprocessing Pipeline:** Built an automated `ColumnTransformer` pipeline integrating `StandardScaler` for continuous numerical features and `OneHotEncoder(drop='first')` for categorical variables.

---

## 🔍 Key Insights

### 1. Product Saturation Risk
* **3 or 4 Products:** Customers holding 3 or 4 products have an alarming **~95% churn rate**, indicating potential dissatisfaction with multi-product complexity or poor bundle experiences.
* **2 Products:** Customers with exactly 2 products demonstrate the lowest churn rate (**~5%**), representing the optimal engagement threshold.

### 2. Geographic & Demographic Disparities
* **Regional Disparity:** Customers in **Germany** churn at **~41%**, compared to only **15–16%** in France and Spain.
* **Gender Disparity:** **Female customers** exhibit a **28%** churn rate versus **14%** for male customers.
* **Age Skew:** Churning customers skew significantly older (concentrated in the 45–60 age bracket) compared to retained customers (predominantly 30–40).

### 3. Account Activity
* **Inactive Status:** Inactive account holders churn at more than double the rate of active members (**28% vs. 12%**).

---


