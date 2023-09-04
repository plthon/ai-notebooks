# Predict Churning Customers

A credit analyst was asked to lay the landscape of the problem of customer attrition. They want to analyze the data to 
find out the reason behind this and leverage the same to predict customers who are likely to drop off.

## Data Description

Dataset: Prediction High Turnover.xlsx

Now, this dataset consists of about 10,000 customers mentioning their age, salary, marital_status, credit card limit, 
credit card category, etc. There are nearly 18 features.

The column and its description to aid analysis:

|              Column Name | Description                                                                                                                      |
|-------------------------:|----------------------------------------------------------------------------------------------------------------------------------|
|                CLIENTNUM | Client number. Unique identifier for the customer holding the account                                                            |
|           Attrition_Flag | Internal event (customer activity) variable - if the account is closed then 1 else 0                                             |
|             Customer_Age | Demographic variable - Customer's Age in Years                                                                                   |
|                   Gender | Demographic variable - M=Male, F=Female                                                                                          |
|          Dependent_count | Demographic variable - Number of dependents                                                                                      |
|          Education_Level | Demographic variable - Educational Qualification of the account holder (example: high school, college graduate, etc.)            |
|           Marital_Status | Demographic variable - Married, Single, Divorced, Unknown                                                                        |
|          Income_Category | Demographic variable - Annual Income Category of the account holder (<  40K, 40K - 60K,  60K− 80K,  80K− 120K, > $120K, Unknown) |
|            Card_Category | Product Variable - Type of Card (Blue, Silver, Gold, Platinum)                                                                   |
|           Months_on_book | Period of relationship with bank                                                                                                 |
| Total_Relationship_Count | Total no. of products held by the customer                                                                                       |
|   Months_Inactive_12_mon | No. of months inactive in the last 12 months                                                                                     |
|    Contacts_Count_12_mon | No. of Contacts in the last 12 months                                                                                            |
|             Credit_Limit | Credit Limit on the Credit Card                                                                                                  |
|      Total_Revolving_Bal | Total Revolving Balance on the Credit Card                                                                                       |
|          Avg_Open_To_Buy | Open to Buy Credit Line (Average of last 12 months)                                                                              |
|     Total_Amt_Chng_Q4_Q1 | Change in Transaction Amount (Q4 over Q1)                                                                                        |
|          Total_Trans_Amt | Total Transaction Amount (Last 12 months)                                                                                        |
|           Total_Trans_Ct | Total Transaction Count (Last 12 months)                                                                                         |
|      Total_Ct_Chng_Q4_Q1 | Change in Transaction Count (Q4 over Q1)                                                                                         |
|    Avg_Utilization_Ratio | Average Card Utilization Ratio                                                                                                   |

## Solution
Please find the solution in the notebook `Predict Churning Customers.ipynb` in the same directory.

## Results and Discussion

### Understanding Customer Churn Factors

#### Exploratory Data Analysis (EDA)
An initial exploration revealed that around 16% of customers have churned. The EDA process involved plotting 
distributions of numerical features against the target variable. Notable observations include:
- Customers with fewer total products held tend to exhibit higher attrition rates.
- Attrited customers often have zero revolving credit card balance and fewer transactions.
- Low card utilization ratios are associated with attrited customers.

#### Feature Correlation
A correlation analysis indicated weak relationships between numerical features and customer churn. Five features, 
including Contacts_Counts_12_mon, Months_Inactive_12_mon, Dependent_count, Customer_Age, and Months_on_book, showed the 
most prominent, yet still weak, correlations.

#### Categorical Features
Exploring categorical features revealed that while most categories showed no significant difference in churn 
proportions, customers with doctorate degrees and platinum cardholders displayed higher churn rates.

### Predictive Modelling for Customer Churn

#### Handling Imbalanced Data
Given the dataset's class imbalance, the Synthetic Minority Over-sampling Technique (SMOTE) was employed to balance 
the data. Additionally, class weights were adjusted to address the skewed class distribution, prioritizing the minority 
class (attrited customers).

