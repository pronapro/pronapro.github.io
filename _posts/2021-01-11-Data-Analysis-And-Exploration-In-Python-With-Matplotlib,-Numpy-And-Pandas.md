---
layout: post
title:  "
Data Analysis And Exploration In Python With Matplotlib, Numpy And Pandas

"
date:   2021-01-11 16:01:15 +0300

---
## Image 
In this blog, we are going to cover the most commonly used data science libraries to do data analysis. The goal of this blog is to give you a brief on how to perform data analysis operations you are most likely to encounter. Data analysis is all about cleaning, manipulating and modelling in order to discover meaningful insights to guide in decision making. Data analysis step is an important one in order to build accurate models. Data scientist spend 80% of the project time doing data analysis before they even develop the algorithms/models.

### Prerequisite
I assume you are already familiar with python programing language. If you are not familiar with python  check out my guide on Python programming

You have a python environment already set up. I am using jupyter notebook to do the analysis and if possible to use it.

## Structure Of The Blog
We will first go through a crash course on NumPy, Pandas and Matplotlib before doing analysis on a real-world dataset.

## Dataset 
We shall be using two data sets which we shall merge together. The data sets are free so feel free to download them and follow along.

The datasets are:

Africa-2018-population-and-internet-users-statistics.csv
economic-data-africa.csv
The first  data set is from HDX

# Numpy
NumPy stands Numerical Python or Numeric Python. It is the library used to compute mathematical operations.It works effectively for arrays and matrices which are essential to most machine learning algorithms. In NumPy, dimensions are called axes. The number of axes is called the rank. Machine learning requires scientific calculations. Numpy has an optimized implementation of mathematical operations on arrays and matrices. Numpy has a ndarray which must-have elements of the same type. The 1-D array are vectors and two 2-D arrays are matrices.

By conventions, we import Numpy us np alias

Import NumPy as np

## NumPy Array Attributes
Ndim – displays the dimension of the array
Shape –  returns a tuple of integers indicating the size of the array
Size – returns the total number of elements in the NumPy array
Dtype – returns the type of elements in the array, 
Itemsize – returns the size in bytes of each item
Reshape: Reshapes the NumPy array
Creating A NumPy Array.
There are different ways to create NumPy arrays just as there’s more than one way to skin a cat. We can create arrays from lists and built-in functions.

Create array from list
```python 
# create numpy array from list
num =&#91;1,2,3,4,5]
num = np.array(num)
num
array(&#91;1, 2, 3, 4, 5])
``` 
A Numpy array transforms sequences of sequences into two-dimensional arrays, sequences of sequences of sequences into three-dimensional arrays, and so on. This means the depth of nesting creates dimensions.

```python 
#2 dimension array
import numpy as np
arr_2 =np.array([[1,2,3,4],[5,6,7,8]])
arr_2
#output
array([[1, 2, 3, 4],
       [5, 6, 7, 8]])
```
## Create From Built-In Methods
NumPy has functions to help us create array place holders in case we know the dimensions of the array we want to create but don’t have the data yet.

Create an array with zeros

We pass in the a tuple of dimensions of the array we want to create containing zeros. our example has dimension 3, 4 which means an array with 3 rows and 4 columns is created.

```python
# create array with zeros
num_0 = np.zeros((3,4))
num_0
#output
array([[0., 0., 0., 0.],
       [0., 0., 0., 0.],
       [0., 0., 0., 0.]])
```


Create a NumPy array with ones.

Similar to create with zeros in such a way that only array dimensions are needed  
```python 
Create a NumPy array with ones
# create NumPy array with ones takes in the shape of the array to be created (rows, columns)
# create numpy array with ones
num_1 =np.ones((4,4))
num_1
array([[1., 1., 1., 1.],
       [1., 1., 1., 1.],
       [1., 1., 1., 1.],
       [1., 1., 1., 1.]])
``` 
Create an  array with any number of choice

