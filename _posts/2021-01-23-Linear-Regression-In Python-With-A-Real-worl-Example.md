---
layout: post
title:  "
Linear Regression In Python With A Real-world Example

"
date:   2021-01-23 16:01:15 +0300
categories: jekyll update
---
## Image 

## Introduction
In this blog, we will be working linear regression using data we analyzed in the previous blog. The objective of this blog is to make you understand how to implement linear regression using python. We shall be using sklearn library to do the regression, matplotlib for visualization and pandas to do the analysis.

## Linear Regression
Linear regression is about getting a line of best fit for values. It helps model the relationship between variables for example predicting the cost of a hotel given its neighbourhood, service and type. It is a supervised learning algorithm meaning we provide data to the model for it to learn patterns. Regression helps to predict or interpolate the values of that we haven’t seen given data we have seen before.

Regression is an intuitive algorithm which we all have ever done in our mind, for example, predicting the price of vegetables in a given season.it is the easiest and one of the commonest machine learning algorithms. Actually, most problems just require regression instead of fancy machine learning Algorithms. You can apply it in finance, health, economics problems where the variables are linearly related etc. The limitation of the algorithm is it works with dependant variables that are continuous in nature.

### Variable Types
We have two types of variables. Independent variable and dependent variable. Dependent variable /outcome must be continuous type but Independent variables/features can be any time, for example,  discrete, continuous, categorical type(gender, class).

### Equation
We write the function for linear equation as 
## Image 
where:
m = coefficient/ rate of improvement
b-bias
The aim is to find the optimal parameters( coefficient and bias).
y /f(x) is the predicted value.
Y is The regression line or line of best fit is one for which an error is minimized. The errors or residuals can be drawn as vertical lines from the observed value to the regression line (see figure one).
Residuals are the difference between the points and the fitted line.

### Cost Function
We write the cost function for the above equation as:
## Image 

N is the data points
Y is the actual value of observation
y=mx+b which is the predicted value
Our goal is to minimize it to improve the accuracy by finding m for which mse(m) is minimum

## Simple/Univariate Regression
Simple regression is one where we have one feature and one target variable. Simple regression is an easy one. An example is trying to predict the performance of students given the hours they put into studying. Income was given the position or years of experience of the developer.

### Equation
This is the same as the general equation, i represents the observation .
## Image 

It has one feature x and output/ target one. the goal is to find f(x) so that when new data is exposed to the function we can get a prediction which is close to the actual value.

Example: Consider our situation where we have government expenditure  (G)and unemployment(U) ignoring other factors that lead to unemployment we model the relationship as.

## Image 

Implementation
We are going to use the African economic data which has government expenditure and unemployment percentage. We shall take unemployment as our target value and government expenditure as x value. For this task, we shall be using sklearn for the regression class, Pandas for analysis and loading data and Matplotlib for visualization.

```python
#import necessary packages
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression
#Load data
df = pd.read_csv('economic-data-africa.csv', sep=';', encoding='ISO-8859-1')
``` 

Let us take a peek at the first 5 rows of our dataset by calling df.head(). the index count start at zero thats the reason the last value 4.
## Image 

### Summarize Data

Before we go ahead and train our regression model there is a need for us to do data analysis on it. This step is important because it helps us discover any outliers and other anomalies in the data. We shall do this in two ways. First using descriptive statistics and then data visualization.

### Descriptive statistics

Descriptive statistics help us find distributions in our data. Here we perform statistical tasks like finding the mean, median, count etc on the data. This can be done individually, but thanks to pandas describe function we can do this in one line. let us check the dimension and data types of our variables

```python 
#check dimension of data
df.shape
(51, 3)
#check data type
df.dtypes
CountryName           object
GovExpenditurePerc     int64
UnemploymentPerc       int64
dtype: object
```


The results show us that we have a matrix of 51 by 3 dimension. our dataset has three columns/features and 51 rows. Matrix is written row by column. we also see that our features are country name, UnemploymentPerc and GovExpenditurePerc with data types object/string, integer respectively.

We use describe method to check the the statistical properties of the data.

## Image 

### Data visualizations

Visualization makes it easy for us to see the variable distributions, identify outliers and map relationship in the data. We shall draw a scatter plot of the data to see how they relate to each other. Because linear regression works well with linearly related data, we use this step to verify the variables are linearly related. the bar graph will show the variable distribution.

```python
df.hist( color ="#FF69B4")
plt.savefig("simple_hist.png")
plt.show()
```
## Image 

