# FraudRiskDefender
Projct of detection of fraudulent transactions originating on mobile devices

#### This project was made by Gabriel Alves.

# 1. Business Problem.
A Blocker Fraud Company is a company specialized in detecting fraud in financial transactions made through mobile devices. The company has a service called "Blocker Fraud" which guarantees the blocking of fraudulent transactions.

The company's business model is a Service type, with monetization based on the performance of the service provided. This means that the user pays a fixed fee based on the successful detection of fraud in the client's transactions.

However, Blocker Fraud Company is in the expansion phase in Brazil and has adopted a very aggressive strategy to acquire clients more quickly. The strategy works as follows:

- The company will receive 25% of the value of each transaction truly detected as fraud.
- The company will receive 5% of the value of each transaction detected as fraud, but is truly legitimate.
- The company will refund 100% of the value to the client for each transaction detected as legitimate, but is truly a fraud.

# 2. Business Assumptions.

**Dataset features:**

- **step:** maps a unit of time in the real world. In this case 1 step is 1 hour of time. Total steps 744 (30 days simulation).
- **type:** CASH-IN, CASH-OUT, DEBIT, PAYMENT and TRANSFER.
- **amount:** amount of the transaction in local currency.
- **nameOrig:** customer who started the transaction.
- **oldbalanceOrg:** initial balance before the transaction.
- **newbalanceOrig:** new balance after the transaction.
- **nameDest:** customer who is the recipient of the transaction.
- **oldbalanceDest:** initial balance recipient before the transaction. Note that there is not information for customers that start with M (Merchants).
- **newbalanceDest:** new balance recipient after the transaction. Note that there is not information for customers that start with M (Merchants).
- **isFraud:** This is the transactions made by the fraudulent agents inside the simulation. In this specific dataset the fraudulent behavior of the agents aims to profit by taking control or customers accounts and try to empty the funds by transferring to another account and then cashing out of the system.
- **isFlaggedFraud:** The business model aims to control massive transfers from one account to another and flags illegal attempts. An illegal attempt in this dataset is an attempt to transfer more than 200.000 in a single transaction.

**Some assumptions were made in order to ensure a more accurate analysis of the dataset. These assumptions are as follows:**

- Since the dataset was constructed to represent transactions over a period of 30 days, only the steps representing the hours within those 30 days were considered, ranging from 1 to 720. This decision was made because all other transactions were classified as fraud, which seemed highly unusual and indicated a possible error in data extraction/generation.
- Transactions with a value of 0 were excluded from the analysis.
- Transactions with a balance of 0 before and after the transaction, both in the source and destination accounts, were kept in the dataset. This decision was made because it was not specified, nor could it be determined, whether this is a normal occurrence for this type of mobile financial service.

# 3. Solution Strategy

My strategy to solve this challenge was:

**Step 01. Data Description:** Describe the available data, including its structure, characteristics, and basic statistics.

**Step 02. Feature Engineering:** Create new variables or transform existing ones with the aim of improving the predictive power of the model.

**Step 03. Data Filtering:** Remove or filter out unwanted or irrelevant instances from the dataset.

**Step 04. Exploratory Data Analysis:** Conduct exploratory analysis of the data to gain insights, identify patterns, and relationships between variables.

**Step 05. Data Preparation:** Preprocess and clean the data, including handling missing values, encoding categorical variables, and scaling numeric features.

**Step 06. Feature Selection:** Select the most relevant and informative features for the classification task.

**Step 07. Machine Learning Modeling:** Train and evaluate machine learning models using the prepared dataset.

**Step 08. Hyperparameter Fine-Tuning:** Optimize the model's hyperparameters to improve its performance.

**Step 09. Convert Model Performance to Business Values:** Translate the model's performance metrics into meaningful business values or impact, such as financial losses prevented or detection rates.

**Step 10. Deploy Model to Production:** Integrate the final model into a production environment to make real-time predictions and monitor its performance over time.

# 4. Top 3 Data Insights

**Hypothesis 01:** The majority of frauds occur when the final balance of the origin account is 0.

**True -**  98% of the frauds occurred with a starting balance of zero in the source account, indicating that the account is clean out after the fraud


**Hypothesis 02:** The majority of frauds occur with transfers or cash out.

**True -** Frauds occur only in Transfer and Cash out transactions, almost in equal proportion


**Hypothesis 03:** The majority of frauds occur in the last 5 days of the month.

**False -** Although the first 5 days of the month have the highest representation of frauds, the difference in comparison to other days is negligible, with a narrow margin ranging from 1.34% to 0.41%.

# 5. Machine Learning Model Applied

Four different types of classification algorithms were used, including:

- Logistic Regression
- K-Nearest Neighbors
- Random Forest
- XGBoost Classifier

When testing all four algorithms mentioned above, we calculated several relevant metrics to make a comparison and select the algorithm with the best results for fraud classification, as shown in the table below:

![models_performances_table](https://github.com/GabrielAlvesDS/fraud_risk_defender/blob/main/docs/models_performances_table.PNG)

# 6. Machine Learning Modelo Performance

Analyzing the results of all tested algorithms, I chose the XGBoost Classifier due to its high performance in metrics a, b, c, and its fast processing time. Although Random Forest had slightly better results, it required much more processing time.

We apply Sklearn's GridSearchCV method to identify the optimal parameters for the algorithm. The results obtained were the following:

![GridSearchCV_final_scores](https://github.com/GabrielAlvesDS/fraud_risk_defender/blob/main/docs/GridSearchCV_final_scores.PNG)

**Final XGBoost Confusion Matrix**
![Final_model_confusion_matrix](https://github.com/GabrielAlvesDS/fraud_risk_defender/blob/main/docs/Final_model_confusion_matrix.PNG)

# 7. Business Results

- The company will receive 568,024,814.50 due to transactions truly detected as fraud
- The company will receive 0.00 due to transactions detected as fraud, but actually legitimate
- The company will give back 30,606,186.24 due to transactions detected as legitimate, but actually fraud


The company will have a total of **537,418,628.26**

# 8. Conclusions


# 9. Lessons Learned

# 10. Next Steps to Improve

