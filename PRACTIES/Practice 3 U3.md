### **Simple Linear Regression**



```R
dataset <- read.csv('Salary_Data.csv')
```
comenzamos cargando el cvs con los datos a utilizar, en este caso seria Salary_Data.csv


```R
library(caTools)
set.seed(123)
split <- sample.split(dataset$Salary, SplitRatio = 2/3)
training_set <- subset(dataset, split == TRUE)
test_set <- subset(dataset, split == FALSE)

```
indicamos que vamos a trabajar con una semilla 123 utilizando la librería caTtools, 
igualmente se le indica un split de 75% y que los sets a utilizar serán Training set y test set.	


```R
regressor = lm(formula = Salary ~ YearsExperience,
               data = dataset)
summary(regressor)

```
se crea la variable regressor y se le indica que se le cargaran los datos del dataset solo tomando en cuenta el salario y los años  de experiencia en la regresión


```R
y_pred = predict(regressor, newdata = test_set)

```
se carga la variable de preddicion y_pred buscando obtener los nuevos datos ya predichos.

```R
library(ggplot2)
ggplot() +
  geom_point(aes(x=training_set$YearsExperience, y=training_set$Salary),
             color = 'red') +
  geom_line(aes(x = training_set$YearsExperience, y = predict(regressor, newdata = training_set)),
            color = 'blue') +
  ggtitle('Salary vs Experience (Training Set)') +
  xlab('Years of experience') +
  ylab('Salary')

```
utilizando ggplot con la respectiva configuracion y con los datos de entrenamiento de 
salario contra experiencia obtenemos lo siguiente 

<p align="center">
  <img width="484" height="358" src="https://i.imgur.com/xy8Z4H1.png">
  
</p>


```R
ggplot() +
  geom_point(aes(x=test_set$YearsExperience, y=test_set$Salary),
             color = 'red') +
  geom_line(aes(x = training_set$YearsExperience, y = predict(regressor, newdata = training_set)),
            color = 'blue') +
  ggtitle('Salary vs Experience (Test Set)') +
  xlab('Years of experience') +
  ylab('Salary')


```
volvemos a cargar lo mismo pero esta ves solo utilizamos un tercio de los datos de prueba

<p align="center">
  <img width="630" height="463" src="https://i.imgur.com/Lj1iELI.png">
  
</p>
