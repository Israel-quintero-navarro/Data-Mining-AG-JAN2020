### **Evaluatori Practice 3**


##### Implement the Naive Bayes classification model with the Social_Network Ads.csv data set and using the e1071 library 
with the naiveBayes () function. Once the classifier is obtained, do the corresponding data visualization analysis.

```R
getwd()
[1] "C:/Users/Spiral/Documents/Data Mining/Unit 3/Evaluacion"

dataset = read.csv('Social_Network_Ads.csv')
dataset = dataset[3:5]

dataset$Purchased = factor(dataset$Purchased, levels = c(0, 1))

```


first before starting with the manipulation of the data we have to load these, using the function we go to the corresponding 
directory and proceed to load the cvs in the new variable called dataset, we indicate that we will only use columns 3 to 5 
and the purchase values ​​that are 1 or 0 since these will help us to indicate if it is true or false.

```R
library(caTools)
set.seed(123)
split = sample.split(dataset$Purchased, SplitRatio = 0.75)
training_set = subset(dataset, split == TRUE)
test_set = subset(dataset, split == FALSE)

training_set[-3] = scale(training_set[-3])
test set[-3] = scale(test_set[-3])

```

We load the caTool library and indicate the seed, creating a split in the dataset, assigning training set with true values 
and test set with false values. We indicate that it will be 75% of the data where you would create the split.

using scale we make the content of the matrix center the values ​​so that they can be manipulated and scaled.

```R
library(e1071)
classifier = naiveBayes(formula = Purchased ~ .,
                        data = training_set,
                        type = 'C-classification',
                        kernel = 'linear')

y_pred = predict(classifier, newdata = test_set[-3])
y_pred
  [1] 0 0 0 0 0 0 0 1 0 0 1 0 0 0 0 0 0 0 0 0 1 0 0 0 0 1 0 0 0 1 0 0 0 0
 [35] 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 1 1 0 1 0 0 1 1 0 1 1 1 0 1 1
 [69] 1 1 1 0 1 1 1 0 1 0 0 1 0 1 0 1 0 1 1 0 0 1 1 0 1 0 1 1 1 1 0 1
Levels: 0 1

cm = table(test set[, 3], y_pred)
cm
   y_pred
     0  1
  0 57  7
  1  7 29

```

Once this is done, we will now use the e1071 library to implement the statistical learning methods using the naive bayes method. 
We indicate that the data will be the training set. the type will be c-classification and the linear kernel. We create the prediction axes 
where the purchases made will be inserted and cm where the confusion matrix will be indicated with the real data and the predictions 
containing the results of the predictions.


```R
 library(ElemStatLearn)
 set = training_set
 X1 = seq(min(set[, 1]) - 1, max(set[, 1]) + 1, by = 0.01)
 X2 = seq(min(set[, 2]) - 1, max(set[, 2]) + 1, by = 0.01)
 grid_set = expand.grid(X1, X2)
 colnames(grid_set) = c('Age', 'EstimatedSalary')
 y_grid = predict(classifier, newdata = grid_set)
 plot(set[, -3],
      main = 'Naive Bayes (Training set)',
      xlab = 'Age', ylab = 'Estimated Salary',
      xlim = range(X1), ylim = range(X2))
contour(X1, X2, matrix(as.numeric(y_grid), length(X1), length(X2)), add = TRUE)
points(grid_set, pch = '.', col = ifelse(y_grid == 1, 'springgreen3', 'tomato'))
points(set, pch = 21, bg = ifelse(set[, 3] == 1, 'green4', 'red3'))


```

```R

 library(ElemStatLearn)
 set = test_set
 X1 = seq(min(set[, 1]) - 1, max(set[, 1]) + 1, by = 0.01)
 X2 = seq(min(set[, 2]) - 1, max(set[, 2]) + 1, by = 0.01)
 grid_set = expand.grid(X1, X2)
 colnames(grid_set) = c('Age', 'EstimatedSalary')
 y_grid = predict(classifier, newdata = grid_set)
 plot(set[, -3], main = 'Naive Bayes (Test set)',
      xlab = 'Age', ylab = 'Estimated Salary',
      xlim = range(X1), ylim = range(X2))
 contour(X1, X2, matrix(as.numeric(y_grid), length(X1), length(X2)), add = TRUE)
 points(grid_set, pch = '.', col = ifelse(y_grid == 1, 'springgreen3', 'tomato'))
 points(set, pch = 21, bg = ifelse(set[, 3] == 1, 'green4', 'red3'))
 
```
using ElemStatLearn in order to visualize the data in the grouping made by the naive bayes model, the set to be used in each specific case is assigned. 
indicates the minimum and maximum for our groups. the plot type and plot specifications. We indicate the name, axes name, contour, and colors. 
since it will be a parabolic plot with the colors and the contour indicates where the division will take place.

<p align="center">
  <img width="544" height="781" src="https://i.imgur.com/F4Jab5o.png">
  
</p>


### **Observaciones**

podemos ver con los plots obtenidos que aproximadamente un 80% de los datos fueron insertados correctamente mientras que los demás indicados por los 
puntos rojos y verdes que están dentro de su color o grupo incorrecto.
