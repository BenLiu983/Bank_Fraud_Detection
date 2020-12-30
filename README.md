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

<img src="https://user-images.githubusercontent.com/64850893/103326030-82dd1a00-4a1c-11eb-918e-9475ff45ff1a.jpg" width="600" height="300">

## Model 1.2 - Logistic regression after Scaling (Case 2)
Used MinMax scaling before applying model.

<img src="https://user-images.githubusercontent.com/64850893/103326071-ba4bc680-4a1c-11eb-95a1-a29c39670e93.jpg" width="600" height="300">

Compare the 2 roc_auc results before and after scaling the dataframe, it can be concluded that scaling the dataframe increases the value of the metric. Therefore, I used the scaling dataframe in the following modeling experiments.

## Model 2 - XGBoost （Case 2）
In addition to the previous prodecure, I utilize the grid search to conduct the hypoparameter tuning (learning rate, number of estimators)

<img src="https://user-images.githubusercontent.com/64850893/103326158-08f96080-4a1d-11eb-924a-d5d016c69cdb.jpg" width="600" height="300">

## Model 3 - lightGBM (Case 2)
Similar to XGBoost, I use the grid search to conduct the hypoparameter tuning (learning rate, number of estimators, max_depth)

<img src="https://user-images.githubusercontent.com/64850893/103326210-40680d00-4a1d-11eb-9754-b1959e0d7491.jpg" width="600" height="300">

## Conclusion 

After the comparing the roc_auc of the 3 models in 3 cases, both XGBoost and lightGBM with the feature combanation case 2, achieved the highest roc_auc 0.76, increasing the base by 7%. However, a disadvantage of XGBoost is that its running time is relatively slow. Therefore, lightGMB with case 2 was the optimal model. To further investigate this model, it can be concluded "transactionAmount", "availableMoney", "posEM_new" are some of the key factors that would determine whether a transaction is fraud or not, according to the following plot.

<img src="https://user-images.githubusercontent.com/64850893/103326210-40680d00-4a1d-11eb-9754-b1959e0d7491.jpg" width="600" height="300">


## Future

In the future investigation, I will attempt to experiment more kinds of feature combination. Additionally, more machine learning models with hyperparameter tuning would be applied.