Full method takes in the a tuple of dimensions and the number we want to populate the array with as arguments.
```python
num_choice = np.full((3,4),6)
num_choice
array([[6, 6, 6, 6],
       [6, 6, 6, 6],
       [6, 6, 6, 6]])
```
arange function

arange method is like the range function in python lists. its syntax is (start, end, step). the drawback of this method is you always have to know the step.
```python 
# create array from a given range
num_range = np.arange(2,20,2)
num_range
array([ 2,  4,  6,  8, 10, 12, 14, 16, 18])
```  
### linspace 

Creates linearly spaced arrays at a given interval, the syntax is (start, stop, number of points). This solves the problem of not knowing the step due to the difficulty of calculating the step off head working with floats and large numbers.
```python
arr_lin = np.linspace(1, 5, 10) 
arr_lin
#output
[1.         1.44444444 1.88888889 2.33333333 2.77777778 3.22222222
 3.66666667 4.11111111 4.55555556 5.        ]
```
## Accessing Array
We access elements of an array using their index. we can access values at an index or at a range of values. The syntax for indexing 2D array is arr[row][column] or arr[row, column] choose one and stick to it. The former can be modified to arr[rowstart_index:rowend_index, columnstart_index: columnend_index] to work with ranges.
```python 
Accessing the first element of an array.
arr_lin[0] 
Accessing elements of a two-dimension array
#first element, first row and third column
Arr_2[0,2]
```

Negative indexing

Negative indexing starts from the last element/ end. We use negative indexing when we want to get arrays from the bottom. the syntax is the same to the above though we add negative signs to the index.

## Slicing
Slicing means taking a given section of an array using indexes. A slice contains a start and end index plus an optional step. The returned array includes the start index but excludes end index
```python 
# slice
num[1:3]
array([2, 3])
# we can slice from a given index to an end using
num[1:]
array([2, 3, 4, 5])
# slice from start to a iven index
num[:3]
array([1, 2, 3])
#negative slicing. slice from index one from the 
num[-4:-1]
array([2, 3, 4])
#slicing multidimensional array
num_rand[0,0:2]
array([0.64028572, 0.91023538])
```

## Data Types
The array has the following data types. integer, float, string, boolean, DateTime, Unicode string, etc. It is vital for us to know the data types of our array. We can check the data type of an array using .dtype.You can create an array with a defined data type. You can also convert the data type of an existing array using astype.

```python 
#checking data type
num.dtype
dtype('int64')
str_value =np.array(["array","python","pandas"])
str_value.dtype 
dtype('<U6')
#creating array with defined data type
arr = np.array([2, 4, 8, 16], dtype='S')
arr.dtype
dtype('S2')
#converting array to another data type
​
to_int = arr.astype(int)
to_int.dtype
dtype('int64')
```
## Shape And Reshaping 
This is the changing of the shape of an array. The shape represents the number of items in each dimension. When we reshape we either add or remove the number of items in each dimension while leaving the elements of both arrays be the same. Reshape from one dimension to two. We can reshape to any dimension if values needed for reshaping are equal in both shapes.
```python
# reshape from one dimension to two
arr1 =np.array([1,2,3,4,5,6,7,8,9,10])
new_arr1 = arr1.reshape(5, 2)
new_arr1
array([[ 1,  2],
       [ 3,  4],
       [ 5,  6],
       [ 7,  8],
       [ 9, 10]])
```

Reshape to 1-D array

This is converting array from n-dimension to one dimension. It is referred to as flattening. We use reshape(-1) or ravel methods to flatten arrays of any dimension.
```python
# flattening array
new_to_int = to_int.reshape(-1)
new_to_int
array([ 2,  4,  8, 16])
#we can also flatten an array using ravel
new_arr1.ravel() 
array([ 1,  2,  3,  4,  5,  6,  7,  8,  9, 10])
```

