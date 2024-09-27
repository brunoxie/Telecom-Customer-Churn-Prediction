# Telecom Customer Churn Prediction

## Overview

This project aims to predict customer churn for a telecommunications company using machine learning models. The motivation behind this project stems from the fact that customer retention is crucial for reducing acquisition costs and maximizing profits. Our goal is to build models that accurately predict whether a customer will leave (churn) or stay with the company, allowing targeted retention strategies.

## Data Source

The dataset used for this analysis was sourced from the IBM Sample Data Sets for customer retention programs. It contains 7043 customers and 21 features, including:
- **Churn**: Whether the customer stayed or left.
- **Services**: Phone, internet, online security, etc.
- **Account Information**: Length of tenure, contract type, payment method, etc.
- **Demographics**: Age, gender, family details.

You can access the dataset [here](data).

## Methodology

We used the following machine learning models to predict customer churn:
1. **Logistic Regression**: A baseline model that provides simple, interpretable results.
2. **Random Forest**: An ensemble learning method that builds multiple decision trees to improve prediction accuracy.
3. **Boosting**: A method that sequentially improves the model by focusing on misclassified instances in previous models.

The dataset was split into training (50%), validation (25%), and test (25%) sets. We also addressed class imbalance using up-sampling techniques to create balanced datasets for comparison.

We used the following metrics to evaluate model performance:
- **Deviance**: To measure the goodness of fit.
- **Accuracy**: To determine how often the model predicts correctly.
- **ROC/AUC**: To evaluate model performance in distinguishing between churned and retained customers.

## Code
You can find the code written in R [here](Code.Rmd)

## Deliverables
The final deliverables of this project include an [Analysis Summary](Analysis%20Summary.md) and a [Slide](Slide.pdf). The analysis summary details the approaches and the results. And the slide gives a high-level presentation on the analysis.
