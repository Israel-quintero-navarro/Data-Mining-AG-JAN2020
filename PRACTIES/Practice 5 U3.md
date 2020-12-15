### **Árbol de deciciones**

```R
library(ElemStatLearn)
set = training_set
X1 = seq(min(set[, 1]) - 1, max(set[, 1]) + 1, by = 0.01)
X2 = seq(min(set[, 2]) - 1, max(set[, 2]) + 1, by = 0.01)
grid_set = expand.grid(X1, X2)
colnames(grid_set) = c('Age', 'EstimatedSalary')
y_grid = predict(classifier, newdata = grid_set, type = 'class')
plot(set[, -3],
     main = 'Decision Tree Classification (Training set)',
     xlab = 'Age', ylab = 'Estimated Salary',
     xlim = range(X1), ylim = range(X2))
contour(X1, X2, matrix(as.numeric(y_grid), length(X1), length(X2)), add = TRUE)
points(grid_set, pch = '.', col = ifelse(y_grid == 1, 'springgreen3', 'tomato'))
points(set, pch = 21, bg = ifelse(set[, 3] == 1, 'green4', 'red3'))
```

cargamos la librería  ElemStatLearn y con los datos de los dataset anteriormente usados 
y creados se llevan a cabo las secuencias, un grid_set en el cual compararemos las secuencias 
y combinaremos el age y el estiamtedsalary en un solo vector.


<p align="center">
  <img width="683" height="381" src="https://i.imgur.com/o10aBoi.png">
  
</p>

```R
library(ElemStatLearn)
set = test_set
X1 = seq(min(set[, 1]) - 1, max(set[, 1]) + 1, by = 0.01)
X2 = seq(min(set[, 2]) - 1, max(set[, 2]) + 1, by = 0.01)
grid_set = expand.grid(X1, X2)
colnames(grid_set) = c('Age', 'EstimatedSalary')
y_grid = predict(classifier, newdata = grid_set, type = 'class')
plot(set[, -3], main = 'Decision Tree Classification (Test set)',
     xlab = 'Age', ylab = 'Estimated Salary',
     xlim = range(X1), ylim = range(X2))
contour(X1, X2, matrix(as.numeric(y_grid), length(X1), length(X2)), add = TRUE)
points(grid_set, pch = '.', col = ifelse(y_grid == 1, 'springgreen3', 'tomato'))
points(set, pch = 21, bg = ifelse(set[, 3] == 1, 'green4', 'red3'))
```
realizaremos lo mismo pero esta vez pera el test_set


<p align="center">
  <img width="652" height="393" src="https://i.imgur.com/Zs9qTZj.png">
  
</p>

```R
plot(classifier)
text(classifier, cex=0.6)

```
con estos resuldatos procederemos a crear el arbol de deciciones con lo siguiente 


<p align="center">
  <img width="678" height="466" src="https://i.imgur.com/sV3pcb3.png">
  
</p>