## Copying Array
If we create an array from an existing array, the new array will be in view mode and when you change something in the new array the modifications will also apply to the first array. this is so to avoid memory problems. To copy an array we use copy method to prevent modifications in the new array affecting the original array and vice versa
```python
# without copy function
new_array = num
new_array
array([1, 2, 3, 4, 5])
new
new_array[0] = 20
new_array
array([20,  2,  3,  4,  5])
num
array([20,  2,  3,  4,  5])
```

let us create one where we copy the function and see how it behaves
```python 
# with copy
​
num_copy = num.copy()
num_copy
array([20,  2,  3,  4,  5])

num_copy[0] =6
num_copy
array([6, 2, 3, 4, 5])

num
array([20,  2,  3,  4,  5])
``` 


## Array Operations
Numpy arrays can perform basic math operations like addition, multiplication, subtraction, division matrix dot product, element-wise division.

Universal array functions

Numpy has universal functions that carry out some tasks for like square root, exponential, trigonometry sin and cos, logarithm. mean, min, max, sum, product, transpose etc.

# Pandas
Pandas is a package for data manipulation and analysis in Python. Pandas has two main data structures. Series and data frame

Series
Series are like 1-dimensional object built on top of numPy objects that can hold many data types. Series can be given labels at each index 

Series data has Shape, Size, Values, index,Ndim attributes

By conversion, we import pandas as pd.

Import pandas as pd

### Creating A Series
We can create a series from a list as follows. the difference between numpy array and series is series have labels.Without specifying the index labels the index become the labels
```python 
num = [0, 2, 4,6,8,10]
num_s = pd.Series(num )
num_s
0     0
1     2
2     4
3     6
4     8
5    10
dtype: int64
```
Create with labels

We use the label argument of the series method to add labels. the labels should be the same length as the series.
```python 
## create labels
num = [0, 2, 4,6,8,10]
num_index =["first","second","third","fourth","fifth","sixth"]
num_s = pd.Series(num, index =num_index )
num_s
first      0
second     2
third      4
fourth     6
fifth      8
sixth     10
dtype: int64
```
Create a series from a dictionary

A dictionary stores information in key-value format. We can create a series with labels using a dictionary.
```python 
# create with dictionary
num_d = {"first":2,"second":4,"third":8,"fourth":16}
num_d =pd.Series(num_d)
num_d
```
Dataframe
Dataframes are multidimensional like tables in excel with many rows and columns.you can think of dataframe as a collection of series.

Create dataframe

We create from a dictionary
```python 
## create from dictionary
people ={"names":["High","Mark","Micheal","carr"],
         "ages":[12,32,24,30]}
people=pd.DataFrame(people)
people

names	ages
0	High	12
1	Mark	32
2	Micheal	24
3	carr	30
#access with loc
people.loc[0]
names    High
ages       12
Name: 0, dtype: object
```
Adding indexes

We can add an index to the dataframe using index argument. We can also reset the index of the dataframe using reset people.reset_index().set_index(“ages”). The axis dimension have indices, 0 for vertical dimension and 1 for horizontal

```python
# add index
people ={"names":["High","Mark","Micheal","carr"],
         "ages":[12,32,24,30]}
p_index =["first","second","third","fourth"]
people=pd.DataFrame(people, index =p_index)
people
 
names	ages
first	High	12
second	Mark	32
third	Micheal	24
fourth	carr	30
```
## Access Values
We access values using either dictionary or object notation. To add new columns we dictionary notation to avoid creating a new dataframe. To access more than one column we use a dictionary notation and pass in a list of columns we want to access.
```python 
# dictionary  notation
people["names"]
Out[220]:
first        High
second       Mark
third     Micheal
fourth       carr
Name: names, dtype: object
In [222]:
# using object notation
people.ages
Out[222]:
first     12
second    32
third     24
fourth    30
Name: ages, dtype: int64

#access multiple columns
df[["col_1","col_2"]]
```
## Selecting Row
We select row using loc or iloc. loc takes in the index while iloc selects based on position instead of label.
```python 
# select row using loc
people.loc["fourth"]
names     carr
ages        30
amount       0
Name: fourth, dtype: object
2
# select row using iloc
people.iloc[2]
names     Micheal
ages           24
amount          0
Name: third, dtype: object
```
Select rows and columns

