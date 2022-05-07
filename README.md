# Health Insurance Cross-Sell

# 1. Business Problem
This project is based in a Kaggle challenge which an insurance company wants to start a cross-sell strategy. The company objective is to start selling car insurance for their clients that already have bought a health insurance with them. So the company made a research and asked to their clients if they are interested or not in buying that vehicle insurance.

So the company gave us a list with other clients that did not answered the research. As the company only have a budget to contact 20.000 clients, our job is to find out which clients in this list are the most propense to buy our car insurance to achieve the maximum profit for the company.

# 2. Business Assumptions
- There is no method for deciding which clients the company will call. (Random)
- There is a limited budget, so the company can make only 20,000 calls.

- Create a Machine Learning model that will tell us the propensity score of each client. (Learn to Rank)
- The propensity score of each customer will be returned in Google Sheets API.

# 3. Bringing the Solution to Life
My strategy to solve this challenge was:

- Create a Machine Learning model that will tell us the propensity score of each client. (Learn to Rank)

Observation: This solution is ficticious and was developed with open data that was made avaiable through the Kaggle platform. But to practice, I got this dataset from a AWS server.

Link: https://www.kaggle.com/datasets/anmolkumar/health-insurance-cross-sell-prediction

## 3.1 Data Description

| Variable | Definition |
| -------- | ---------- |
| id	               | Unique ID for the customer |
| Gender             | Gender of the customer |
| Age	               | Age of the customer |
| Driving_License    | 0: Customer does not have DL, 1: Customer already has DL |
| Region_Code     	 | Unique code for the region of the customer |
| Previously_Insured | 1 : Customer already has Vehicle Insurance, 0 : Customer doesn't have Vehicle Insurance |
| Vehicle_Age        |	Age of the Vehicle |
| Vehicle_Damage     |	1 : Customer got his/her vehicle damaged in the past. 0 : Customer didn't get his/her vehicle damaged in the past. |
| Annual_Premium     |	The amount customer needs to pay as premium in the year | 
| PolicySalesChannel |	Anonymized Code for the channel of outreaching to the customer ie. Different Agents, Over Mail, Over Phone, In Person, etc. |
| Vintage	Number     | Number of Days, Customer has been associated with the company |
| Response           |	1 : Customer is interested, 0 : Customer is not interested |

As we explore the data, we discover that this dataset have 381,109 rows and 12 columns. That means that we can process these data in our own computer.

## 3.2 Feature Engineering:
![alt_text](https://github.com/jaohenritm/Health-Insurance-Cross-Sell/blob/main/img/MindMap.png)

## 3.3 Data Filtering:
In this step, there was no need to filter any features.

## 3.4 Exploratory Data Analysis
On our exploratory data analysis we checked some business hypothesis to get some some informations about the data and to learn about the business itself.


### These heatmap shows us the correlation between all predictors and our response feature.

![alt_text](https://github.com/jaohenritm/Health-Insurance-Cross-Sell/blob/main/img/HeatMap.png)


### Table of All Hypothesis
|Hypothesis  |  Conclusion   | Relevance |
|------------|  ------------ | -----------|
|H1: In average, Female should buy car insurance.                                 | False | Low |
|H2: Older people should buy car insurance                                        | True | High |
|H3: Clients with vehicle damage should buy more car insurance                    | True | High |
|H4: Clients with higher annual premium should buy car insurance.                 | Inconclusive | Medium |
|H5: Clients that don't have a driving license should not buy a car insurance.    | True  | High |
|H6: People with more recent cars should be more propense to buy a car insurance. | False | High |

## 3.5 Data Preparation
So we separeted our dataset in train and validation with a proportion of 80% train and 20% validation.

## 3.6 Feature Selection

After doing the Exploratory Data Analysis and implementing Boruta and Features Importance, we came to the conclusion that the best features to use for our model were: 

- vintage
- annual_premium
- age
- region_code
- vehicle_damage
- previously_insured
- policy_sales_channel

## 3.7 Machine Learning Modelling
For this case, we used some machine learning algorithms to rank these clients per their propensity score.

Machine Learning Models:
- K-nearest Neighbors Algorithm
- Logistic Regression
- Random Forest
- XGBoost
- LightGBM
- Extra Trees

Amongst them, the model that achieved the better result was the Random Forest, but in this case, as the Random Forest turned out to be a super heavy model that can't be uploaded in our free Heroku platform, we proceeded with the second one, which was the XGBoost.

# 4 Machine Learning Performance

## 4.1 XGBoost Results
So we used as our metrics the **Precision at K and Recall at K**, as the business team is going to do to do 20,000 calls, we will use the Precision and Recall at 20,000.

**Precision at 20,000: 0.32**

**Recall at 20,000: 0.70**

## 4.2 Business Performance
After doing everything that was necessary to build our Machine Learning model, now we need to see how the things turns out in the business context.

![alt_text](https://github.com/jaohenritm/Health-Insurance-Cross-Sell/blob/main/img/results.png)

As 20,000 represents nearly 20% of our total test population, if we were to call the 20,000 of this dataset, we should achieve nearly 60% of our total interested population meanwhile using our baseline model that number would be only 20% of our total interested clients.

For the Insurance All company the new model have 3x more effectiveness in achieving their clients. 

So now, to do a simulation we will consider somethings:
- The validation dataset contains the same distribution as the Train dataset.
- For every sale, the company profits $2,000 dollars.

---

**Random Method: $10,160,000 profit.**

**Machine Learning Model: $30,480,000 profit.**

Applying our machine learning model instead the random one on the validation dataset, the company would profit approximately **$20,320,000 dollars** more.

# 5. Deployment
Our Machine Learning model was hosted in the Heroku (A cloud-based platform) and can be accessed by clicking in the icon below.

For the business team we created a Google Sheets spreadsheet where the user can insert the attributes of the client and then by clicking on the button, the spreadsheet will return the propensity score of that client by a number that varies from 0 to 1.

<a href="https://hics-model.herokuapp.com/" target="_blank"><img src="https://img.shields.io/badge/Heroku-430098?style=for-the-badge&logo=heroku&logoColor=white" target="_blank"></a>
</div>

<a href="https://docs.google.com/spreadsheets/d/1z4MgVGyOG4tLDsUY_-qb9z0Wxf9WL_nMA-f6uzluXYQ/edit" target="_blank"><img src="https://img.shields.io/badge/Google%20Sheets-34A853?style=for-the-badge&logo=google-sheets&logoColor=white" target="_blank"></a>
</div>

![alt_text](https://github.com/jaohenritm/Health-Insurance-Cross-Sell/blob/main/img/spreadsheet.png)

As we can see in this image, the most propense client to buy our car insurance is the small sample of the dataset is identified by the ID: 132632.

# 6. Final Result
The objective was to practice and learn more about "Learn to Rank" solutions, and I think that it was a satisfactory one as we learned more about 
Business, Python and a tip of JavaScript.
