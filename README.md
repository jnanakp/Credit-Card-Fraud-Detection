# Credit Card Fraud Detection 

📊 **Project Overview**

This project applies advanced machine learning techniques to detect fraudulent activity in credit card transactions. Using a real-world dataset of 97,852 transactions from 2010, we built a high-performing fraud detection system capable of identifying high-risk activity with strong generalization and business impact. The goal was to maximize fraud savings while minimizing false positive costs through robust modeling and financial evaluation.

---

🧠 **Key Objectives**

- Detect fraudulent credit card transactions with high precision.  
- Engineer meaningful features to capture behavioral, temporal, and geographic fraud signals.  
- Handle severe class imbalance with specialized techniques.  
- Recommend a fraud score cutoff that optimizes financial outcomes.

---

🗃️ **Dataset Description**

- **Type**: Real credit card transaction records  
- **Size**: 97,852 transactions  
- **Features**: Card number, merchant info, zip/state, date, amount, fraud indicator  
- **Time Frame**: January 1, 2010 – December 31, 2010  
- **Fraud Proportion**: ~2.1% fraudulent transactions  
- **Goal**: Classify whether a transaction is fraudulent

---

🧹 **Data Cleaning**

Key data preparation steps included:
- Removed non-purchase transactions and excluded business-related merchants.  
- Capped extreme transaction amounts over $3 million.  
- Repaired missing values in `merchnum`, `merch zip`, and `merch state` using hierarchical logic.  
- Imputed values based on merchant description, ZIP code, and other related fields.

---

🛠️ **Feature Engineering**

We created over **2,600 variables** including:
- **Velocity Features**: Frequency of card/merchant activity over rolling time windows (1, 3, 7, 14, 30, 60 days).  
- **Geographic Features**: Merchant state, zip, and foreign zip flag.  
- **Combination Features**: Card × merchant, merchant × state, and advanced multi-attribute combinations.  
- **Temporal Features**: Day of week, time-since-last transaction, binned amount categories.  
- **Target Encoded Features**: Based on fraud rates across zip, state, and day-of-week.

---

🔍 **Feature Selection**

Applied a two-step process:
- **Filtering**: Top features selected using the Kolmogorov–Smirnov (KS) statistic.  
- **Wrapping**: Forward and backward selection using LightGBM and Random Forest to finalize impactful variables.

Final configuration:
- `num_filter = 200`  
- `num_wrapper = 20`  
- Reduced feature set preserved high predictive power with improved model interpretability.

---

🤖 **Models Explored**

| Model              | Notes                                         |
|--------------------|-----------------------------------------------|
| Logistic Regression| Baseline model, fast but limited complexity   |
| Decision Tree      | Interpretable, risk of overfitting            |
| Random Forest      | Strong baseline, robust but noisy at times    |
| LightGBM           | ⭐ Best performance overall                    |
| XGBoost            | Powerful but sensitive to hyperparams         |
| CatBoost           | Strong with categorical features              |
| Neural Network     | High variance, moderate generalization        |

---

🏆 **Final Model: LightGBM**

**Why LightGBM?**  
- Excellent performance across all datasets  
- Fast training and prediction time  
- Tunable and scalable for large datasets

**Results (FDR @ Top 3%)**:  
- **Train**: 82.38%  
- **Test**: 78.13%  
- **Out-of-Time (OOT)**: **87.54%**

**Estimated Annual Fraud Savings**: ~$47 million

**Key Hyperparameters**:
- `learning_rate`: 0.01  
- `max_depth`: 6  
- `n_estimators`: 200  
- `subsample`: 0.7  
- `min_child_samples`: 70  

---

💰 **Financial Analysis**

We evaluated model cutoffs using three financial curves:
- **Fraud Savings Curve**: Cumulative savings from catching fraud.  
- **False Positive Loss Curve**: Cost of incorrectly flagged legitimate transactions.  
- **Net Savings Curve**: Combines fraud savings and losses to find optimal cutoff.

**📌 Recommended Cutoff**: Top 4% of predicted scores  
- Balances fraud recovery and operational costs  
- Maximizes **net savings while controlling false positives**

---

📈 **Results Summary**

| Dataset   | FDR (Top 3%) | Notes                       |
|-----------|--------------|-----------------------------|
| Train     | 82.38%       | Strong fit                  |
| Test      | 78.13%       | Minimal overfitting         |
| OOT       | 87.54%       | Excellent generalization    |


