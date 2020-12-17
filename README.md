# Optimizing an ML Pipeline in Azure

## Overview
This project is part of the Udacity Azure ML Nanodegree.
In this project, we build and optimize an Azure ML pipeline using the Python SDK and a provided Scikit-learn model.
This model is then compared to an Azure AutoML run.

## Summary
**In 1-2 sentences, explain the problem statement: e.g "This dataset contains data about... we seek to predict..."**
The data contains different attribute of banking clients. The classification goal is to predict if the client will subscribe a term deposit (variable y).

Data
Shape: 32,950 (row) x 20 (column)

The data is available at below link. 
(https://automlsamplenotebookdata.blob.core.windows.net/automl-sample-notebook-data/bankmarketing_train.csv)

**In 1-2 sentences, explain the solution: e.g. "The best performing model was a ..."**

Best Performing model was Logistic Regression. Dependent variable Y('Yes' , 'No') was converted to 1 and 0 to fit the model.

## Scikit-learn Pipeline
**Explain the pipeline architecture, including data, hyperparameter tuning, and classification algorithm.**

Pipeline consists of the following:
1. Data collection
2. Data Cleaning
3. Data splitting for train and test sets
4. Hyper parameter sampling
5. Model training
6. Model testing
7. Saving and registering best model into workspace 

Data sets we have devided into train(80% of the given data) and test datasets (20% of the given data).
Hyper Parameter used is : C: is the inverse of the regularization term (1/lambda). It tells the model how much large parameters are penalized, smaller values result in larger penalization.
Algorith used is Logistic Regression.

**What are the benefits of the parameter sampler you chose?**
We can think of regularization as adding (or increasing the) bias if our model suffers from (high) variance (i.e., it overfits the training data). On the other hand, too much bias will result in underfitting (a characteristic indicator of high bias is that the model shows a "bad" performance for both the training and test dataset). We have added here C: the inverse of the regularization term (1/lambda). C value is chosen from (1,2,3,4). 

**What are the benefits of the early stopping policy you chose?**
We have used here bandit policy. It terminates runs where the primary metric is not within the specified slack factor/slack amount compared to the best performing run. It saves both time and computation. 

## AutoML
**In 1-2 sentences, describe the model and hyperparameters generated by AutoML.**
Automated machine learning, also referred to as automated ML or AutoML, is the process of automating the time consuming, iterative tasks of machine learning model development. It allows data scientists, analysts, and developers to build ML models with high scale, efficiency, and productivity all while sustaining model quality. Automated ML in Azure Machine Learning is based on a breakthrough from our Microsoft Research division.
[Source: https://docs.microsoft.com/en-us/azure/machine-learning/concept-automated-ml]



## Pipeline comparison
**Compare the two models and their performance. What are the differences in accuracy? In architecture? If there was a difference, why do you think there was one?**

## Future work
**What are some areas of improvement for future experiments? Why might these improvements help the model?**

## Proof of cluster clean up
**If you did not delete your compute cluster in the code, please complete this section. Otherwise, delete this section.**
**Image of cluster marked for deletion**
