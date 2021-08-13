# Python-Linear-Regression-Boston-House-Prices


**Summary**

This project performs linear regression modeling for all feature subsets with and without the addition of polynomial (degree 2) transformation in order to predict Boston house prices using the built-in sklearn dataset. 16,283 models are trained and tested given 13 features and whether or not transformed, i.e. 8,191 * 2 or (2^13-1) * 2. The top 25 models based on RMSE (root mean squared error) are then trained and tested 100 times again, the data being randomized each time before applying the same train-test split (monte carlo cross validation). The average RMSE for each model over the 100 trials is used to determine the best performing model. 

The best performing model had the following average results.

<img src="https://github.com/aaronmkwong/Python-Linear-Regression-Boston-House-Prices/blob/main/Images/01_best_model_results.JPG" width="400" height="60">

The model had 20 features in total, i.e 5 original, 5 original<sup>2<sub> and 10 pair subsets.
