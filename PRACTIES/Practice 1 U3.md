Analiza la siguiente función de “backwardElimination”

```R
backwardElimination <- function(x, sl) {
```
Se nombra la función y se le agregan sus parámetros correspondientes

```R
numVars = length(x)
```
La variable numVars es agregada y se especifica el valor de la longitud con x

```R
for (i in c(1:numVars)){
```
en un ciclo for se indica que por cada valor en el vector se realizara lo siguente

```R
regressor = lm(formula = Profit ~ ., data = x)
```
con la variable regressor que contendra los valores del modelo de regresion lineal se contendra toda la columna de profit en x

```R
maxVar = max(coef(summary(regressor))[c(2:numVars), "Pr(>|t|)"])
```
en un if se indica que si el valor maximo es mayor sl se buscara un vector que tenga el mismo valor que maxVar y la guarde en j


```R
if (maxVar > sl){
      j = which(coef(summary(regressor))[c(2:numVars), "Pr(>|t|)"] == maxVar)
```
Se elimina el vector j de el dataset


```R
x = x[, -j]
    }
```
restamos la unidad de longitud de el dataset numVars del for y regresamos la sumatoria de los valores en regressor para seguir con el ciclo.

```R
    numVars = numVars - 1
  }
  return(summary(regressor))
}
```
