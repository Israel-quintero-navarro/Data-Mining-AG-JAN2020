### **Evaluaton Practice 4**


##### mplement the K-Means grouping model with the Iris.csv dataset found at https://github.com/jcromerohdz/iris using the kmeans () method in R. 
Once the grouping model is obtained do the corresponding data visualization analysis.

```R
getwd()

```
first, we make sure we are in the correct directory

```R
dataset = read.csv(choose.files())
dataset = dataset[1:4]

```
We proceed to load the csv with which we are going to work, in this case it would be iris.csv and we create a dataset from vectors 1 to 4 
since column 5 presents information in an illegal format.

```R
set.seed(6)
wcss = vector()

```
A randomity seed is created and the WCSS method is performed, an algorithm that adds the distances between each point to the centroid of 
the cluster called the elbow method or the elbow method.

```R
 for (i in 1:10) wcss[i] = sum(kmeans(dataset, i)$withinss)

```
with a for in which each cluster from 1 to 10 will perform a sum of kmeans in the data and filter them by inertia.

```R
plot(1:10,
     wcss,
     type = 'b',
     main = paste('The Elbow Method'),
     xlab = 'Number of clusters',
     ylab = 'WCSS')
 
```    
We proceed to create the necessary plot to represent. with the data matrix, labels and types of figures.     

<p align="center">
  <img width="681" height="463" src="https://i.imgur.com/UxhsNIP.png">
  
</p>


```R

 set.seed(29)
kmeans = kmeans(x = dataset, centers = 3)
y_kmeans = kmeans$cluster

```

another random seed is generated. With the kmeans function and indicating the dataset and the numbers of 
centroids deduced by the graph, a filter is made.

```R
library(cluster)
 clusplot(dataset,
          y_kmeans,
          lines = 0,
          shade = TRUE,
          color = TRUE,
          labels = 2,
          plotchar = FALSE,
          span = TRUE,
          main = paste('Clasification of iris'),
          xlab = 'features',
          ylab = 'Clusters')

```
we start the cluster library and graph with a two-dimensional density model entering the parameters
and necessary settings.

<p align="center">
  <img width="652" height="436" src="https://i.imgur.com/dly54KC.png">
  
</p>


### **Observaciones**

We can see that it can be implemented depending on the library in different ways, the visualization 
of data depending on the quantity, each one can carry a different role and a faster representation 
as long as the data is grouped correctly.