```python 
# Visualising the data distribution
plt.scatter(df["GovExpenditurePerc"], df["UnemploymentPerc"], color = '#FF69B4')
plt.title('Unemployment vs Government expenditure',fontsize =20)
plt.xlabel('Government Expenditure',fontsize =20)
plt.ylabel('Unemployment',fontsize =20)
plt.grid()
plt.savefig("UnempVsExp.png")
plt.show()
``` 
# Image 
From our plots, we see that there is an outlier. The expenditure above 80 which may affect our model. Let us remove data that is above 80 per cent.

```python
# Remove rows with outliers
df = df.loc[df['GovExpenditurePerc'] < 70]
df.shape
(50, 3)
```
### Model training

Let us assign our variables to x and y.
X = government expenditure
y= unemployment
We reshape x into two dimension using reshape(-1, 1).
We divide data into training and test sections using sklearn test split function so that we can use the test set to use to evaluate how our linear regression model performs on unseen data. We assigned 80% of the data as a train set and 20% as a test set. We shall train our model using the LinearRegression class from sklearn. After creating an instance of the class we call the fit method and pass in x and y data to fit the data.

```python 
# deciding target and data value
Y =df.iloc[:,2].values
X = df.iloc[:, 1].values

#reshape x
X =X.reshape(-1, 1)

# Split the data into Train set and Test set
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, Y, test_size = 0.2,random_state = 0)

# Fitting Simple Linear Regression to the Training set
from sklearn.linear_model import LinearRegression
regressor = LinearRegression()
regressor.fit(X_train, y_train)
##Print our w and E value
print(regressor.coef_) # the slope
print(regressor.intercept_) # the intercept
#ouput
[0.33058722]
0.8284703168542435
```
We are now done training our regression model and have the coefficients and intercept of our model. These can be put in our equation to find the find the line of best fit.we can use this to get unemployment percentage of any country when we have its government expenditure.

## Image 
Let us plot and see our line of best fit in the training set.

```python 
# Visualize the Train set line of regression line
plt.scatter(X_train, y_train, color = '#FF69B4')
plt.plot(X_train, regressor.predict(X_train), color = 'black')
plt.title('Unemployment vs Government expenditure (Training set)',fontsize =15)
plt.xlabel('Government Expenditure',fontsize =20)
plt.ylabel('Unemployment',fontsize =20)
plt.grid()
plt.savefig("UnempVsExpenditure.png")
plt.show()
```
## Model Evaluation
The aim of this step is to see how the model performs on unseen data. Often times algorithms perform well during training data and poorly when new data is used that is why it is important to evaluate the performance on the test set. if we are not satisfied with the results we iteratively to improve the performance. First, we use the inbuilt predict function to get the predicted values, get the mean square error and then compare the actual and predicted value.

```python
# Predicting the Test set results
y_pred = regressor.predict(X_test)
#mean squared error 
metrics.mean_squared_error(y_test, y_pred)
values = pd.DataFrame({'Actual': y_test.flatten(), 'Predicted': regressor.predict(X_test).flatten()})
values 
```
Let us visualize the actual values alongside the predicted to see how our model performs, discover any hidden patterns. From what we see our model doesn’t perform well.

```python 
df_error = values
df_error.plot(kind='bar',figsize=(16,10),color =["gray","pink"])
plt.grid(which='major', linestyle='-', linewidth='0.5', color='green')
plt.grid(which='minor', linestyle=':', linewidth='0.5', color='black')
plt.title("Actual and predicted values",fontsize =20)
plt.savefig("simple_actualpredicted.png")
plt.show()
``` 
## Image 

# Multivariate Linear Regression
Multivariate linear regression has many two or more features. In real-world situations, we usually use multivariate regression because many features have to be put into consideration. Many of the concepts here are the same the ones in the simple linear regression section with a few extensions so we won’t be going into much details on them.

Equation
## Image 
The hypothesis for multivariate linear regression is an extension of the simple linear regression.
Y =the predicted value.
W0 = bias term . this is the point where the line intercepts the y-axis.
W1,…..Wn are the parameters.
X1,…..Xn are the feature values.

For our problem, the distinct features are population penetration, internet usage and government expenditure. We can model it as follows.

## Image 
We have to add a bias term because even when there is no population growth, government expenditure and internet usage it will be hard for unemployment to be zero because there are other factors that influence like past government expenditure.


