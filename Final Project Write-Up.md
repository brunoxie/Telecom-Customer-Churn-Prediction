## I.	Introduction

**Background**

Telcom System (Telco) is a global leader in telecommunication whose operations and management system covers all network segments, including transport, connectivity, and distributed network applications.(1) The main services Telco provides are phone, multiple lines, internet, online security, online backup, device protection, tech support, and streaming TV and movies. Customer retention management is extremely important for telecommunication companies like Telco because the costs of acquiring new customers are much higher than the costs of keeping the remaining customers. The marketing department of Telco proposes to start a marketing campaign to reduce the churn rate and keep their customers. Another data scientist team will conduct cost-benefit analysis to target most profitable customers to campaign on based on our result. Our main task is to predict the customer's behavior of retention based on their features and help identify customers who are most likely to stay and who are not.

**Motivation**

Churn rate is one of the most important metrics for a growing enterprise. It represents the rate at which customers stop doing business with an entity and it is most commonly expressed as the percentage of service subscribers who discontinue their subscriptions within a given time period.(2) Corporations care about churn because it leads to higher Customer Acquisition Costs and loss in profits. Regardless of the strength of marketing strategy and the effectiveness of approach to nurturing leads, every customer costs money to obtain. Acquiring new customers is considerably more expensive than maintaining and upgrading existing customer relationships.(3) Therefore, the more customers churn, the more money must be spent to recoup the loss of business by finding new ones.

To decrease the churn rates, analyzing churn as it occurs is considered to be the most important step.(4) The first step is to understand the directions that churn risk comes from, and that each one represents an opportunity to improve the company and strengthen the customer relationships. The analysis results would benefit the following design and implementation of retention plan. 

With better predictions, Telco could know more about the relationship between customer behaviors and their decision on whether or not to churn, thus proactively taking actions to increase their satisfaction and retain customers in that specific area. Customer relation management and marketing budgets could be more accurately targeted and used. For example, use of emails or direct outreach to customers began to drift away. Finally, users could receive more customized and instant service from Telco instead of taking time and money changing the service provider. We believe that machine learning tools are particularly suited for solving this problem as there is a huge amount of customer behavior data from Telco databases and they can be used as potential predictors to build the model. 

There are many other business application opportunities for our model since not only telecommunication companies care about churn rate and the prediction model could be used by external digital marketing analysis teams to do analysis for other customer-based business. 

## II.	Data and data processing

**Dataset Introduction**

The data was downloaded from IBM Sample Data Sets for customer retention programs. It is based on Telcom that provides home phone and Internet services to customers in California. The data contains information of 7043 customers, and 21 features for each customer, which can be categorized in the following groups:	
*	customers who left or stayed within this month (Churn);
*	services that each customer has signed up for (phone service, multiple lines service, internet, online security, online backup, device protection, tech support, and streaming TV and movies)
*	customer account information (how long they’ve been a customer, contract, payment method, paperless billing, monthly charges, and total charges)
*	demographics information about customers (gender, senior, partners, dependents). 

**Data Exploration**

We started our analysis with a quick look at the distribution of Churn. Among 7043 users, 26.58% of them churned and it is a relatively large proportion, indicating Telco’s  urgent need for customer retention management. This also implies that the data is unbalanced, which might undermine the performance of our models. We will address this issue later in the paper.
 