we can select specific rows and columns using loc. syntax loc[“row”, “column”]

```python
people.loc["second","ages"]
# select both row and column
people.loc["second","ages"]
32
#select more rows and columns
people.loc[["second","fourth"],["ages","names"]]
ages	names
second	32	Mark
fourth	30	carr
``` 
Set Index
We can set the index of a dataframe using set_index method and pass in the column of the dataframe we want to use. If there is an index already we use reset_index first and then set_index.

```python 
people.reset_index().set_index("ages").head()
index	names
ages		
12	first	High
32	second	Mark
24	third	Micheal
30	fourth	carr
``` 
Look At The Data
We use the head method to look at the top rows of the dataset and tail to look at the bottom rows. by default, they return 5 rows but you can give a number of rows you want to return

```python
people.head(2)
names	ages
first	High	12
second	Mark	32
people.tail(2)
names	ages
2	Micheal	24
3	carr	30
```
Assign value to columns

we can assign one value to all cells of a column using dictionary notation.


```python
people["amount"] =0
people
names	ages	amount
first	High	12	0
second	Mark	32	0
third	Micheal	24	0
fourth	carr	30	0
```
Checking columns and index

we can also check to see the column values and row values as follows.

#checking columns and rows
​

```python
#checking columns and rows
​
people.index.values
array(['first', 'second', 'third', 'fourth'], dtype=object)
 
people.columns.values
array(['names', 'ages', 'amount'], dtype=object)
```
Conditional selection

We select rows basing on column condition using comparison operators like >,<,==,!= etc. we use | and & to combine multiple conditions.

```python 
## select based on condition
#people[people['ages'] > 25] 
#Select using loc method
young =people.loc[people['ages'] < 25]
​
young
names	ages	amount
first	High	12	0
third	Micheal	24	0
​
# return one column 
young =people.loc[people['ages'] < 25]["ages"]
young
# return one column 
young =people.loc[people['ages'] < 25]["ages"]
young
first    12
third    24
Name: ages, dtype: int64
# return selected columns
# return one column 
young =people.loc[people['ages'] < 25][["ages","amount"]]
young
ages	amount
first	12	0
third	24	0
#Select basing on multicolumn condition
older_broke = people.loc[(people['ages'] >25) & (people['amount']<=0)]
older_broke
names	ages	amount
second	Mark	32	0
fourth	carr	30	0
​```
Handling Missing Values
In a real application, data is always missing for a number of reasons. When this happens we have to find a way of handling it. missing values are called nans and we can identify them using pandas.

Deleting missing values

We can drop all missing values

We delete using dropna function. We can remove partially using how =” any” or all using how=” all”  to modify the dataframe we use parameter inplace =True

Imputing missing values

We can replace the nan values with others instead of just discarding the row or column containing them. We can use fillna to fill values nan values. It takes in a value you are going to impute with

fillna(val)

We can also impute using statistical methods like mean, median and mode

Replace values

You can replace one value with other values 

Remove values

You can remove rows that do not satisfy a certain condition.


```python 
for x in people.index:
  if people.loc[x, "ages"] > 25:
    people.drop(x, inplace = True)
people
people
names	ages	amount
first	High	12	0
third	Micheal	24	0
```
Remove Duplicates
Sometimes due to combining data or human errors, data can have duplicates that we need to identify and remove

Identifying duplicates. We use duplicated function which returns a boolean value true if the row is duplicated.

```python 
people.duplicated()
first    False
third    False
dtype: bool
```
Removing duplicates

people.drop_duplicates(inplace = True)

Use (inplace = True) if you want the original to be modified

### Combining Data
When you have data from different sources as it is in most cases, you may it is better to combine them to do analysis and exploration once. This helps in seeing things like correlation.

