# Charity_Funding_Predictor

### Directory
* Code folder: holds jupyter notebooks
* Model folder: holds exported models (initial and optimized)
* Resources: holds CSV data file

### Overview

The purpose of this analysis was to design a neural network to create a binary classification model to predict whether an Alphabet-Soup funded organization will be successful based on the features in the dataset. After preprocessing the data, an initial model was compiled, trained, and evaluated. Next, the model was further optimized using kerastuner to try to achieve a target predictive accuracy of 75%.

### Results

**Data Preprocessing**
* Target variable: "IS_SUCCESSFUL" column. This column indicates successful organizations with a 1 and unsuccessful organizations with a 0.
* Feature variables: "APPLICATION TYPE", "AFFILIATION", "CLASSIFICATION", "USE CASE", "ORGANIZATION", "STATUS", "INCOME AMT", "SPECIAL CONSIDERATIONS", "ASK AMT".
    * Bucketing was performed on variables with more than 10 unique values. Rare values bucketed into "Other"
    * get_dummies was used to convert categorical data to numerical data for the purposes of this analysis.
* Variables that were removed: "EIN" and "NAME". These columns were removed as the EIN (idenfication number) and name of the organizations are neither targets nor features.

**Compiling, Training, Evaluating the Model**
* The initial model was set up with the following criteria:
    * Hidden layers: 2
    * Neurons in each layer: 1st (8), 2nd (5)
    * Activation function for hidden layers: relu, selected as it is the most common activation function
    * Activation function for output layer: sigmoid, selected as it is common for binary classification
    * Model Accuracy: 0.7321 (73.21%)
    
* Optimized model was found using keras-tuner to find the optimal hidden layers, neurons, and activation functions:
    * Hidden layers: 5
    * Neurons in each layer: 1st (1), 2nd (7), 3rd (3), 4th (9), 5th (3)
    * Activation function for hidden layers: tanh, keras-tuner found tanh to be the optimal activation function
    * Activation function for output layer: sigmoid, selected as it is common for binary classification
    * Model Accuracy: 0.7338 (73.38%)
    
### Summary

The keras-tuner ran 508 trials with different hyperparameter settings and found the "optimal model" only increased the model accuracy 0.17% to 73.38%. This falls short of the 75% target predictive accuracy. To try to improve on this neural network, next steps might be to consult with a domain expert to see if any feature variables can be removed that likely have little to no effect on the target. Running a simple logistic regression model for comparison would also be a next step.
