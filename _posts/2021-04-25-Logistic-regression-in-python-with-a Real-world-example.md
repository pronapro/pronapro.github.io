---
layout: post
title:  "
Logistic Regression In Python With A Real-world Example
"
date:   2021-04-25 16:01:15 +0300
categories: jekyll update
---
# Introduction
Imagine you want to apply to a school, for a visa or maybe you are eyeing a promotion somewhere and don’t want to waste your money and time on things you won’t get. Assuming they work on people based on a first come first serve basis so you have an idea and collected data of people’s results. You are wondering if there is a way to check if your outcome is going to be a  positive or a negative one. And are wondering how you are to do that. The data you collected is a lot so you cant manually work with it. you can use logistic regression to solve such a problem.
The objective of this blog is to make you understand how to implement logistic regression using python. The data we are using is Graduate admission data and we shall be using the sklearn library to do the regression, matplotlib and seaborn for visualization and pandas to do the analysis.

# Logistic Regression
Even though it has a name regression, Logistic regression is a classification algorithm. It is a supervised machine learning algorithm meaning the data has to be labelled.
Logistic regression is different from linear regression in such a way that linear regression is about predicting continuous values while logistic regression predicts discrete values. For our admission example. Linear regression predicts the percentage chance of getting admission while logistic predict if you will be admitted or rejected.
The main goal of the algorithm is to estimate the parameters/coefficients of an equation that best describes the data we have.

## Application
Logistic regression is used when the target variable is a discrete value/categorical, for example,
1. spam or not spam.
2. a student will be admitted or rejected, 
3. someone has a disease or not.
4. handwriting recognition to predict the target number

## Types Of Logistic Regression
Logistic regression can be binomial, ordinal or multinomial.

### Binomial Logistic Regression
Binomial also called binary logistic regression is used when our target value has two outcomes/categories for example with graduate admission you can either be accepted or rejected, another example is getting visa approval, or if an email is a spam or not spam.

### Ordinal Logistic Regression
Used when the target value has three or more outcomes with a natural ordering. The values are usually non-mathematical values such as frequency, satisfaction etc
An example is how one is satisfied with a given course they were admitted to. They can be:
1. Very Unsatisfied
2. Unsatisfied
3. Neural
4. Satisfied
5. Very Satisfied

### Norminal Logistic Regression
Used when the target value has three or more outcomes with no natural ordering. It is used with survey data where only variable classes are important. An example is a survey of courses students want to be applied to.

What course are you interested in?

1. Computer science
2. Machine learning 
3. Data science

## Equation
If you are to recall the equation of a straight line is y =mx+b, we use the sigmoid function to transform the data to have a value between 0 and 1.
Model
Output = 0 or 1
Hypothesis => z = mx + b
p(x) = sigmoid (z) this can be represented as:

# image 
When we plot the hypothesis values and values after applying sigmoid we get the graph below:

# image 
As z tends infinity, predicted will become 1 and predicted value will become 0 as z tends to negative infinity

### Decision Boundary
If we have two classes we have to get two haves to do this we decide to get a threshold to help us with as a decision boundary. A number below it is rounded to zero and numbers above it becomes 1. The commonly used decision boundary is 0.5. Values below it such as 0.4,0.3,02 become 0 and values above it such as 0.6, 0., 0.8 become 1.

## Cost Function
We use the cost function to estimate the coefficients of the function. Our goal is to minimize it to improve the accuracy by finding m and b for which error is minimum.
The value m moves stretches the s-curve and b moves it left or right which curve the shape the s curve will take. The shape of the curve should be one that fits most of the data accurately.Like with linear regression, logistic regression handles many variables.
Estimating coefficients
For each training
1. Calculate target value using the values of your current parameters
2. Calculate new parameter values basing on the error in the prediction
Repeat 1-2 until the model gives an accurate performance

We use maximum-likelihood estimation to estimate the coefficients of the model. If we are dealing with two classes the best coefficients would result in a model that would predict a value very close to 1 for the default class and a value very close to 0 for the other class.
Ypred is the predicted value.

# images 

## Model Evaluation
To evaluate our model we have to have a metric to help us know how well our model performs. In this post, we will use two types of evaluation metrics. Accuracy and confusion matrix.

Confusion Matrix
We will also use a confusion matrix to help us know how well it performs and misclassifies classes. A confusion matrix is also easy to understand.
It’s a table with NxN dimension where N is the number of outcomes. In our example, we have two outcomes hence 2×2.

# image 

True positive(TP): Predicted True and actual is True.
True negative(TN): Predicted False and actual is False
False positive(FP): Predicted True and actual is False
False negative (FN): Predicted False and actual is True Accuracy

### Accuracy 

The accuracy metric tells us how well our model performs. This is the percentage of classes that were not correctly classified.
# image 
#### Misclassification rate (MR)

This is the percentage of classes that were not correctly classified.

# Implementation
We are going to implement logistic regression using Graduate admission data from Kaggle. Our target value should be admitted(1) or rejected(0).our data has the following attributes ‘Serial No.’, ‘GRE Score’, ‘TOEFL Score’, ‘University Rating’,’SOP’, ‘LOR ‘, ‘CGPA’, ‘Research’, ‘Chance of Admit ‘.

Let us import the necessary libraries.

