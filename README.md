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

![fraud_post](https://user-images.githubusercontent.com/64850893/103315082-94a9c780-49f2-11eb-854c-0aec766b7e63.jpg)

Among the non-fraud transaxtions,





