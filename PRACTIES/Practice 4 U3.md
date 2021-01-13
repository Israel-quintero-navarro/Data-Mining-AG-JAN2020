### **Multiple Linear Regression**

```R
dataset <- read.csv('50_Startups.csv')
```
comenzamos cargando el csv con los datos a utilizar, en este caso seria 50_Startups.csv

```R
dataset$State = factor(dataset$State,
                       levels = c('New York', 'California', 'Florida'),
                       labels = c(1,2,3))
dataset
```
se hace la transformación de los datos ( string to numeric ) y desplegamos el dataset

```R
library(caTools)
set.seed(123)
split <- sample.split(dataset$Profit, SplitRatio = 0.8)
training_set <- subset(dataset, split == TRUE)
test_set <- subset(dataset, split == FALSE)
```
indicamos que vamos a trabajar con una semilla 123 utilizando la librería caTtools, igualmente 
se le indica un split de 75% y que los sets a utilizar serán Training set y test set.	

```Rregressor = lm(formula = Profit ~ .,
               data = training_set )

summary(regressor)
```
se usa el método de regresión linear múltiple y se le indica que se le cargaran los datos 
y se realizara un summary

```Ry_pred = predict(regressor, newdata = test_set)
y_pred
```
cargamos la prediccion de la prueba	

```R
regressor = lm(formula = Profit ~ R.D.Spend + Administration + Marketing.Spend + State,
               data = dataset )
summary(regressor)

regressor = lm(formula = Profit ~ R.D.Spend + Administration + Marketing.Spend,
               data = dataset )
summary(regressor)
```
se realiza el metodo de regresion linear multiple con el modelo de eliminacion, 
mostrando primero todas las columnas del dataset pero solo tomando en cuenta las originales 
y el segundo con state imprimiendo el summary 

```R
regressor = lm(formula = Profit ~ R.D.Spend + Marketing.Spend,
               data = dataset )
summary(regressor)

regressor = lm(formula = Profit ~ R.D.Spend + Marketing.Spend,
               data = dataset )
summary(regressor
```

al ser eliminadas ciertas columnas para la regresión se imprime el summary de las eliminaciones.

```R
y_pred = predict(regressor, newdata = test_set)
y_pred
```
realizamos la predicción final para cada set

<p align="center">
  <img width="567" height="76" src="https://i.imgur.com/DfaE4G8.png">
  
</p>

y obtenemos el siguiente ploteo

<p align="center">
  <img width="615" height="429" src="https://i.imgur.com/NvJx0bJ.png">
  
</p>

