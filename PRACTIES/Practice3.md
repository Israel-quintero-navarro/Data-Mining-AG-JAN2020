# Se proporcionan los siguientes datos

_revenue = c(14574.49, 7606.46, 8611.41, 9175.41, 8058.65, 8105.44, 11496.28, 9766.09, 10305.32, 14379.96, 10713.97, 15433.50)
expenses = c(12051.82, 5695.07, 12319.20, 12089.72, 8658.57, 840.20, 3285.73, 5821.12, 6976.93, 16618.61, 10054.37, 3803.96)_

## se solicita calcular los siguientes puntos:


* Ganancia mensual.
* Ganancia después de impuestos por mes (impuesto del 30%).
* Margen de ganancia mensual.
* Meses buenos.
* Meses malos.
* El mejor mes.
* El peor mes.



Ganancia mensual.

_La ganancia es calculada mediante la resta de los revenues menos los expenses_

![img](https://i.imgur.com/38UesON.png)

Ganancia después de impuestos por mes (impuesto del 30%).
Para calcular la ganancia después de obtener los impuestos primero se calcula el impuesto total y posteriormente la ganancia.

![img](https://i.imgur.com/euJoVT9.png)

Margen de ganancia mensual.
El margen de ganancias redondeando ( ganancias entre rentas) por 100

![img](https://i.imgur.com/RBxUAQq.png)

Media después de los impuestos.
se calcula la media ya con la ganancias después de los impuestos para futuro uso
 
![img](https://i.imgur.com/7oHtUJ3.png)

Meses buenos.
los meses buenos se despliegan calculando la ganancia después de los impuestos que sea mayor a la media, los meses buenos se despliegan con el texto TRUE

![img](https://i.imgur.com/S3w0rLJ.png)

Meses malos.
los meses buenos se despliegan calculando la ganancia después de los impuestos que sea menor a la media, los meses buenos se despliegan con el texto TRUE

![img](https://i.imgur.com/HqO9wUz.png) 

Ganancia máxima y mínima después del impuesto.
para futuro uso se calcula la ganancia minima y maxima utilizando los respectivos comandos de R ( max, min) junto con la ganancia ya con el impuesto.

![img](https://i.imgur.com/PiQBiY1.png)

El mejor mes.
Para obtener el mejor mes utilizamos la simbología del igual igual == usando las variables de ganancia después de tax y la ganancia máxima después del tax, el mejor mes es desplegado con el texto TRUE

![img](https://i.imgur.com/H1yt5Rf.png)

El peor mes.
Para obtener el peor mes utilizamos la simbología del igual igual == usando las variables de ganancia después de tax y la ganancia mínima después del tax, el peor mes es desplegado con el texto TRUE
 
![img](https://i.imgur.com/425eRlc.png)

Conversión a dolares.
dividiendo los valores antes obtenidos entre 1000 y con 0 decimales se obtiene el  

![img](https://i.imgur.com/vQ62E1G.png)

Matriz.
con el comando Matrix desplegamos todos los resultados en forma de matriz tabular

![img](https://i.imgur.com/RB0lzKV.png)