We combine data frames using merge. By default, merge does it by index but you can specify the key to use in merging data. When two data frames share a column then we can merge then using that key otherwise we assign keys to merge on.

```python 
df = pd.merge(df_left, df_right, on="key")
df = pd.merge(df_left, df_right, left_on="key_left", right_on="key_right")
```
### Descriptive Statistics
Pandas has functions like mean, sum, max, min, mode that are the most used statistical methods. They take on optional parameters skipna which is true by default and specifies that nans are skipped/excluded and axis which that direction to follow vertical or horizontal
Creating column values with a mean of other values
```python 
col = df.loc[: , "column_1":"column_3"]
df['column_mean'] = col.mean(axis=1)
```
# Matplotlib
Matplotlib is a plotting library used for data visualization.

We import it under plt alias

import matplotlib.pyplot as plt

We plot using plot() which by default draws a line.Plot takes in x -axis(horizontal)and y-axis(vertical) coordinates
```python 
x = range(10) # Sequence of values for the x-axis
y = [x1+3 for x1 in x]
​
plt.plot(x, y) 
plt.show()
```
## Image 
### Multi Plots
You can also plot many plots once
```python
x = range(10) # Sequence of values for the x-axis
y = [X+3 for X in x]
y2 =[X**2 for X in x]
plt.plot(x, y) 
plt.plot(x, y2)
plt.show()
```
### Limiting The Axis
We can set limits for x and y axis  using xlim(xmin, xmax) and ylim(ymin, ymax) functions. 

### Adding Labels, Title
For our plots to make meaning to other people, it is important we add labels to the x, y-axis and title.

```python 
x = range(10) # Sequence of values for the x-axis
y = [x1+3 for x1 in x]
​
plt.plot(x, y)
plt.xlabel('x sequence to 10')
plt.ylabel('y sequence x+3')
plt.title("plot of x+3 against x")
plt.show()
```
### Adding Legend When We Have Many Plots
In situations where we have many variables we are plotting so we should add legends to do so.

```python 
x = range(10) # Sequence of values for the x-axis
y = [X+3 for X in x]
y2 =[X**2 for X in x]
plt.plot(x, y, "-b", label ="x+3")
plt.plot(x, y2, "-r",label ="x**2")
plt.legend(loc="upper left")
plt.xlim(0, 8)
plt.show()
```
## Image 
### Saving Plots 
We can save our plots in many formats which we can later share with others

```python 
plt.savefig('legend.jpg')
```
### Styling
Colour code:

We can style our plots using different colours using c or colour parameter

b = Blue
c = Cyan
g = Green
k = Black
m = Magenta
r = Red
w = White
y = YellowPie Chart

### Markers
We use markers to emphasis points on the plots. You can specify marker size using ms. Change marker edge colour using mec . Fill marker colour using mfc parameter.

```python 
#markers
x = range(10)
y = [X+3 for X in x]
y2 =[X**2 for X in x]
plt.plot(x, y, marker ="*", ms =15)
plt.plot(x, y2, marker ="o",mec = 'r')
plt.show()
```
## Image 
### Line Styles
Use line style or ls to change the style of the line to one of the following
– Solid line
— Dashed line
-. Dash-Dot line
: Dotted Line


```python 
#line style
x = range(10)
y = [X+3 for X in x]
y2 =[X**2 for X in x]
plt.plot(x, y, linestyle ="dotted")
plt.plot(x, y2,linestyle ="dashed")
plt.show()
``` 
## Image 
### Line Width
We can change the width of the line using linewidth 

You can also set the font, background colour, the scale of plots etc.
```python 
x = range(10) # Sequence of values for the x-axis
y = [x1+3 for x1 in x]
plt.plot(x, y, linewidth =10, color ="maroon")
plt.show()
```
Subplots
Display multi plots on one figure. We use subplots function which takes three arguments. The first represents rows, second columns and the third shows the index of the current plot.

