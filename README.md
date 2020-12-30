# Bank_Fraud_Detection

# Background
Fraud is a significant problem for any bank. Fraud can take many forms, whether it is someone stealing a single credit card, to large batches of stolen credit card numbers being used on the web, or even a mass compromise of credit card numbers stolen from a merchant via tools like credit card skimming devices.

This project is based on a transaction dataset that contains information about 800,000 records of a bank in Canada. The goal of this report is to build a predictive model to determine whether a given transaction will be fraudulent or not. The primary metric is roc_auc.


# Data Preparation

![ori_data](https://user-images.githubusercontent.com/64850893/103314535-68da1200-49f1-11eb-8c3f-4c007ba870f2.jpg)

Since this dataset is in line-delimited JSON format, I firstly transfromed it to a dataframe format.

![data](https://user-images.githubusercontent.com/64850893/103314331-c326a300-49f0-11eb-8381-0bae91605374.jpg)

# EDA
I utilized my domain knowlegdge in banking to select a few key features, and conducted descriptive analysis. Take the column "postEntryMode" for example:
Among all the fraud transactions, 

<img src="https://user-images.githubusercontent.com/64850893/103315082-94a9c780-49f2-11eb-854c-0aec766b7e63.jpg" width="600" height="300">

Among the non-fraud transaxtions,

<img src="https://user-images.githubusercontent.com/64850893/103315273-14d02d00-49f3-11eb-9a83-596a7bde10fd.jpg" width="600" height="300">

From the above 2 plots, it seems like "posEntryMode" has a influence on whether it is a fraud or not. So this feature will be added to my model.

## Feature engineering (3 cases)
Case 1: explanatory variables include 'cvvNotSame','amountOver', 'posEM_new', 'hour', 'transactionAmount', 'availableMoney', 'cardPresent'

Case 2: explanatory variables include 'cvvNotSame','amountOver', 'posEM_new', 'hour', 'transactionAmount', 'availableMoney', 'cardPresent', 'merchantCategoryCode'

Case 3: explanatory variables include 'cvvNotSame','amountOver', 'posEM_new', 'hour', 'transactionAmount', 'availableMoney', 'cardPresent', 'transactionType'

## Model 1 - Logistic regression (Case 2)
Implemented train-test split, cross validation, fitting the model, plotting roc curve.

<img src="https://user-images.githubusercontent.com/64850893/103315900-f23f1380-49f4-11eb-8b8a-bc94d38e0d7d.jpg" width="600" height="300">

## Model 1.2 - Logistic regression after Scaling (Case 2)
Used MinMax scaling before applying model.

<img src="https://user-images.githubusercontent.com/64850893/103316089-6679b700-49f5-11eb-8b2b-5d5e5dc7e7ba.jpg" width="600" height="300">

Compare the 2 roc_auc results before and after scaling the dataframe, it can be concluded that scaling the dataframe increases the value of the metric. Therefore, I used the scaling dataframe in the following modeling experiments.

## Model 2 - XGBoost
In addition to the previous prodecure, I utilize the grid search to conduct the hypoparameter tuning (learning rate, number of estimators)



## Model 3 - lightGBM
Similar to XGBoost, I use the grid search to conduct the hypoparameter tuning (learning rate, number of estimators, max_depth)



## Conclusion 

After the comparing the roc_auc of the 3 models in 3 cases, the optimal model is the XGBoost with the feature combanation case 2, achieving 0.76 for the roc_auc and increasing the base by 7%. However, a disadvantage of XGBoost is that its running time is relatively slow. Therefore, lightGMB can be applied when the efficiency is a significant factor. 

## Future

In the future investigation, I will attempt to experiment more kinds of feature combination. Additionally, more machine learning models with hyperparameter tuning would be applied.
