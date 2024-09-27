# Telecom Customer Churn Prediction

## Overview

This project aims to predict customer churn for a telecommunications company using machine learning models. The motivation behind this project stems from the fact that customer retention is crucial for reducing acquisition costs and maximizing profits. Our goal is to build models that accurately predict whether a customer will leave (churn) or stay with the company, allowing targeted retention strategies.

## Deliverables
- [Analysis Summary](Analysis%20Summary.md)
- [Presentation](Presentation.pdf)
- [Code](Code.Rmd)

## Context

Telecom companies face high costs for acquiring new customers, making it essential to reduce churn and maintain long-term relationships with existing customers. This project helps Telcom System, a global leader in telecommunications, by providing predictive insights into which customers are likely to churn based on various features such as demographics, services used, and payment methods. The predictions are intended to guide future marketing campaigns and customer retention strategies.

## Data Source

The dataset used for this analysis was sourced from the IBM Sample Data Sets for customer retention programs. It contains 7043 customers and 21 features, including:
- **Churn**: Whether the customer stayed or left.
- **Services**: Phone, internet, online security, etc.
- **Account Information**: Length of tenure, contract type, payment method, etc.
- **Demographics**: Age, gender, family details.

You can access the dataset [here](https://www.ibm.com/communities/analytics/watson-analytics-blog/).

## Methodology

We used the following machine learning models to predict customer churn:
1. **Logistic Regression**: A baseline model that provides simple, interpretable results.
2. **Random Forest**: An ensemble learning method that builds multiple decision trees to improve prediction accuracy.
3. **Boosting**: A method that sequentially improves the model by focusing on misclassified instances in previous models.

The dataset was split into training (50%), validation (25%), and test (25%) sets. We also addressed class imbalance using up-sampling techniques to create balanced datasets for comparison.

### Data Preprocessing
- Dropped irrelevant variables such as customer ID.
- Standardized continuous variables for better comparison.
- Transformed categorical variables into dummy variables.

### Model Evaluation Metrics
We used the following metrics to evaluate model performance:
- **Deviance**: To measure the goodness of fit.
- **Accuracy**: To determine how often the model predicts correctly.
- **ROC/AUC**: To evaluate model performance in distinguishing between churned and retained customers.

## Key Findings

1. **Unbalanced Data**: Random Forest outperformed other models with an AUC of 85.50% and an accuracy of 79.86%. However, it struggled with predicting customers who churned.
   
2. **Balanced Data**: Performance across models was generally consistent, but no significant improvement was seen in predictive power after balancing the data.

3. **Most Important Features**:
    - Users with higher monthly charges or those using paperless billing are more likely to churn.
    - Demographic features like seniority and lack of dependents increase churn likelihood.
    - Users with additional services such as online security and backup tend to stay longer.

## Conclusion

Our best model reachese an accuracy of 80%+. Additionally, our analysis shows that customer churn prediction can be effectively tackled with machine learning models like Random Forest and Boosting. While balancing the dataset did not significantly improve predictive accuracy, the insights provided by the model enable better targeting for marketing and retention strategies. Focusing on key features like monthly charges and service usage will allow the company to take proactive steps to retain high-risk customers. 
