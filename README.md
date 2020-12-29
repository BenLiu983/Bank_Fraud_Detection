# Bank_Fraud_Detection

# Background
Fraud is a significant problem for any bank. Fraud can take many forms, whether it is someone stealing a single credit card, to large batches of stolen credit card numbers being used on the web, or even a mass compromise of credit card numbers stolen from a merchant via tools like credit card skimming devices.

This project is based on a transaction dataset that contains information about 800,000 records of a bank in Canada. The goal of this report is to build a predictive model to determine whether a given transaction will be fraudulent or not. The primary metric is roc_auc.


# Data Preparation
Since this dataset is in line-delimited JSON format, I firstly transfrom it to a dataframe format.
![readme_plot1](https://github.com/BenLiu983/Bank_Fraud_Detection/issues/1#issue-776090095)
