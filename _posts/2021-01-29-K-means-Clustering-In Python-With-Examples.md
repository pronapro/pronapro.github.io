---
layout: post
title:  "
K-means Clustering In Python With Examples
"
date:   2021-01-29 16:01:15 +0300
categories: jekyll update
---


## Image 
# Introduction
In this blog, we shall be looking at how to solve such problems that require clustering/grouping. We shall use K-means clustering using the sklearn library. Other  common clustering algorithms we won’t be looking at in this blog  are hierarchical clustering, density-based clustering and  model-based clustering. Grouping things is important in everyday life. We naturally group things that are kind related. In fact, even in society, we tend to have classes. Grouping data is easy when we have little data where information doesn’t require much calculations to identify similarities, when we have massive amounts of data computers tend to perform better than humans in a short period of time.

Clustering is applied to unsupervised machine learning problems because it does not require a target during training inorder to identify the output.its is applied on problems like image segmentation, image compression, topic based document classification, customer segmentation etc.

# K-Means Algorithm
K-means algorithm is an unsupervised learning. It is an iterative algorithm that partitions n datasets into k groups where k must be less than n. K-means is a distance-based algorithm. Each point belongs to one group.Member of a cluster/group have similarities in their features.

The number of clusters K has to be known for us to group our data points into clusters. K-mean is the simplest and commonly used clustering algorithm.

## How It Works
1. Identify the number of groups k needed
2. Randomly select k points from the data and make them the initial centroids
3. Assign input data to k that is the nearest centroid (using Euclidean distance or Manhattan distance)
4. Calculate and Update the centroid with  the mean of all members of a cluster.
5. Iterate steps 3 and 4 until the cluster centroids are unchangeable.
# Implementation
Import libraries

Pandas, sklearn, matplotlib, NumPy are the libraries we are going to use.  These libraries are not built-in libraries so you have to install them on your local machine.

```python 
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```
## Load Data
Data

For this example we are going to use African economic data to do the clustering. This has two features: government expenditure and unemployment percentages that are easy to visualize in 2D space. We shall add internet usage to the data in the second example to show how one can visualize data that is more than two dimensions. Our data is already clean so we shall not bother with the steps with a few intended outliers.

We use pandas to load the data set.

```python 
#read data
df = pd.read_csv('economic-data-africa.csv', sep=';', encoding='ISO-8859-1')
# peek of data
df.head()
```

## Image 

## Define K Value Using The Elbow Method
K value is the number of clusters/classes/groups we want to divide our data into. Before we use the k -means algorithm we have to know it. K value can be obtained intuitively from having domain knowledge or experience working with such datasets. Let us assume we don’t know how many classes we need. We use the elbow method to help identify which k value is optimal.

For our example, we shall take the number of k from 1to 10. Elbow method calculates the sum of squared distance between each element and the centroid of each cluster. kmeans.fit_predict method returns an array containing cluster labels of each data point. kmeans inertia_ attribute is the Sum of squared distances of samples

```python 
#sum of squared distance
ssd = []
for i in range(1, 10):
    kmeans = KMeans(n_clusters = i, init = 'k-means++', random_state = 5)
    kmeans.fit(X)
    ssd.append(kmeans.inertia_)
plt.plot(range(1, 10), ssd)
plt.grid()
plt.title('The Elbow Method', fontsize =20)
plt.xlabel('Number of clusters', fontsize =20)
plt.ylabel('SSD',fontsize =20)
plt.savefig("elbow.png")
plt.show()
```
# image 

Elbow point is a point when the graph starts moving almost parallel to the x axis. It’s the optimal number of k.sometimes it’s hard to get the number when the curve is smooth and no bent points.

From the elbow method, we see that four is the base number of classes to use. This makes sense because we have countries with low unemployment, countries with high unemployment and average unemployment the same as with government expenditure.

We assume the classes are:

Lower government expenditure and a lower unemployment rate
Lower government expenditure and a higher unemployment rate
Higher government expenditure and a higher unemployment rate
Higher government expenditure and a lower unemployment rate
Let us go ahead and implement the clusters. We shall visualize the clusters to see how they are distributed.

```python 
kmeans= KMeans(n_clusters = 3, init = 'k-means++', random_state = 2)
label = kmeans.fit_predict(X) 
centroids = kmeans.cluster_centers_
u_labels = np.unique(label)
color_s =["gray","pink","navy","maroon"] 
for i in u_labels:
    plt.scatter(X[label == i , 0] , X[label == i , 1] ,s=100, label = "cluster "+str(i), color =color_s[i])

plt.scatter(centroids[:,0] , centroids[:,1] , s = 300, color = 'orange')
plt.title('Clusters of countries')
plt.xlabel('Government expenditure')
plt.xlabel('Unemployment')
plt.legend()
plt.savefig("outcluster.png")
plt.show()
``` 
## Image 
We see that we have one value that is an outlier and creating its own class. This is because k means is a distance based algorithm.this point is too powerful it gets its own class.this is a challenge if we are modeling data because you might work hard on this and it doesn’t work again. A simple example that isn’t related to data we are using is incase you run an online business and you are trying to model services based on clients, one person that shopped once because they had a party might cause data to skew yet they won’t buy that again.