#### Model Selection
An ensemble model, XGBoost, was chosen for its robustness and ability to handle imbalanced datasets. The model aimed 
not only for high accuracy but also high recall for class 1 (attrited customers).

#### Model Performance
The XGBoost model achieved a remarkable accuracy of 0.96 and a recall of 0.95 for class 1. This suggests the model's 
proficiency in identifying attrited customers.

### Understanding Model Behaviour

#### Feature Importance
The XGBoost model's feature importance analysis highlighted the top five contributors:
-	Total transaction count,
-	Total transaction amount,
-	Total revolving balance,
-	Total relationship count,
-	Change in Transaction Count (Q4 over Q1). 

These features had the greatest influence on the model's performance.

#### SHAP Values
Using SHAP (SHapley Additive exPlanations) values, we gained a nuanced understanding of feature contributions. The top 
five features according to SHAP values mirrored those from feature importance:
-	Total transaction count,
-	Total transaction amount,
-	Total revolving balance,
-	Total relationship count,
-	Change in Transaction Count (Q4 over Q1).

## Conclusion and Recommendations
Based on our analysis, customers with a low number of total transaction counts, low total transaction amounts, and low 
revolving balances are more likely to churn. We recommend:
-	Targeted interventions for customers with low engagement levels.
-	Providing personalized incentives to encourage higher transaction activity.
-	Regularly monitoring and addressing the specific needs of high-risk customers. 

In summary, our analysis has uncovered valuable insights that can guide strategic decisions to reduce customer churn 
and enhance overall customer retention efforts.

## Notes
All notes below are explained and given by ChatGPT 3.5.

### SMOTE (Synthetic Minority Over-sampling Technique)
SMOTE, which stands for Synthetic Minority Over-sampling Technique, is a technique used to address class imbalance in 
machine learning datasets. Imagine you're trying to solve a puzzle, but one piece is missing. SMOTE helps by creating 
new puzzle pieces that look similar to the missing one, making the puzzle more complete.

In a dataset, the majority class (like existing customers) often has more examples than the minority class (like 
churning customers). This imbalance can lead a model to focus more on the majority class and ignore the minority class. 
SMOTE fixes this by generating new, synthetic examples for the minority class. It does this by taking an existing 
minority example and creating similar but slightly different examples.

Picture it like this: If you have a few blue puzzle pieces (minority class) and lots of red pieces (majority class), 
SMOTE would craft new blue pieces that fit well with the existing ones. This helps the model learn from both classes 
equally, making it better at identifying the minority class and solving the puzzle accurately.

### XGBoost
XGBoost, known as Extreme Gradient Boosting, is a sophisticated machine learning technique that harnesses the collective 
intelligence of multiple decision-making experts to make accurate predictions. Think of it as a collaboration among 
experts, where each expert focuses on different aspects of the problem and learns from others' mistakes. This approach 
aligns seamlessly with the task of predicting churning customers, as XGBoost's ensemble of decision trees collaboratively 
analyzes customer data to identify intricate patterns that might indicate potential churn. By combining these insights, 
XGBoost equips us to anticipate customer behavior more effectively, a crucial aspect in understanding and mitigating 
churn risks.

### Feature Importance & SHAP Values
Feature importance and SHAP (SHapley Additive exPlanations) values are both ways to understand the impact of features on 
predictions, but they work differently:

#### Feature Importance:
Feature importance tells us which features had the most influence on a model's predictions. It's like ranking the players 
in a team by their contribution to winning a game. Models like XGBoost calculate feature importance during training by 
measuring how much each feature helps improve predictions. This helps us know which features are generally more valuable 
for making decisions.

#### SHAP Values:
SHAP values go a step further. They show how each feature affects a specific prediction by considering all possible 
feature combinations. It's like understanding how each player's unique skills influence a particular play in a game. 
SHAP values show the contribution of each feature to a prediction compared to if that feature wasn't there. This helps 
us see the detailed impact of features, especially when they interact with each other.

In the context of predicting churning customers, feature importance would tell us which features generally matter more 
for identifying churn. SHAP values would dive deeper, showing how each feature contributes to predicting churn for 
individual customers, considering the interactions between features.
