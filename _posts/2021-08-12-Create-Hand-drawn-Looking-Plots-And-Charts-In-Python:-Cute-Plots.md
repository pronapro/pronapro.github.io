---
layout: post
title:  "
Create Hand-drawn Looking Plots And Charts In Python: Cute Plots

"
date:   2021-08-12 16:01:15 +0300
categories: jekyll update
---


Visualization is the best way to summarize data. It helps identify patterns and outlines. It also helps break down complex things, quantifies things that help to effectively communicate the information. 
The format you represent this data depends on your audience and what you are trying to pass on. Sometimes you just want to have something cute.

In this post, we shall be looking at how to do hand drawing looking plots using python. We are going to look at the most common plots that are to say line plot, scatter plot, piechart, barplot.  
We are going to be using matplotlib and cutecharts package. You can pick one that you find interesting. cutecharts has the capability of making interactive and dynamic charts, its only limitation is it only works with four kinds of plots at the moment that is to say  Bar, Line, Pie, Radar and Scatter.


We are going to be using matplotlib xkcd() 
First import matplotlib. Then create the data we are going to be using and create a dataframe. Let use just create random data but feel free to follow along with your dataset. 


let us install the necessary packages


```python
pip install cutecharts
pip install matplotlib
```

After installing the packages, let us import the packages we will be using.pandas will be used to create dataframes since the visualization packages data that is in that format. matplotlib and cutecharts are the packages we will use for our visualization.


```python
import pandas as pd 
import matplotlib.pyplot as plt 
import numpy as np 
import cutecharts.charts as ctc

```

let create a matplotlib object using xkcd so the hand drawn format can be applied to all our plots. 


```python
plt.xkcd()
```

## Bar graph 
let us start with bar graph. I just created a ramdon dataset containing age, score and names. you can use any dataset you have and follow along to this example. 
Bar graphs can help make comparisons,we can also spot outliers.

### Bar plot using matplotlib
The plots look like they are hand drawn. You can also can color.


```python
age  = [20, 19, 40, 22, 16, 30, 19]
score = [70, 50, 80, 80, 36, 75, 55]
name  = ['Mary', 'Jone', 'Anne', 'Mark', 'Roy', 'Eric', 'Ink']
df = pd.DataFrame({'Age': age,  'Score': score}, index=name)

plt.rcParams['figure.figsize'] = [12, 8]
# This figure will be in XKCD-style
fig1 = plt.figure()
ax = df.plot.bar()
ax.set_title("Grades")
ax.set_xlabel("Names")
ax.set_ylabel("Percentage score")
```  
![Barplots](/img/posts/cuteplots/barplot.png)
    


### Bar plot using cutecharts 
This is more dynamic and interactive compared to the one using matplotlib. the output is an html file which is saved in our working directory. 


```python
chart = ctc.Bar('Grades', width='500px', height='400px')
chart.set_options(
    labels=list(df.index.values),
    x_label='Names',
    y_label='Percentage score' ,
    colors=['#c1e7ff' for i in range(len(df))]
    )
chart.add_series('Score', list(df['Score']))
chart.render()
```

<iframe src ="/htmlembed/barplot.html" width ="100%">
</iframe>

## scatter plot 
scatter plots help us display relationships between variables. the data points are represented as dots or circles. 


```python
#df.reset_index(drop=True)
fig1 = plt.figure()
ax = plt.scatter(x=df.Age.values, y=df["Score"].values)
plt.title("Grades")
plt.xlabel("Age")
plt.ylabel("Percentage score")
```  
![png](/img/posts/cuteplots/scatterplot.png)
    


## Line plot
A line plot helps display trends of variables over time.


### Line plot using matplotlib


```python
#markers
x = range(10)
y = [X+3 for X in x]
y2 =[X**2 for X in x]
plt.plot(x, y, marker ="*", ms =15)
plt.plot(x, y2, marker ="o",mec = 'r')
plt.title("Functions of X")
plt.xlabel("x =1-9")
plt.ylabel("function of x(f(x^2),f(x+3))")
plt.show()
```   
![png](/img/posts/cuteplots/lineplot.png)
    


### Line plot using cutecharts 


```python
#markers
x = range(10)
y = [X+3 for X in x]
y2 =[X**2 for X in x]

df2=pd.DataFrame({
    'x':x,
    'y':y,
    'z':y2})
chart = ctc.Line('Functions of X', width='500px', height='400px')
chart.set_options(
    labels=list(df2['x']), 
    x_label='x =1-9',
    y_label='function of x(f(x^2),f(x+3))'
    )
chart.add_series('f(x+3)', list(df2['y'])) 

chart.add_series('f(x^2)', list(df2['z']))

chart.render()
```
<iframe src ="/htmlembed/lineplot.html" width ="100%">
</iframe>

## Pie charts 

### Pie charts using matplotlib


```python
contribution = [10, 9, 3, 35, 26, 10, 7]
name  = ['Mary', 'Jone', 'Anne', 'Mark', 'Roy', 'Eric', 'Ink']
df=pd.DataFrame({'x':name,
                 'y':contribution})
plt.pie(contribution, explode=None, labels=name)
``` 
![png](/img/posts/cuteplots/piechart.png)
    


### Pie charts using cutecharts


```python


chart = ctc.Pie('% contribution by Students', width='1280px', height='720px')
chart.set_options(
    labels=list(df['x']),
    inner_radius=0
    )
chart.add_series(list(df['y'])) 
chart.render()
```
<iframe src ="/htmlembed/piechart.html" width ="100%">
</iframe>