Kmeans is sensitive to outliers. outliers increase the mean of the data. The outlier creates its own cluster. Here we have one but with many outliers, it might be worse. It’s important to remove outliers from data before using the k-means algorithm.

Let us explore what happens when we remove the outlier and perform kmeans clustering on the data. after removing outliers we perform the elbow method to get the optimal number of clusters k.

```python 
X = df[["GovExpenditurePerc", "UnemploymentPerc"]]
#remove outlier
X = X.loc[X['GovExpenditurePerc'] < 80]
#elbow method
ssd = []
for i in range(1, 10):
    kmeans = KMeans(n_clusters = i, init = 'k-means++', random_state = 5)
    kmeans.fit(X)
    ssd.append(kmeans.inertia_)
plt.plot(range(1, 10), ssd)
#plt.grid()
plt.title('The Elbow Method', fontsize =20)
plt.xlabel('Number of clusters', fontsize =20)
plt.ylabel('SSD',fontsize =10)
plt.savefig("elbow.png")
plt.show()
```
## Image 

```python 
kmeans= KMeans(n_clusters = 4, init = 'k-means++', random_state = 2)
label = kmeans.fit_predict(X) 
centroids = kmeans.cluster_centers_
u_labels = np.unique(label)
color_s =["gray","pink","navy","maroon"] 
for i in u_labels:
    plt.scatter(X[label == i , 0] , X[label == i , 1] ,s=100, label = "cluster "+str(i), color =color_s[i])

plt.scatter(centroids[:,0] , centroids[:,1] , s = 300, color = 'orange')
plt.title('Clusters of countries')
plt.xlabel('Government expenditure')
plt.xlabel('Unemployment')
plt.legend()
plt.savefig("noOutliercluster.png")
plt.show()
``` 

## Image 

With removed outliers, we see that the optimal number of k is 4 and all clusters have elements within them. This shows us the importance of removing outliers or knowing how to deal with it. One rich customer or one-time customer might make you create a category which is not always there due to reasons like they were throwing a party etc.

It’s time to get a sense of what the clusters look like

## Image 
## Image 

# Working With More  Dimensions
We follow the same steps and methods when implementing k-means on data in higher dimensions. The only challenge we face when working with data in high dimension is visualizing it. In this step we are going to look at how to deal with such using some visualization and PCA which is a dimension reduction algorithm.

Let us look at our data.

## Image 

We have already identified the value of k so we won’t do that step again. feel free to do it. I am skipping it because I don’t want to write almost the same code multiple times.

Below is information about each cluster in table format.

## Image 

## Visualization
One way to do this is using a pairplot from seaborn. This helps see the contribution of each variable.
## Image 
Another way is to use a parallel coordinates graph from pandas.
## Image 

## Visualization using PCA

PCA works well in combination with k-means if we have data with many features. This lowers dimensions of data to a few that are needed. In our case, we need data to be in two dimensions. let’s go ahead and implement it. We have to import PCA in order to use it.
```python 
from sklearn.decomposition import PCA
from sklearn.cluster import KMeans
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
#initializing PCA
m_df =pd.read_csv("kmeansdata.csv")
pca = PCA(2)
#Transform the data
df = pca.fit_transform(m_df)

kmeans = KMeans(n_clusters= 4)

#predict the labels.
label = kmeans.fit_predict(df)
# plotting
#Getting the Centroids
centroids = kmeans.cluster_centers_
u_labels = np.unique(label)
color_s =["gray","pink","navy","maroon"] 
#plotting the results:
 
for i in u_labels:
    plt.scatter(df[label == i , 0] , df[label == i , 1] ,s=100, label = "cluster "+str(i), color =color_s[i])
plt.scatter(centroids[:,0] , centroids[:,1] , s = 300, color = 'orange')
plt.legend()
plt.savefig("multi_pca.png")
plt.show()
``` 

## Evaluation
It is hard to evaluate the performance of the K -means algorithm since we don’t have ground truth data. The correctness of the model depends on the use case and user.

## Conclusion
In this blog, we learnt how to implement k means clustering and how to visualize our clusters. We used PCA to do dimension reduction in order to visualize data in higher dimensions. I hope you have enjoyed it and as usual, I encourage you to use the skills you have learnt and apply them to other datasets. See you in the next blog.