plt.subplot(1, 2, 2) # there is one row, two columns and this is the second plot

We add the main title to all plots using plt.subtitle(“Main Title”)

Types Of Plots
Matplotlib provides many types of plot formats for visualising information

1. Scatter Plot
2. Histogram
3. Bar Graph

Case Study
Read The Data 
We shall be using two datasets. one economic data and another internet usage in African countries. Read the two data sets using panda’s read_csv method.

Import libraries we are to use
```python 
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```
Look at the data

We shall look at the structure of each dataset before combining them

Take a look at the data using head and tail

Head by default lets us see the first 5 rows of the data set and tail lets us see the last 5 rows. you can add any number you want to view
``` python 
# let use read in our data
# economic data showing government expenditure and the unemployment rate
econ = pd.read_csv('economic-data-africa.csv', sep=';', encoding='ISO-8859-1')
#internet usage dataset
apis = pd.read_csv("africa-2018-population-and-internet-users-statistics.csv")
In [3]:
# lets take alook at the data
#lets start with economic data
econ.head(5)


CountryName	GovExpenditurePerc	UnemploymentPerc
0	Algeria	42	11
1	Angola	32	7
2	Benin	22	1
3	Botswana	35	18
4	Burkina Faso	23	3

# internet usage data
apis.head()
	AFRICA	Population\n (2018 Est.)	InternetUsers\n 31-Dec-2000	InternetUsers\n 31-Dec-2017	Penetration\n (% Population)	InternetGrowth %\n2000 - 2017	Facebook\n subscribers31-Dec-2017
0	Algeria	42,008,054	50,000	18,580,000	44.2 %	37,060 %	19,000,000
1	Angola	30,774,205	30,000	5,951,453	19.3 %	19,738 %	3,800,000
2	Benin	11,458,674	15,000	3,801,758	33.1\n%	25,245 %	920,000
3	Botswana	2,333,201	15,000	923,528	39.6\n%	6,057 %	830,000
4	Burkina Faso	19,751,651	10,000	3,704,265	18.8\n%	36,942 %	840,000
```
Merge Data Sets
For proper handling of the data, we are going to join/merge it. We shall use keys that are common, that is the countries.

We see that the data set has different length hence it is wise to merge by key instead of index.

Before we merge based on the countries we look at the cames to make sure they are the same and if not correct them.

In our dataset, we can see congo, republic of congo, South Africa and all two and more part names are written differently.

Let us create a dictionary containing names we want to replace in our dataset.
```
names ={'Cabo\n Verde':'Cabo Verde', 'Central African Rep.':'Central African Republic',
 'Congo,\n Dem. Rep.':'Congo, Democratic Republic of the Congo',
 'Congo':'Congo, Republic of',
 "Cote\n d'Ivoire":"Côte d'Ivoire",
 'Sierra\n Leone':'Sierra Leone',
 'South\n Africa':'South Africa',
 'Sao\nTome & Principe':'São Tomé and Príncipe'}
 ```
 ```python 
 apis = apis.set_index("AFRICA")

apis =apis.rename(index =names)

apis =apis.reset_index()

#merge the data set with the internet usage data set
all_data =pd.merge(econ, apis, left_on="CountryName", right_on="AFRICA")

all_data.head()
```
### Removing Irrelevant Features
If we take a peek at the data we see that the countries appear in three rows. So let’s remove the other rows because they are not significant. We delete the data using del
```python 
# let us drop the Africa column since the values are the same as the country name
del all_data["AFRICA"]

First, we shall first check the columns that exist in the dataframe
# let us check the datatype of our column data
all_data.dtypes

CountryName                          object
GovExpenditurePerc                    int64
UnemploymentPerc                      int64
Population\n (2018 Est.)             object
InternetUsers\n 31-Dec-2000          object
InternetUsers\n 31-Dec-2017          object
Penetration\n (% Population)         object
InternetGrowth %\n2000 - 2017        object
Facebook\n subscribers31-Dec-2017    object
dtype: object
```
Cleaning the data

