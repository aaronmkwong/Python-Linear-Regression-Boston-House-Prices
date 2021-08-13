# Python-Linear-Regression-Boston-House-Prices

**SUMMARY**

This project performs linear regression modeling for all feature subsets with and without the addition of polynomial (degree 2) transformation in order to predict Boston House Prices using the built-in sklearn dataset. 16,382 models are trained and tested given 13 features and whether or not transformed, i.e. 8,191 * 2 or (2<sup>13</sup>-1) * 2. The top 25 models based on RMSE (root mean squared error) are then trained and tested 100 times again, the data being randomized each time before applying the same train-test split (monte carlo cross validation). The average RMSE for each model over the 100 trials is used to determine the best performing model. 

The **_best performing model (BPM)_** had the following average results, which I would consider good but not great, and the project would benefit from more advanced techniques and in-depth testing in future versions.   

<img src="https://github.com/aaronmkwong/Python-Linear-Regression-Boston-House-Prices/blob/main/Images/01_best_model_result_B.JPG" width="400" height="60">

When the polynomial features are added there are 20 in total, i.e 5 original, 5 original<sup>2</sup> and 10 ( n(n-1)/2 ) pair subsets as well as the constant.

1, x0, x1, x2, x3, x4, x0<sup>2</sup>, x0x1, x0x2, x0x3, x0x4, x1<sup>2</sup>, x1x2,  x1x3, x1x4, x2<sup>2</sup>, x2x3, x2x4, x3<sup>2</sup>, x3x4, x4<sup>2</sup>

RM (x0): average number of rooms per dwelling <br/>
AGE (x1): proportion of owner-occupied units built prior to 1940 <br/> 
DIS (x2): weighted distances to five Boston employment centres <br/>
PTRATIO (x3): pupil-teacher ratio by town <br/>
LSTAT (x4): % lower status of the population

This is a somewhat brute force approach. But as a first look at the Boston House Prices dataset, I wanted the project to be as much of an exercise in writing and reusing functions as a statistical learning exercise. 

The target is MEDV, median value of owner-occupied homes in $1000's.

A description of the history and source of the dataset can be viewed **[here](https://github.com/aaronmkwong/Python-Linear-Regression-Boston-House-Prices/blob/main/Images/02_dataset_description.JPG)** as per the sklearn python library.      

**WALKTHROUGH**

The code can be viewed **[here](https://github.com/aaronmkwong/Python-Linear-Regression-Boston-House-Prices/blob/main/Program%20Files/Boston_House_Prices_06C.ipynb)**.

There are 3 custom written **_functions_** for this project. 

summary_stats() returns data exploration statistics using pandas .describe() and adds to it data types, null count, target correlation and feature correlation (multicollinearity check); arguments include dataframe, features (list) and target name (str).   

feature_select() returns a dataframe of all model experiment results with the following arguments.

arg1 (dataframe): not compatible with time series data <br/>
arg2 (list): feature column names as a list of strings (or list of list depending on agr3 inputs) <br/>
arg3 (int): choice 1 (create subset) or 2 (do not subset) or 3 (use predetermined subset) <br/>
arg4 (str): target colum name as a string <br/>
arg5 (int): choice 1 (yes) or 2 (no) or 3 (both) to add polynomial transformed (including interaction) features <br/>
arg6 (int): polynomial transformation degrees of freedom; recommend 2 only <br/>
arg7 (int): number of trials; test data is randomized each trial <br/>
arg8 (float): portion of records for testing (multiplied to total, rounded whole number);  recommended 0.3 <br/>

create_subset() returns a list of list of features for input back into feature_select() function in order to run multiple trials, with a series as the only argument.

For this project, I wanted the insights of **_data exploration_** summarized and avoid the cognitive load of working with visualizations. summary_stats() tells me all features (including categorical) are numerical, there is no missing data, distribution and which features correlate strongest with the target and themselves without irrelevant and duplicated values as seen in the correlation matrix. 

<img src="https://github.com/aaronmkwong/Python-Linear-Regression-Boston-House-Prices/blob/main/Images/03_summary_statistics_B.JPG">

The **_model results_** show that while BPM initially had a lower RMSE (left table), after 100 experiments (right table) it generalized well whereas the other likely suffered from overfitting. Of note, unlike the other, BPM did not contain the highest correlated feature pair TAX_RAD (0.91), but did contain AGE_DIS (-0.75), LSTAT_RM (-0.61), so the presence of multicollinearity may still exist. A "1" prefix in the model name indicates whether polynomial features have been added.

<img src="https://github.com/aaronmkwong/Python-Linear-Regression-Boston-House-Prices/blob/main/Images/04_model_results.JPG">

For the sake of **_model explainability_** I randomized and split the dataframe itself (rather than using sklearn train_test_split) and retained the original index as a column so I could track the original test data to the BPM predictors and predictions. The prediction is the intercept plus the dot product of the coefficients and the predictor values. 

<img src="https://github.com/aaronmkwong/Python-Linear-Regression-Boston-House-Prices/blob/main/Images/05_model_interpretation.JPG">

Finally for some quick **_model error testing_** I plotted actuals versus predictions and created a histogram. While the scatter plot is far from a straight line and the distribution shows some skew, generally the visualizations appear to be consistent with the previous model results.       

<img src="https://github.com/aaronmkwong/Python-Linear-Regression-Boston-House-Prices/blob/main/Images/06_model_error_testing.JPG" width="700" height="250">