![alt text](https://github.com/brunoxie/Machine-Learning-Final-Project/blob/main/Picture1.png)

We examined the relationships between different features and Churn and found the ones that might affect the outcome. As it can be seen from the distribution of churn rates for different demographic groups, there is no significant difference in terms of gender, senior users have a higher churn rate, and users who do not have partners and dependents are more likely to churn. 
 
![alt text](https://github.com/brunoxie/Machine-Learning-Final-Project/blob/main/Picture2.png)
 
As for users in different services, those who use Fiber optic have a distinctly much higher churn rate than other users. There is not much difference in terms of phone service, and multiple lines.

![alt text](https://github.com/brunoxie/Machine-Learning-Final-Project/blob/main/Picture3.png)
 
We took a deeper look at the specific services users use, and found that users that don’t have online security, online backup, device protection, technical support, streaming TV or streaming movies have a higher churn rate than those who do have these services. 
 
![alt text](https://github.com/brunoxie/Machine-Learning-Final-Project/blob/main/Picture4.png)

Churn rates also show an interesting relationship with users' payment methods, those who pay monthly and those use paperless billing are more likely to churn and those who pay by electronic check have a significant higher churn rate. 

![alt text](https://github.com/brunoxie/Machine-Learning-Final-Project/blob/main/Picture5.png)

The results below align with our expectation about customer brand loyalty. Those who have a longer time using Telco services have a lower chance to leave their program. Additionally, higher monthly charges may lead to a higher rate of leaving, which leads our research to pricing strategy. In total charges, users that have churned tend to have lower total charges. This is a reasonable result given they have shorter time using Telco.

![alt text](https://github.com/brunoxie/Machine-Learning-Final-Project/blob/main/Picture6.png)

**Data Processing**

Based on the characteristics of our dataset shown above, we implement the following steps to process our data before building the models. First, we dropped the irrelevant variable customer ID. Second, we standardized the continuous variables so that it is comparable between different units. Last, we transformed all the categorical variables, where each variable with more than two categories were spreaded into new variables with dummy values. For example, the payment method variable has four categories: electronic check, mailed check, bank transfer, credit card. We turn each category into its own variable, so users that used electronic check would have the value 1 under the electronic check column, whereas the rest of the columns are listed as 0. Therefore, the final data consists of 22 input variables including demographic information, service subscription and account information. 

## III.	Modelling

**Methodology**

We ran three models including logistic regression, random forest, and boosting. We took 50% of the sample data as our training set, 25% as our validation set, and 25% as our test set. We tested several parameter combinations and tune parameters across the various models and initially evaluated the best for each type of model using the deviance metric defined as the sum over the dataset of −2 log(P(Y = yi | xi)) on validation set predictions. Once we found the best performing model, we retrained it on both the training and validation sets and took a look at prediction accuracy on the test set. We mainly used measures including confusion matrices, ROC, AUC for each model to determine the optimal model in predicting customers churn.

Given that our data is unbalanced, with the ratio of users churned and not churn is 1:3, we might underestimate the class of churn. Therefore, we took an up-sampling technique to create a balanced data and alleviate this issue. We will present our results both for original unbalanced data and balanced data in the following parts of our paper.

**Summary Results**

[alt text](https://github.com/brunoxie/Machine-Learning-Final-Project/blob/main/Picture17.png)

**Unbalanced Data**

* Logistic Regression
In logistic regression, we consider the 3 types of models: regular logistic regression, lasso model with lambda that minimizes cross-validated error, lasso model with lambda in which the error is within 1 se of the minimum. These three models have similar predictive powers in terms of deviance, accuracy, and AUC. In this part, we chose logistic regression as the final model given it has the smallest deviance. We trained the final logistic regression on the data combined with the training set and validation set.

![alt text](https://github.com/brunoxie/Machine-Learning-Final-Project/blob/main/Picture7.png)

* Random Forest 
For random forest models, we ran a parameter search for number of trees, number of variables to possibly split at in each node, and minimal node size to tune the parameters. Based on deviance, we select the optimal parameters where number of trees equals to 1000, number of variables to split equals to 5, and minimal node size equals to 5. 
 
![alt text](https://github.com/brunoxie/Machine-Learning-Final-Project/blob/main/Picture8.png)

* Boosting Trees
For boosting trees, we ran a parameter research for learning rate and maximum depth of trees. We found the optimal model that minimizes deviance has a learning rate of 0.01, maximum depth of trees of 1. Using deviance, accuracy, and ROC, we found the boosting tree model does not perform well in the unbalanced data. We will see the difference when we train the boosting model in balanced data in the next part.
 
![alt text](https://github.com/brunoxie/Machine-Learning-Final-Project/blob/main/Picture9.png)

**Balanced Data**

* Logistic Regression
Similar to what we did before, we trained 3 logistic models, including logistic regression, lasso model with lambda that minimizes cross-validated error, lasso model with lambda in which the error is within 1 se of the minimum. In terms of comparing the three models, We saw that there is no significant difference in the deviance for each model. We chose the logistic regression model as the final model and trained it both in the balanced train data and validation data. In terms of comparing the unbalanced data and balanced one, we found that actually the model’s performance is worse off with deviance increases and accuracy decreases. This might be due to the reason that replicated instances in up-sampling may not reflect the situation consistent with the test set.  
 
![alt text](https://github.com/brunoxie/Machine-Learning-Final-Project/blob/main/Picture10.png)
 
* Random Forest
Here we ran the parameter search again in terms of number of trees, number of variables to possibly split at in each node, and minimal node size. The optimal model with lowest deviance has the number of trees equal to 1000, number of variables equal to 5, and minimal node size equal to 20. For 3 features with most predictive powers, the variable importance plot suggests the same result as before.

![alt text](https://github.com/brunoxie/Machine-Learning-Final-Project/blob/main/Picture11.png)
 
* Boosting Trees
For boosting trees, we ran parameter search and found the optimal learning rate is 0.3 and optimal maximum depth of trees is 5. Note that, compared to unbalanced data, the performance of boosting trees improves substantially. The levels of accuracy and AUC of boosting are similar to the other models now. This suggests that unbalanced data do undermine the accuracy of our models and it’s necessary to transform the data into a balanced one.

![alt text](https://github.com/brunoxie/Machine-Learning-Final-Project/blob/main/Picture12.png)
 
## IV.	Results

We tested the best model for each dataset against their test datasets. We used deviance, confusion matrix, and ROC curve to determine the model with most predictive powers among these three models. For the models trained by unbalanced data, we can see the performance for each is really similar. In the ROC curve, it’s hard to distinguish each. Looking at the specific number of accuracy and AUC, we found the random forest model is the optimal one with a minimum deviance loss of 1446.06, a maximum accuracy rate of 79.86%, and a maximum AUC of 85.50%, which are slightly better than ones of the other models.

![alt text](https://github.com/brunoxie/Machine-Learning-Final-Project/blob/main/Picture13.png)

We further examined the confusion matrix of the selected random forest model for the test set. The result here suggests that if a customer is predicted to churn, there is a 69% chance it will actually leave; if a customer is predicted to stay, there is a 82% chance it will stay. It also means that of customers that churn, 50% are predicted as churn; of customers that stay, 91% are predicted to stay. This reveals a potential problem, that is, while the model is doing generally well in predicting users who stay, it doesn’t predict well in users who churn. This is because the model is built based on unbalanced data. 

![alt text](https://github.com/brunoxie/Machine-Learning-Final-Project/blob/main/Picture14.png)
 
For the model trained in balanced data, we can also see that they have rather similar performances as the ROC curves of each model are almost overlapped. By taking a look at the specific numbers in the evaluations of model’s performances, we found the random forest model is the best model in this data with a minimal deviance of 1486.97, a maximum accuracy rate of 78.84%, a maximum AUC of 84.85%. In comparison to the unbalanced data, we see there is no significant improvement regarding the performance of the optimal model.
 
![alt text](https://github.com/brunoxie/Machine-Learning-Final-Project/blob/main/Picture15.png)

Here we examined the confusion matrix of the best random forest model. The result suggests that if a customer is predicted to churn, there is a 62% chance it will do so. If a customer is predicted to stay, then the chance it stays is 86%. It also suggests that of customers that churn, 62% of them are predicted correctly; of customers that stay, 85% of them are predicted to do so. Unfortunately, there is not much improvement in predicting those who churn by using balanced data.

![alt text](https://github.com/brunoxie/Machine-Learning-Final-Project/blob/main/Picture16.png)

## V.	Conclusion

Our primary objective in this project is to develop a machine learning model that has very strong power in predicting churn rate. We went through models including logistic regression, random forests, boosted trees. By using the model evaluating metrics including deviance, confusion matrix, accuracy, ROC, we selected the best-performing model of random forest in the unbalanced data and balanced data respectively. These models have 80% accuracy overall, which we believed it’s sufficient to achieve our primary goal and help the Telco marketing team to predict and target customers that will leave or stay in the services.

There are also potential improvements that could be made based on our models. One of the toughest issues we are facing in training a machine learning model is that the data is highly unbalanced. We tried to mitigate this issue by using the technique of up-sampling which could create a balanced data. However, our result in the balanced data shows that it does not successfully solve the issue, given the accuracy is low in predicting those who leave. Further improvements focusing on better dealing with class imbalance is highly recommended. A more sophisticated technique may be beneficial such as using weight or synthetic minority sampling technique (SMOTE).

 
## Reference

(1)	Telecom Official Website: https://www.telco.com/about-us/ 
(2)	Investopedia: investopedia.com/terms/c/churnrate.asp  
(3)	Customer churn analysis: One of SaaS’ most important processes: https://www.profitwell.com/customer-churn/analysis 
(4)	Hubspot:  https://blog.hubspot.com/service/what-is-customer-churn 
				


