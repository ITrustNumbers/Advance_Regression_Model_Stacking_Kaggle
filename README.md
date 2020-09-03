# Advance Regression : Model Stacking with Meta-Modelling
> This Project is my Entry to a Kaggle Competition [House Prices: Advanced Regression Techniques](https://www.kaggle.com/c/house-prices-advanced-regression-techniques)

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

## 2. Data Cleaning :[Data Cleaning Notebook](https://github.com/ITrustNumbers/Advance_Regression_Model_Stacking_Kaggle/blob/master/Data%20Cleaning.ipynb)

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
