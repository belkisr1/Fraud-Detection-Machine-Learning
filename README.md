🚫 Detecting Financial Fraud at Caishen International Bank
Project Overview

I was tasked by Caishen, a major Zurich-based international bank, to develop a robust machine learning solution to drastically improve their fraud detection capabilities. The bank's explicit three-year strategic goal was to achieve a 99% identification rate of all fraudulent activity within customer accounts. This project focused on building a minimally complex yet highly effective binary classifier using a dataset of one million historical bank transactions.

The Business & Technical Challenge: Class Imbalance

The core technical challenge was extreme class imbalance. The vast majority of transactions were legitimate, meaning a naive model could achieve 99% accuracy by simply classifying everything as non-fraudulent. This, however, results in a 0% sensitivity (Recall), completely failing the business objective.

My objective was to design a comprehensive ML pipeline that:

Achieved high Sensitivity (Recall) to minimize undetected fraud (False Negatives).

Maintained acceptable Precision to minimize false alerts for legitimate customers (False Positives).

My End-to-End Machine Learning Pipeline

1. 🔍 Exploratory Data Analysis (EDA) & Feature Engineering

I began by conducting deep univariate, bivariate, and multivariate analysis to form data-backed hypotheses:

Identifying Fraud Patterns: Analysis of numerical distributions (e.g., Amount, OldBalanceOrg) showed that fraudulent transactions concentrated in very specific, high-value ranges, often involving the full draining of the original account balance.

Transaction Type Analysis: I discovered that fraud was overwhelmingly concentrated in CASH_OUT and TRANSFER transaction types.

Action: I engineered new categorical features (One-Hot Encoding) for transaction type to make this critical distinction usable by the model.

Feature Selection: I identified and removed non-predictive, high-cardinality columns like account names (NameOrig, NameDest) to prevent data leakage and simplify the model.

Engineering New Features: To capture suspicious behaviors, I engineered interaction variables that represent the change in account balances, such as:

Balance Change Orig=OldBalanceOrg−NewBalanceOrig

Balance Change Dest=OldbalanceDest−NewbalanceDest

2. ⚖️ Addressing Class Imbalance

Recognizing that the model would be severely biased toward the majority class, I applied a specific strategy to handle the imbalance:

Strategy: I implemented SMOTE (Synthetic Minority Over-sampling Technique) on the training data to generate synthetic examples of the minority (fraudulent) class. This balances the input features presented to the classifier, allowing it to learn meaningful decision boundaries for fraud.

3. 🧠 Model Selection & Training

Given the binary classification nature and the need for high Recall, I selected and rigorously benchmarked two models:

Model Selected	Rationale
Logistic Regression	Baseline, for interpretability and quick performance assessment.
Gradient Boosting Classifier (XGBoost/LightGBM)	Highly effective for handling imbalanced data and complex non-linear relationships, making it the top candidate for high-stakes fraud detection.
Hyperparameter Tuning: I used Grid Search and Cross-Validation to optimize the key hyperparameters of the selected model, specifically focusing on parameters that influence complexity and generalization (e.g., max_depth, learning_rate, scale_pos_weight).

4. 📈 Performance Evaluation & Impact

The final Gradient Boosting model was selected as the production candidate based on its superior performance on the crucial metrics:

Metric Success: The model achieved a Recall/Sensitivity of 99.1%, successfully exceeding the bank's strategic goal of 99% fraud identification.

Business Trade-off: The model maintained a Precision of 85.5%, meaning only about 14.5% of the alerts generated were false positives, a highly manageable rate for the security team given the severity of the fraud being prevented.

This solution provides Caishen with a production-ready model that directly supports their strategic mandate, transitioning them from a reactive, rule-based flagging system to a proactive, highly accurate machine learning defense.
