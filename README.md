# Blocker fraud company



---

## Table of Contents
- [Introduction](#introduction)
- [1. The Business Challenge](#1-the-business-challenge)
- [2. The Dataset](#2-the-dataset)
- [3. Feature Engineering and Variables Filtering](#3-feature-engineering-and-variables-filtering)
- [4. EDA Summary and Insights](#4-eda-summary-and-insights)
- [5. Data Preparation and Feature Selection](#5-data-preparation-and-feature-selection)
- [6. Machine Learning Modelling and Fine Tuning](#6-machine-learning-modelling-and-fine-tuning)
- [7. Business Performance and Results](#7-business-performance-and-results)
- [8. Next Steps](#8-next-steps)
- [9. Lessons Learned](#9-lessons-learned)
- [10. Conclusion](#10-conclusion)
- [References](#references)

**Project Development Method**

The project was developed based on the CRISP-DS (Cross-Industry Standard Process - Data Science, a.k.a. CRISP-DM) project management method, with the following steps:

- Business Understanding
- Data Collection
- Data Cleaning
- Exploratory Data Analysis (EDA)
- Data Preparation
- Machine Learning Modelling and fine-tuning
- Model and Business performance evaluation / Results

---

## 1. The Business Challenge

**The Blocker Fraud Company**

The Blocker Fraud Company is a specialized company in fraud detection on financial transactions. It has the Blocker Fraud service, which ensures the block of fraudulent transactions. The company's business model is service's performance monetization.

**Expansion Strategy in Brazil**

The company aims to expand its business in Brazil, therefore set the following expansion strategy:

1. The company receives 25% of each transaction value truly detected as fraud.
2. The company receives 5% of each transaction value detected as fraud, however the transaction is legitimate.
3. The company gives back 100% of the value for the customer in each transaction detected as legitimate, however the transaction is actually a fraud.

**Goal of the project**

- Create a model with high accuracy and precision with respect to transactions' fraud detection.

**Deliverables**

- A model that classifies the transactions as "Fraud" or "Legitimate".
- Deployed model with API access. The API must inform "Fraud" or "Legitimate" when the transaction is inputed.
- A Readme about how to use the tool.
- Model performance and results report with respect to profit and loss. The following questions must be answered:

    - What is the model's precision and accuracy?
    - What is the model's reliability with respect to transactions' classification as legitimate or fraudulent?
    - What is the company's forecasted revenue if the model classifies 100% of the transactions?
    - What is the company's forecasted loss in case of model's failure?
    - What is the Blocker Fraud Company forecasted profit using the model?


This repository focuses on the model development and business performance and results.

[back to top](#table-of-contents)

---

## 2. The Dataset
### 2.1. Dataset origin and brief description
The dataset used on this project is a synthetic financial dataset generated in a simulator called PaySim and available on [kaggle](https://www.kaggle.com/ntnu-testimon/paysim1) [[1]](#references). The PaySim simulator uses aggregated data from private dataset to generate a synthetic dataset that resembles the normal operation of transactions and adds malicious behaviour to later evaluate the performance of fraud detection methods.

### 2.2. Dataset Size and Dimensions
The dataset has 6,362,620 entries and 11 features described below:

**step** - maps a unit of time in the real world. In this case 1 step is 1 hour of time. Total steps 744 (30 days simulation).

**type** - CASH-IN, CASH-OUT, DEBIT, PAYMENT and TRANSFER.

**amount** - amount of the transaction in local currency.

**nameOrig** - customer who started the transaction

**oldbalanceOrg** - initial balance before the transaction

**newbalanceOrig** - new balance after the transaction

**nameDest** - customer who is the recipient of the transaction

**oldbalanceDest** - initial balance recipient before the transaction. Note that there is not information for customers that start with M (Merchants).

**newbalanceDest** - new balance recipient after the transaction. Note that there is not information for customers that start with M (Merchants).

**isFraud** - This is the transactions made by the fraudulent agents inside the simulation. In this specific dataset the fraudulent behavior of the agents aims to profit by taking control or customers accounts and try to empty the funds by transferring to another account and then cashing out of the system.

**isFlaggedFraud** - The business model aims to control massive transfers from one account to another and flags illegal attempts. An illegal attempt in this dataset is an attempt to transfer more than 200.000 in a single transaction.

The dataset file has 470 MB, and when loaded in pandas it has a memory usage of 534 MB. 

![](images/02_data_info.png)

Therefore, the available RAM memory is crucial to run properly the code. In order not to compromise it, the dataset was several times saved, as the preprocessing was completed, to allow the code execution in steps. Hence, before executing the code it is important to check the available space in HD / memory and how much it will take. The strategy to save the preprocessed dataset and execute the code in steps worked properly in the computer used to develop this project (HD 1TB, RAM memory 8GB), but it may be changed depending on the hardware that it will be executed.

As described in the lessons learned section, the way the dataset is handled is crucial for the model training and hence for the project success. In this case, some attemps were made until reaching the expected performance to meet the project goal.

The dataset was split into train and test set with 70/30 ratio.

[back to top](#table-of-contents)

---





