
### **Visualización de datos para Regresión logística**

```R
dataset <- read.csv('Social_Network_Ads.csv')
dataset <- dataset[, 3:5]
```
comenzamos cargando nuestro archivo indicando en el directorio que vamos a trabajar 

```R
library(caTools)
set.seed(123)
split <- sample.split(dataset$Purchased, SplitRatio = 0.75)
training_set <- subset(dataset, split == TRUE)
test_set <- subset(dataset, split == FALSE)

```
indicamos que vamos a trabajar con una semilla 123 utilizando la librería caTtools, igualmente se le 
indica un split de 75% y que los sets a utilizar serán Training set y test set.	

```R
raining_set[, 1:2] <- scale(training_set[, 1:2])
test_set[, 1:2] <- scale(test_set[, 1:2])

```
Generamos una variable para los datasets y con scale ajustamos la información en ambos datasets.

```R
classifier = glm(formula = Purchased ~ .,
                 family = binomial,
                 data = training_set)

```
se crea una variable para el clasificador utilizando la fórmula dándole el valor a la columna de purchased

```R
prob_pred = predict(classifier, type = 'response', newdata = test_set[-3])
prob_pred
y_pred = ifelse(prob_pred > 0.5, 1, 0)
y_pred

```
ahora generamos la variable que va a guardar la diferencia entre los datasets que creamos 

```R
cm = table(test_set[, 3], y_pred)
cm

```
creamos la matriz de confunsion

```R
ggplot(training_set, aes(x=EstimatedSalary, y=Purchased)) + geom_point() + 
  stat_smooth(method="glm", method.args=list(family="binomial"), se=FALSE)

ggplot(training_set, aes(x=Age, y=Purchased)) + geom_point() + 
  stat_smooth(method="glm", method.args=list(family="binomial"), se=FALSE)

```
ahora generamos la variable que va a guardar la diferencia entre los datasets que creamos 

```R
ggplot(test_set, aes(x=EstimatedSalary, y=Purchased)) + geom_point() + 
  stat_smooth(method="glm", method.args=list(family="binomial"), se=FALSE)

ggplot(test_set, aes(x=Age, y=Purchased)) + geom_point() + 
  stat_smooth(method="glm", method.args=list(family="binomial"), se=FALSE)


```
procedemos a cargar la librería ggplot y a comenzar a asignar los campos para el plotter de cada 
uno de los dos plots buscados, uno usando x=EstimatedSalary, y=Purchased y otro con x=Age, y=Purchased


```R
library(ElemStatLearn)
set = training_set
X1 = seq(min(set[, 1]) - 1, max(set[, 1]) + 1, by = 0.01)
X2 = seq(min(set[, 2]) - 1, max(set[, 2]) + 1, by = 0.01)
grid_set = expand.grid(X1, X2)
colnames(grid_set) = c('Age', 'EstimatedSalary')
prob_set = predict(classifier, type = 'response', newdata = grid_set)
y_grid = ifelse(prob_set > 0.5, 1, 0)
plot(set[, -3],
     main = 'Logistic Regression (Training set)',
     xlab = 'Age', ylab = 'Estimated Salary',
     xlim = range(X1), ylim = range(X2))
contour(X1, X2, matrix(as.numeric(y_grid), length(X1), length(X2)), add = TRUE)
points(grid_set, pch = '.', col = ifelse(y_grid == 1, 'springgreen3', 'tomato'))
points(set, pch = 21, bg = ifelse(set[, 3] == 1, 'green4', 'red3'))

```

```R
set = test_set
X1 = seq(min(set[, 1]) - 1, max(set[, 1]) + 1, by = 0.01)
X2 = seq(min(set[, 2]) - 1, max(set[, 2]) + 1, by = 0.01)
grid_set = expand.grid(X1, X2)
colnames(grid_set) = c('Age', 'EstimatedSalary')
prob_set = predict(classifier, type = 'response', newdata = grid_set)
y_grid = ifelse(prob_set > 0.5, 1, 0)
plot(set[, -3],
     main = 'Logistic Regression (Test set)',
     xlab = 'Age', ylab = 'Estimated Salary',
     xlim = range(X1), ylim = range(X2))
contour(X1, X2, matrix(as.numeric(y_grid), length(X1), length(X2)), add = TRUE)
points(grid_set, pch = '.', col = ifelse(y_grid == 1, 'springgreen3', 'tomato'))
points(set, pch = 21, bg = ifelse(set[, 3] == 1, 'green4', 'red3'))
```

y por último cargamos library(ElemStatLearn) para generar el modelo, asignando en cada uno de lo casos 
cual dataset va a utilizar, mínimos y máximos, los datos del plot como nombre, color, encabezados, etc

