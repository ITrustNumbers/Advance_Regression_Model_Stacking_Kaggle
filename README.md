# Advance Regression : Model Stacking with Meta-Modelling
> This Project is my Entry to a Kaggle Competition [House Prices: Advanced Regression Techniques](https://www.kaggle.com/c/house-prices-advanced-regression-techniques)<br>
The Target was to rank in the Top 5% in the LeaderBoard and Hence, Target Score was to chosen to be < 0.1 

## Result : 
> I Ranked in the Top 5% in the LeaderBoard, 280th Position out of the 5,110 Entries

# Walkthrough :

## 1. About the Data :

#### All the Data used in this Project is from Kaggle House Pricing Data Set

- [Kaggle Competition: House Pricing](https://www.kaggle.com/c/house-prices-advanced-regression-techniques/data)

#### File Description 

- train.csv - the training set
- data_description.txt - full description of each column, originally prepared by Dean De Cock but lightly edited to match the column names used here

#### Data Fields

- You Can Find About the Data Fields [Here](https://github.com/ITrustNumbers/Advance_Regression_Model_Stacking_Kaggle/tree/master/Original_DataSet)

## 2. Data Cleaning :[(Data Cleaning Notebook)](https://github.com/ITrustNumbers/Advance_Regression_Model_Stacking_Kaggle/blob/master/Data%20Cleaning.ipynb)

### Outliers Detection 

> Some Outliers were detected during Visualizing the Data as shown below (Two Points with GrLivArea > 4000 & Sale Price < 200000)

![Outlier Detection](https://github.com/ITrustNumbers/Advance_Regression_Model_Stacking_Kaggle/blob/master/Visualizations/Checking_Outliers.png)

### Outliers Removal

> After Removing the Outliers The Plot shows improvement in Linearity of the Phenomena

![Removal](https://github.com/ITrustNumbers/Advance_Regression_Model_Stacking_Kaggle/blob/master/Visualizations/Removed_Outliers.png)

### Inspecting the Target Value SalePrice 

> While Inspecting the Target Value it was Found that it was Positively Skewed and Hence the Skew Was removed my using Box Cox transformation With Lamda = 0.15

![Target Value Skew](https://github.com/ITrustNumbers/Advance_Regression_Model_Stacking_Kaggle/blob/master/Visualizations/TargetValue_Skew.png)

> As, You can see the Target Value Reached a near Perfect Normal Distribution

### Handling Missing Data 

> There was a lot of Missing Data in the DataSet as some feature were designed to have some properties reflected by Null Values and Hence, A lot of tranformation was done

![Missign Data](https://github.com/ITrustNumbers/Advance_Regression_Model_Stacking_Kaggle/blob/master/Visualizations/MissingData_Percentage.png)

> Some of the Transformation that was to Fill Missing Values 

![Snapshot Natebook](https://github.com/ITrustNumbers/Advance_Regression_Model_Stacking_Kaggle/blob/master/_Images/Fill_MissingValues.PNG)

## Feature Engineering :[(Feature Engineering Notebook)](https://github.com/ITrustNumbers/Advance_Regression_Model_Stacking_Kaggle/blob/master/Feature%20Engineering.ipynb)

### One Feature Was Added

> Total SquareFoot Was Added, By adding SquareFoot Areas Of All Floor of the Houses In the Dataset

### LabelEncoding For the Categorical Features

> Sklearn Label Encoder was used for Label Encoding

### Removed Skew in Feature Distribution

> There was Skew in almost 50% of the Features and some Features had Large amount of it and Hence, Skew as Removed by Using Box Cox Tranformation with Lamda = 0.15 and The Threshold was chosen to be Skew > 0.75

![Skewed Features](https://github.com/ITrustNumbers/Advance_Regression_Model_Stacking_Kaggle/blob/master/_Images/Skewed_Feat.png)

## Model Building :[(Model Building Notebook)](https://github.com/ITrustNumbers/Advance_Regression_Model_Stacking_Kaggle/blob/master/Model%20Building.ipynb)

### Evaluation Metric

> According thr rules of the Competition the Evaluation Metric was Root Mean Square Logarithmic Error(RMSLE)

![RMSLE](https://github.com/ITrustNumbers/Advance_Regression_Model_Stacking_Kaggle/blob/master/_Images/RMSLE.png)

> Note that in the formulation X is the predicted value and Y is the actual value <br />
The Target was to get into top 5% in the kaggle Leaderboard thus, target was to get a RMSLE < 0.1

### Base Model Scoring
> Base Model Was Chosen and then were tuned by GridSearchCV and then were Scored to Gauge Performance 
<br />

- **Lasso Score: 0.1116 (Std: 0.0074)** 
<br />

- **ElasticNet Score: 0.1116 (Std: 0.0074)**
<br />

- **Kernel Ridge Score: 0.1152 (Std: 0.0075)**
<br />

- **Gradient Boosting Score: 0.1166 (Std: 0.0083)**
<br />

- **Xgboost Score: 0.1161 (Std: 0.0072)**
<br />

- **LGBM Score: 0.1164 (Std: 0.0062)**

### Model Stacking : Average Based Model Class

> We begin with this simple approach of averaging base models. We build a new class to extend scikit-learn with our model and also to laverage encapsulation and code reuse (inheritance)

- **Averaged Based Model Class Score: 0.1087 (Std: 0.0076)**

> It seems even the simplest stacking approach really improve the score . This encourages us to go further and explore a less simple stacking approach.

### Model Stacking : Adding a Meta Model

> In this approach, We add a meta-model on averaged base models and use the out-of-folds predictions of these base models to train our meta-model.<br><br>
The procedure, for the training part, may be described as follows:<br><br>
Split the total training set into two disjoint sets (here train and holdout )<br><br>
Train several base models on the first part (train)<br><br>
Test these base models on the second part (holdout)<br><br>
Use the predictions from holdout fold (called out-of-folds predictions) as the inputs, and the correct responses (target variable) as the outputs to train a higher level learner called meta-model.<br><br>
The first three steps are done iteratively . If we take for example a 5-fold stacking , we first split the training data into 5 folds. Then we will do 5 iterations. In each iteration, we train every base model on 4 folds and predict on the remaining fold (holdout).<br><br>
So, we will be sure, after 5 iterations , that the entire data is used to get out-of-folds predictions that we will then use as new feature to train our meta-model<br><br>
For the prediction part , We average the predictions of all base models on the test data and used them as meta-features on which, the final prediction is done with the meta-model.<br><br>

![Adding Meta Model](https://github.com/ITrustNumbers/Advance_Regression_Model_Stacking_Kaggle/blob/master/_Images/Meta-Model.jpg)

> After this all the Results were put in a Ensemble to get the Final Results

- **Final Ensemble Score: 0.076**

## Conclusion :

> The Final Scored Reached is RMSLE = 0.076 i.e < 0.1 and Hence, Target was Reached
