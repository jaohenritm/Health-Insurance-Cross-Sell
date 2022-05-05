# Health-Insurance-Cross-Sell

# 1. Context
This project is based in a Kaggle challenge which an insurance company wants to start a cross-sell strategy. Their objective is to sell car insurance for their clients that already have bought a health insurance with them, for that they made a research and asked to their clients if they are interested in that car insurance.

# 2. Challenge
So the company gave us a list with other clients that did not answered the research. As the company only have a budget to contact 20.000 clients, our job is to find out which clients in this list are the most propense to buy our car insurance to achieve the maximum profit for the company.

## 2.1. Business
- The current method to call the clients is random.
- There is a limited budget to prospect clients.

## 2.2. Solution
- Create a Machine Learning model that will tell us the propensity score of each client. (Learn to Rank)
- The propensity score of each customer will be returned in Google Sheets API.

# 3. Bringing the Solution to Life

Observation: This solution is ficticious and was developed with open data that was made avaiable through the Kaggle platform.

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


## 3.2. Exploratory Data Analysis
On our exploratory data analysis we checked some business hypothesis to get some some informations about the data and to learn about the business itself.

|Hypothesis  |  Conclusion   | Relevance |
|------------|  ------------ | -----------|
|H1: In average, Female should buy car insurance.                                 | False | Low |
|H2: Older people should buy car insurance                                        | True | High |
|H3: Clients with vehicle damage should buy more car insurance                    | True | High |
|H4: Clients with higher annual premium should buy car insurance.                 | Inconclusive | Medium |
|H5: Clients that don't have a driving license should not buy a car insurance.    | True  | High |
|H6: People with more recent cars should be more propense to buy a car insurance. | False | High |


## 3.3 Selected Features

After doing the Exploratory Data Analysis and implementing Boruta and Features Importance, we came to the conclusion that the best features to use for our model were: 

- vintage
- annual_premium
- age
- region_code
- vehicle_damage
- previously_insured
- policy_sales_channel
