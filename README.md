# Health Insurance Cross-Sell

# 1. Business Problem
This project is based in a Kaggle challenge which an insurance company wants to start a cross-sell strategy. The company objective is to start selling car insurance for their clients that already have bought a health insurance with them. So the company made a research and asked to their clients if they are interested or not in buying that vehicle insurance.

So the company gave us a list with other clients that did not answered the research. As the company only have a budget to contact 20.000 clients, our job is to find out which clients in this list are the most propense to buy our car insurance to achieve the maximum profit for the company.

# 2. Business Assumptions
- There is no method for deciding which clients the company will call. (Random)
- There is a limited budget, so the company can make only 20,000 calls.

- Create a Machine Learning model that will tell us the propensity score of each client. (Learn to Rank)
- The propensity score of each customer will be returned in Google Sheets API.

# 3. Solution Strategy
My strategy to solve this challenge was:

**Step 1: Data Description:** My goal is to use statistics metrics to identify data outside the scope of business.

**Step 2: Feature Engineering:** In this part we derive new attributes based on the original features with the objective to better describe the phenomenon that will be modeled.

**Step 3: Data Filtering:** Filter some rows and columns that do not match the scope of the business or can't be used for any reason.

**Step 4: Exploratory Data Analysis:** Explore the data to find insights and better understand the impac of variables on model learning.

**Step 5: Data Preparation:** Prepare the data so that the Machine Learning models can learn the specific behavior.

**Step 6: Feature Selection:** Selection of the most significant attributes for training the model.

**Step 7: Machine Learning Modelling:** Machine Learning model training.

**Step 8: Hyperparameter Fine Tunning:** Choose the best values for each of the parameters of the model selected on the previous step.

**Step 9: Convert Model Performance to Business Values:** Convert the performance of the Machine Learning model into a business result.

**Step 10: Deploy Model to Production:** Publish the model in a cloud environment so that other people or services can use the results to improve their business decision.

# 4. Top 3 Data Insights

**Hypothesis 3:** Clients with vehicle damage should buy more car insurance.

**True:** As observed the majority of clients that wants to buy a car insurance have already suffered a vehicle damage.
![alt_text](https://github.com/jaohenritm/Health-Insurance-Cross-Sell/blob/main/img/h3.png)


**Hypothesis 5:** Clients that don't have a driving license should not buy a car insurance.

**True:** In average, the clients that don't have a driving license is nearly 3x less than clients that have a driving license.
![alt_text](https://github.com/jaohenritm/Health-Insurance-Cross-Sell/blob/main/img/h5.png)


**Hypothesis 6:** People with more recent cars should be more propense to buy a car insurance.

**False:** As we can see in this graphic, people with car older than 2 years are the most propense to buy.
![alt_text](https://github.com/jaohenritm/Health-Insurance-Cross-Sell/blob/main/img/h6.png)


### Table of All Hypothesis
|Hypothesis  |  Conclusion   | Relevance |
|------------|  ------------ | -----------|
|H1: In average, Female should buy car insurance.                                 | False | Low |
|H2: Older people should buy car insurance                                        | True | High |
|H3: Clients with vehicle damage should buy more car insurance                    | True | High |
|H4: Clients with higher annual premium should buy car insurance.                 | Inconclusive | Medium |
|H5: Clients that don't have a driving license should not buy a car insurance.    | True  | High |
|H6: People with more recent cars should be more propense to buy a car insurance. | False | High |

# 5. Machine Learning Applied

In this part, we tested this algorithms:

- Logistic Regression
- Random Forest
- XGBoost
- LightGBM
- Extra Trees

# 6. Machine Learning Performance

So we used as our metrics the **Precision at K and Recall at K**, as the business team is going to do to do 20,000 calls, we will use the Precision and Recall at 20,000.

| Model Name         | Precision at K | Recall at K |
| ------------------ | -------------- | ----------- |
| Random Forest Classifier | 0.33     | 0.09        |
| Light GBM Classifier | 0.33         | 0.70        |
| XGBoost Classifier | 0.32           | 0.70        |
| KNN Regressor Classifier | 0.29     | 0.62        |
| Logistic Regression Classifier | 0.28 | 0.60      |

As we can see the Random Forest Classifier achieved the best result. But because RandomForest is a super heavy model, we will use the Light GBM Classifier for this project.


# 7 Business Results
After doing everything that was necessary to build our Machine Learning model, now we need to see how the things turns out in the business context.

![alt_text](https://github.com/jaohenritm/Health-Insurance-Cross-Sell/blob/main/img/results.png)

As 20,000 represents nearly 20% of our total test population, if we were to call the 20,000 clients of this dataset, we should achieve nearly 60% of our total interested population meanwhile using our baseline model that number would be only 20% of our total interested clients.

For the Insurance All company the new model have 3x more effectiveness in achieving their clients. 

So now, to do a simulation we will consider somethings:
1. The validation dataset contains the same distribution as the Train dataset.
2. For every sale, the company earns $2,000 dollars.
3. The company will call 20,000 clients.

Using the random method (baseline), the Insurance All would earn an estimative of **$10,160,000 dollars.**

Using the machine learning method developed in this project, the company would earn an estimative of **$30,480,000 dollars.**

# 8. Deployment
Our Machine Learning model was hosted in the Heroku (A cloud-based platform) and can be accessed by clicking in the icon below.

For the business team we created a Google Sheets spreadsheet where the user can insert the attributes of the client and then by clicking on the button, the spreadsheet will return the propensity score of that client by a number that varies from 0 to 1.

<a href="https://hics-model.herokuapp.com/" target="_blank"><img src="https://img.shields.io/badge/Heroku-430098?style=for-the-badge&logo=heroku&logoColor=white" target="_blank"></a>
</div>

<a href="https://docs.google.com/spreadsheets/d/1z4MgVGyOG4tLDsUY_-qb9z0Wxf9WL_nMA-f6uzluXYQ/edit" target="_blank"><img src="https://img.shields.io/badge/Google%20Sheets-34A853?style=for-the-badge&logo=google-sheets&logoColor=white" target="_blank"></a>
</div>

![alt_text](https://github.com/jaohenritm/Health-Insurance-Cross-Sell/blob/main/img/spreadsheet.png)

As we can see in this image, the most propense client to buy our car insurance is the small sample of the dataset is identified by the ID: 132632.

# 9. Final Result
The objective was to practice, learn and demonstrate the power of using data solutions, and I think that the result of this project was a satisfactory one as we learned more about Business Model, Python and also JavaScript.