```python 
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.linear_model import LogisticRegression
from sklearn.ensemble import ExtraTreesRegressor
from sklearn.model_selection import train_test_split
``` 
Now that we have the necessary packages, let us explore the data to see if it is in the format we need and if it is not looking at it helps us know where we should modify.
```python 
df = pd.read_csv("Admission_Predict.csv")
df.head()
``` 
# image 

Descriptive statistics

Let us explore and see the characteristics and distribution of the data. let us use pandas functions. finding the distribution is important if we want to do future engineering in the data or know which features are not that important.

```python 
##Descriptive statistics
df.shape
#output 
(400, 9)

#data types 
df.dtypes
#output 
Serial No.             int64
GRE Score              int64
TOEFL Score            int64
University Rating      int64
SOP                  float64
LOR                  float64
CGPA                 float64
Research               int64
Chance of Admit      float64
dtype: object
```
From df.shape, we can see that the data has 400 columns and 9 rows. you can also find the statistical properties of the data for example mean, median, sum, min, max of the different features using df.describe().

# Feature Engineering
we want to predict the outcome of an application that is to say if someone was admitted or rejected. we can see in our data that we dont have that. we are going to use the Chance of Admit column to create that. the process of creating a new feature is called feature engineering.we assume 75% is the decision boundary. chance of admit less than or equal to 0.75 is 0 and greater than 0.75 is a 1.

```python 
df['Decision']= np.where(df['Chance of Admit ']<=0.75,0,1)
print(df['Decision'].value_counts())
df.sample(5)
#output 
0    228
1    172
Name: Decision, dtype: int64
```
# image 

0 represents a rejection and 1 an acceptance. From the output, we see that our data has 228 rejections and 172 acceptances.

We will not be using the Serial No and Chance of Admit columns so let us drop them.let us also check if the columns we will be have any null values.

```python 
#drop series NO  and Chance of Admit column 
df = df.drop(['Serial No.','Chance of Admit '], axis=1)

#check for null values 
df.isnull().sum()
#output
GRE Score            0
TOEFL Score          0
University Rating    0
SOP                  0
LOR                  0
CGPA                 0
Research             0
Decision             0
dtype: int64
```
For data exploration, we can also check how the features are closely related or influence others using correlation matrix. let us visualize the correlation using seaborn
```python 
sns.heatmap(df.corr())
```
# image 
We can also plot to visualize the distribution of the different features. in my example, I am going to plot the research column and university rankings. you can plot for other features that I haven’t plotted.

```python 
#research  count
sns.countplot('Research',data=df)

#university ranking count
p=sns.countplot(x='University Rating',data=df)
p.set_xticklabels(p.get_xticklabels(),rotation=90)
plt.title('Count of University Rating')
```
Let us also do a comparison and see things like how many people with research papers were accepted compared to those without. we will also plot the admission numbers according to the different rankings of schools. I am not plotting for every feature so you can do that if you are curious to see the trend.
```python 
#admission by school
sns.countplot(df['Decision'], hue ='University Rating',data =df )
#admission by research
sns.countplot(df['Decision'], hue ='Research',data =df )
```

## Feature Importance

We deleted the serial number and chance of admit features from the data because they were not important to our problem. we were able to do that because our data has few features hence we were able to see that but in cases where we have many features that is a hectic way of doing it. we can check feature importance using sklearn to save time . we can clearly see that CGPA is the most important key for getting Admission followed by the TOEFL score.
```python 
model = ExtraTreesRegressor() 
model.fit(df.iloc[:,:-1],df.iloc[:,-1])

feat_impt = pd.Series(model.feature_importances_, index = df.iloc[:,:-1].columns) 
feat_impt.nlargest(7).plot(kind='barh')
plt. title("Rank of Feature Importance")
plt.show()
``` 
# Model Training
Let us train the logistic regression model now that we are done exploring the data, cleaning it and making sure it has the features we need to use. we are going to assign the x and y values , divide the data into test and train datasets, instantiate the regression model then train.
```python 
# assign x and y values
X=df.drop(columns = ["Decision"])
y=df["Decision"]
# divide data into rain and test sets 
X_train,X_test,y_train,y_test=train_test_split(X,y,test_size=0.25,random_state=42)
# model instatiation and training 
model = LogisticRegression()
model.fit(X_train, y_train)
``` 
## Model Evaluation
Let us evaluate using Accuracy and confusion matrix
```python 
#Accuracy score
score =model.score(X_test,y_test)
print(score)
#output
0.88
# get predictions on test data
predictions =model.predict(X_test)
#comfusion matrix
cm = metrics.confusion_matrix(y_test, predictions)
print(cm)
#output
[[52  8]
 [ 4 36]]
 ```
 We have an accuracy of 88% and 12 misclassifications in our test data. 8 false negatives and 4 false postives. we can visualize the confusion matrix.

```python 
plt.figure(figsize=(9,9))
sns.heatmap(cm, annot=True, linewidths=.5, square = True, cmap = 'Blues_r');
plt.ylabel('Actual label');
plt.xlabel('Predicted label');
all_sample_title = 'Accuracy Score: {0}'.format(score)
plt.title(all_sample_title, size = 15);
``` 
## Conclusion
In this blog, we have learnt about logistic regression and how to implement it. We used a binary classification example and the same concepts we have looked at in this post can be extended to multiclassification problems. The great thing about logistic regression is it doesn’t require much computing time and recourses hence making it easy to deploy and use it in production.
Thanks for taking the time to read see you in the next blog.




