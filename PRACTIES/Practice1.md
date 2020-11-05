#Práctica 1

_Pruebe la ley de los números grandes para N números aleatorios normalmente distribuidos con media = 0, stdev = 1:
Cree un script R que cuente cuántos de estos números se encuentran entre -1 y 1 y lo dividirá por la cantidad total de N
Usted sabe que E (X) = 68.2% Verifique que Media (Xn) -> E (X) mientras vuelve a ejecutar su script mientras aumenta N
Insinuación:_

>1.	Se inicia el tamaño de la muestra

N=1:100

>2.	posteriormente el contador

C=1 

>3.	se trabaja con un ciclo for (i en rnorm (tamaño)) para generar los numero aleatorios

for(i in norm(N))

{

>4.	se agrega un if para verificar si el contador va a aumentar si es menor que 1 y mayo que -1

if(i<1&i>-1) 

>5.	si es asi el contador aumenta

c=c+1

>6.	se devuelve el resultando y se plotea con la linea plot(result)

results = c/N
result

![result](https://i.imgur.com/G8rax8u.png)

plot(result)

![plot](https://i.imgur.com/ZRYLmBU.png)
