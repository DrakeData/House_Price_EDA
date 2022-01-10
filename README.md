# House Price EDA
## Introduction
Buying a home has been seen as the “American Dream” for several generations. There are many factors that go into picking out the ideal home for the buyer, as well as determining the sales price for the seller. For this exercise, we will be using [Ames, Iowa Real Estate data set from Kaggle.com](https://www.kaggle.com/c/house-prices-advanced-regression-techniques/overview) to perform Exploratory Data Analysis (EDA) to identify key dependent variables that help determine the sales price of a house.

## Data Exploration
Before we start digging deep into the data, I always like to review the data dictionary if one is provided. In this case, there is a ‘data_description.txt’ file that helps us understand the data values and what we should expect from the data set. One thing I noticed is that there is a lot of values that contain ‘NA’ as an actually value instead of a null value. We will need to handle this during the data cleanup process.

## Data Cleaning
Now let’s load the data into a pandas data frame and run descriptive statistics and visualizations to help understand the marginal distribution of the dependent variables.
![describ_data](images/image1.png)
The first thing I notice is that there is a count of 1460 values within the data frame. There are several columns that have null values, in which we will look into:
![data_null](images/image2.png)
There are 34 columns within this data set that contain null values. To simplify what needs to be down, I have broken the data down into 3 groups:
**Group 1:**  Categorical variables where the nulls mean no feature.
-	For these variables, I will replace ‘NA’ with ‘None’
-	Variables affected: PoolQC, MiscFeature, Alley, Fence, FireplaceQu, GarageType, GarageFinish, GarageQual, GarageCond, BsmtQual, BsmtCond, BsmtExposure, BsmtFinType1, BsmtFinType2, and MasVnrType
**Group 2:** Numerical variables where nulls mean no feature
-	For these variables, I will replace ‘NA’ with ‘0’
-	Variables affected: GarageArea, GarageCars, BsmtFinSF1, BsmtFinSF2, BsmtUnfSF, TotalBsmtSF, BsmtFullBath, BsmtHalfBath, and MasVnrArea
**Group 3:** Other null variables – these require a little more detail
-	Functional, MSZoning, Electrical, KitchenQual, Exterior1st, Exterior2nd, SaleType, and Utilities 'NA' will be replaced with their most frequent value (mode)
-	LotFrontage 'NAs' will be imputed with its mean per house based on the mean in the neighborhood
-	GarageYrBlt impute with YearBuilt (assuming that the garage is built at the same time with the house)

## Data Analysis
After the data has been cleaned up, we can begin investigating potential predictors of a home’s sale price. The first thing I did was check to see if there are any correlation with the numeric variables and sale price:
![data_corr](images/image3.png)

We can see that OverallQual, and GrLivArea have a decently high correlation to sale price. Let us dig a little deeper by visualizing them:
![box_plot1](images/image4.png)
From the above visualization, we can see that the higher the quality of the house correlates with a higher sale price.

![scatt_plot1](images/image5.png)
Looking at the above scatter plot, there is a correlation between the above grade (ground) living area and sale price. We can also see there are a couple outliers that have a high living area and a low sale price. We would want to remove these outliers as it can affect any future models that we decide to use with this data later on.

Lastly, I wanted to see if there was a correlation with fireplace quality and sale price:
![box_plot2](images/image6)
Interesting discovery: it’s better to not have a fireplace than a poor quality fireplace. Having an excellent quality fireplace does help increase the sale price.
