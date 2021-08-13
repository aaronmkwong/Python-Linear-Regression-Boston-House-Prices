# Python-Linear-Regression-Boston-House-Prices

**SUMMARY**

This project performs linear regression modeling for all feature subsets with and without the addition of polynomial (degree 2) transformation in order to predict Boston house prices using the built-in sklearn dataset. 16,283 models are trained and tested given 13 features and whether or not transformed, i.e. 8,191 * 2 or (2<sup>13</sup>-1) * 2. The top 25 models based on RMSE (root mean squared error) are then trained and tested 100 times again, the data being randomized each time before applying the same train-test split (monte carlo cross validation). The average RMSE for each model over the 100 trials is used to determine the best performing model. 

The **_best performing model_** had the following average results, which I would consider good but not great, and the project would likely benefit from applying more advanced techniques and in-depth testing in future versions.   

<img src="https://github.com/aaronmkwong/Python-Linear-Regression-Boston-House-Prices/blob/main/Images/01_best_model_results.JPG" width="400" height="60">

When the polynomial features are added there are 20 in total, i.e 5 original, 5 original<sup>2</sup> and 10 ( n(n-1)/2 ) pair subsets as well as the constant.

1, x0, x1, x2, x3, x4, x0<sup>2</sup>, x0x1, x0x2, x0x3, x0x4, x1<sup>2</sup>, x1x2,  x1x3, x1x4, x2<sup>2</sup>, x2x3, x2x4, x3<sup>2</sup>, x3x4, x4<sup>2</sup>

RM (x0): average number of rooms per dwelling <br/>
DIS (x1): weighted distances to five Boston employment centres <br/>
TAX (x2): full-value property-tax rate per $10,000 <br/>
PTRATIO (x3): pupil-teacher ratio by town <br/>
LSTAT (x4): % lower status of the population

Admittedly, this is a somewhat brute force approach with basic data exploration and error testing. But, as a first look at the Boston House Price dataset, I wanted the project to be as much of an exercise in writing and reusing functions as a statistical learning exercise.    
