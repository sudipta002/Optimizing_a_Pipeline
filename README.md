# Optimizing an ML Pipeline in Azure

## Overview
This project is part of the Udacity Azure ML Nanodegree.
In this project, we build and optimize an Azure ML pipeline using the Python SDK and a provided Scikit-learn model.
This model is then compared to an Azure AutoML run.

## Summary

The data contains different attribute of banking clients. The classification goal is to predict if the client will subscribe a term deposit (variable y).

Data
Shape: 32,950 (row) x 20 (column)

The data is available at below link. 
(https://automlsamplenotebookdata.blob.core.windows.net/automl-sample-notebook-data/bankmarketing_train.csv)

## Scikit-learn Pipeline

Pipeline consists of the following:
1. Data collection
2. Data Cleaning
3. Data splitting for train and test sets
4. Hyper parameter sampling
5. Model training
6. Model testing
7. Saving and registering the best model into workspace 

We have devided dataset into train(80% of the given data) and test datasets (20% of the given data).
Hyperparameter used are: 

C: is the inverse of the regularization term (1/lambda). It tells the model how much large parameters are penalized, smaller values result in larger penalization and 

max_iter: is the maximum iteration to converge. 

Sampling space of both hyperparameters is C(1,2,3,4) and max_iter(75,100,125,150).


We have used Logistic Regression with HyperDrive for hyperparameters tuning. 

**What are the benefits of the parameter sampler you chose?**
We can think of regularization as adding (or increasing the) bias if our model suffers from (high) variance (i.e., it overfits the training data). On the other hand, too much bias will result in underfitting (a characteristic indicator of high bias is that the model shows a "bad" performance for both the training and test dataset). We have added here C: the inverse of the regularization term (1/lambda).

**What are the benefits of the early stopping policy you chose?**
We have used here bandit policy. It terminates runs where the primary metric is not within the specified slack factor/slack amount compared to the best performing run. It saves computation time. 

## AutoML


Automated machine learning, also referred to as automated ML or AutoML, is the process of automating the time consuming, iterative tasks of machine learning model development. It allows data scientists, analysts, and developers to build ML models with high scale, efficiency, and productivity all while sustaining model quality. Automated ML in Azure Machine Learning is based on a breakthrough from our Microsoft Research division.
[Source: https://docs.microsoft.com/en-us/azure/machine-learning/concept-automated-ml]

We found Voting Ensemble as the best model with accuracy '0.9152655538694994'.

A voting ensemble works by combining the predictions from multiple models. It can be used for classification or regression. In the case of regression, this involves calculating the average of the predictions from the models. In the case of classification, the predictions for each label are summed and the label with the majority vote is predicted.

[Source: https://machinelearningmastery.com/voting-ensembles-with-python/]

The below algorithms have been run by the fitted model i.e. voting ensemble. Few of the hyperparameters are listed here. 


| 				Algorithm			 | 	Weights	  |	learning_rate |	n_estimators |
|------------------------------------|----------------|---------------|--------------|
| xgboostclassifier, maxabsscaler	 | 0.307692308	  | 0.1			  |		100      |
|lightgbmclassifier, maxabsscaler	 | 0.384615385	  | 0.1			  | 	100      |
|randomforestclassifier, minmaxscaler|	0.076923077	  |	           |  10			 |
|randomforestclassifier, minmaxscaler|	0.076923077	  |	            |	10		 |
|randomforestclassifier, minmaxscaler|	0.153846154	  |	 			  |  	25		 |


## Pipeline comparison

Steps followed in AutoML are:

1. FeaturesGeneration: Generating features for the dataset.
2. DatasetCrossValidationSplit: Generating individually featurized CV splits.
3. ModelSelection: Beginning model selection.

Accuracy of HyperDrive model: 0.912797167425392

Accuracy of AutoML: '0.9152655538694994'

It is obvious that AutoML has achieved a bit higher accuracy with Voting Ensemble than that of Logistic Regression using HyperDrive. 

In experiment with HyperDrive, it is defined to work with Logistic Regression whereas AutoML facilitates to work on wide variety of algorithms. AutoML gives the best result in model selection, thus, providing better accuracy. 

## Future work
1. We would like to use other primary metrics because accuracy sometimes does not help derive model performance. 
2. We would like to have more experiment time for AutoML so that it can run more algorithms. This will help us find out the accurate model.
3. In experiment with HyperDrive, we could use Bayesian sampling in place of Random sampling for Hyperparameter selection. Bayesian sampling is based on the Bayesian optimization algorithm. It picks samples based on how previous samples performed, so that new samples improve the primary metric.
4. We could use warm start which enables to reuse knowledge of previous runs accelerating hyperparameter tuning in HyperDrive experiment.
[Source: https://docs.microsoft.com/en-us/azure/machine-learning/how-to-tune-hyperparameters]
5. We need to work on imbalanced data which can lead to a falsely perceived positive effect of a model's accuracy because the input data has bias towards one class.