When cleaning data we try to look for 

Empty cells
Data in the wrong format
Wrong data
Duplicates
checking data types we see that we have object data types for columns except for government expenditure and unemployment that are integers

We also see that some columns have percentages and escape sequences(\n) in them plus commas which will make it hard for us to convert to integers since the fields are numbers and we will have to do some statistics on them.

```python 
#we see that the values are in strings so let us convert them to appropriate types
# we first convert the data to string then look for , character and remove it
all_data =all_data.astype('str')
all_data =all_data.apply(lambda x: x.str.replace(',', ''))

# let us also remove the % sign
all_data =all_data.astype('str')
all_data= all_data.apply(lambda x: x.str.replace('%', ''))
​

# let us also remove the escape character
all_data =all_data.astype('str')
all_data =all_data.apply(lambda x: x.str.replace('\n', ''))
​

all_data["Penetration\n (% Population)"] = all_data["Penetration\n (% Population)"].astype(float)

all_data[['GovExpenditurePerc', 'UnemploymentPerc','Population\n (2018 Est.)', 'InternetUsers\n 31-Dec-2000','InternetUsers\n 31-Dec-2017','InternetGrowth %\n2000 - 2017','Facebook\n subscribers31-Dec-2017']] = all_data[['GovExpenditurePerc', 'UnemploymentPerc','Population\n (2018 Est.)', 'InternetUsers\n 31-Dec-2000','InternetUsers\n 31-Dec-2017','InternetGrowth %\n2000 - 2017','Facebook\n subscribers31-Dec-2017']].apply(pd.to_numeric)
all_data.dtypes

GovExpenditurePerc                     int64
UnemploymentPerc                       int64
Population\n (2018 Est.)               int64
InternetUsers\n 31-Dec-2000            int64
InternetUsers\n 31-Dec-2017            int64
Penetration\n (% Population)         float64
InternetGrowth %\n2000 - 2017          int64
Facebook\n subscribers31-Dec-2017      int64
dtype: object
``` 
all_data.describe() is used to view some basic statistical details like percentile, mean, std etc. of a data frame or a series of numeric values.

## Handling Outliers
Plotting to scatter plot we see there is an outlier

Our outliers are government expenditure in Libya and the population in Nigeria is higher than in other areas.
```python 
all_data.plot(kind ="scatter" ,x ="GovExpenditurePerc", y ="UnemploymentPerc")
```
## Image 
```python 
all_data.plot(kind ="scatter",x ="Population\n (2018 Est.)",y ="UnemploymentPerc")
```
## Image 

## Feature  Engineering
Feature engineering is all about extracting more information from our data. The two common ways of doing feature engineering are creating new variables or transforming the ones we already have.

We used a correlation matrix to see how features are related to each other or our target.

We see a correlation between internet users and facebook subscriptions. so we shall drop the two columns and have one. Irrelevant features can decrease the accuracy of our model.

```python 
import seaborn as sns
f, ax = plt.subplots(figsize=(10, 8))
corr = all_data.corr()
sns.heatmap(corr, mask=np.zeros_like(corr, dtype=np.bool), cmap=sns.diverging_palette(220, 10, as_cmap=True),
           square=True, ax=ax)
```
## Image 
There is a correlation between population and internet growth,  government expenditure and unemployment which we can look further into.

Since we don’t have any missing values and duplicates we can proceed with data transformation and use in any machine learning algorithm model.

## Conclusion
I hope that you have learned something new in this blog. We have looked at how data analysis helps us have a basic understanding of each variable, the relationship between them, the important variables etc. we also looked at the three most used python libraries i.e Pandas is an important library that helps us do the manipulation, Matplotlib helps us do the visualization and Numpy helps with vector and matrix operations. In our next blog, we shall try to build a machine learning algorithm on the clean data to make some predictions so stay tuned.