## Implementation
We shall use the previous data combined data with population and internet usage. We have to check data and see if each input feature is linearly related to the target value and remove some features that don’t.
We shall use the same sklearn linear regression class as before to train the regression model.

Let use import the necessary libraries and load the dataset.

```python 
#import the neccessary packages
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression

#load the dataset
m_df =pd.read_csv("combined_data.csv")
m_df.head()
```
## Image 

# Summarize Data
I did an analysis before and found out some features don’t contribute much to the performance of the model so let us drop them before we do the analysis. We shall remaining with three input features.
```python 
# delete less contributing features
m_df =X = m_df.drop(["Unnamed: 0",
       'Population\n (2018 Est.)',
       'InternetUsers\n 31-Dec-2017', 
       'InternetGrowth %\n2000 - 2017',
       'Facebook\n subscribers31-Dec-2017'], axis=1)
m_df.head()
``` 
## Image

### Descriptive statistics

In this section we are exploring the mathematical properties of our data set. We check for the data type of variables, get the dimension of the dataset and find the mean, median count and other statistical properties.
```python 
# check dimension of data
m_df.shape
(51, 5)
m_df.dtypes
CountryName                      object
GovExpenditurePerc                int64
UnemploymentPerc                  int64
InternetUsers\n 31-Dec-2000       int64
Penetration\n (% Population)    float64
dtype: object
# descriptions
m_df.describe()
# descriptions
m_df.describe()
```
## Image 
Data visualizations

This step is for us to get an idea of how our data is distributed. From the plots we shall be able to identify any outliers or skewness in our dataset.it is very hard to identify data in high dimension. In this section we are going to only plot histogram.

```python
# histograms
m_df.hist(color ="#FF69B4",alpha=0.5, figsize=(20, 10))
plt.savefig("multi_hist.png")
plt.show()
```
## Image 

We see outliers in almost all features. In this task we will only remove the government expenditure outlier. I encourage you to try and remove the rest and see if there is an improvement in how the regression model performance.
``` python 
# Remove the outlier rows
m_df = m_df.loc[m_df['GovExpenditurePerc'] < 80]
m_df.shape
(50, 5)
``` 
### Model training

We shall assign our x and y values then divide the data set into train and test set. because our features have different ranges we are going to normalize so it can have the same ranges.the normalization rescales values to ranges between 0 to 1.This helps speed the computation and the model is less sensitive to feature scale. Sklearn provides this functionality, all we need is to make normalize =True.

```python 
# x and y values
Y =m_df.iloc[:,2].values
X = m_df.drop(['CountryName', 'UnemploymentPerc'], axis=1).values

# Split the datas into the Train set and Test set
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, Y, test_size = 0.2,
random_state = 0)
# Fitt  Linear Regression to the Train set
from sklearn.linear_model import LinearRegression
regressor = LinearRegression(normalize=True)
regressor.fit(X_train, y_train)

#print weights and bias
print(regressor.coef_) # the coefficients
print(regressor.intercept_) # the intercept
[ 3.31007491e-01 -8.64072992e-06  7.37252335e-02]
-1.040968768854757
```

For clarity let use create a table with coefficients of the features so it is easy for us to feed in the equation.

```python 
#coeficients
x =m_df.drop(['CountryName', 'UnemploymentPerc'], axis=1)
coef =pd.DataFrame(regressor.coef_,x.columns,columns =["coefficient"])
coef
```
## Image 

# Model Evaluation
Let us evaluate and see how our model performs on unseen data.
```python
# Predicting the Test set results
y_pred = regressor.predict(X_test)
values = pd.DataFrame({'Actual': y_test.flatten(), 'Predicted': regressor.predict(X_test).flatten()})
values
```
## image 
```python 
df_error = values
df_error.plot(kind='bar',figsize=(16,10),color =["gray","pink"])
plt.grid(which='major', linestyle='-', linewidth='0.5', color='black')
plt.grid(which='minor', linestyle=':', linewidth='0.5', color='black')
plt.title("Actual and predicted values",fontsize =20)
plt.savefig("Multi_actualpredicted.png")
plt.show()
```
## Image 

# Conclusion
In this blog, we have looked at the basic linear regression model for both simple and Multivariate regression this involved how to make the predictions and how to evaluate our predictions. We have used the basic form of regression but there are other types of regression i.e Ridge regression, Lasso regression and ElasticNet regression. I encourage you to look at them and compare their performances using the evaluation metrics.  Simple data was used to do regression here but the same concept can be applied to complex datasets.

Thanks for reading and see you in the next blog.