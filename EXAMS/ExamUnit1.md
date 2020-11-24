# Instrucciones

_El Banco Mundial quedó muy impresionado con su entrega en la asignación anterior y
tienen un nuevo proyecto para usted._

_Debe generar un diagrama de dispersión (scatter-plot) que muestre las estadísticas
de esperanza de vida ( Life expectancy - eje y) y tasa de fertilidad (Fertility Rate -eje
x) por país (Country)._	

_El diagrama de dispersión también debe clasificarse por países Regiones (Country
Regions)._

_Se le han proporcionado datos durante 2 años: 1960 y 2013 y se le exige que
produzca una visualización para cada uno de estos años._

_Algunos datos se han proporcionado en un archivo csv, algunos en vectores R. El
El archivo csv contiene datos combinados de ambos años. Toda manipulación de datos
debe realizarse en R (No en Excel) porque este proyecto puede ser auditado en una
etapa posterior._

_También se le ha pedido que proporcione información sobre cómo se comparan los
dos períodos. (Hint: Básicamente la explicación de sus observaciones)._

## Procedimiento y evidencias

Primero comenzamos cargando la información que se nos proporcionó y que vamos a necesitar para este trabajo, estos dos archivos sería 
el csv “DataFrameEvaluation_Data.csv” y introducimos los datos en el archivo “Test-Vectors.R” que son 3 vectores, estos incluyen 
los códigos del país, la esperanza de vida de 1960 y la esperanza de vida de 2013. utilizando **stats <- read.csv(file.choose())**  buscamos el archivo.

Posteriormente cargamos la librería necesaria para poder hacer el ploteo con el comando **library(ggplot2)**

![img](https://i.imgur.com/zmNBjAK.png)
![img](https://i.imgur.com/gOn7sRc.png)

Antes de crear los plots primero necesitamos manejar los datos que se proporcionaron para así poder obtener un mejor ploteo. para hacer esto utilizamos 
la función merge y así crear los data frames.

Primero creamos un data frame que incluya los códigos de país, la esperanza de vida de y la esperanza de vida al nacer de 1960/2013 respectivamente.
posteriormente procedemos al merge y le damos un nuevo nombre que será el que aparezca en la columna del plot igualmente indicando así que el nombre 
del frame será merged y que los parámetros by.x / by.y son los que tienen parecido dentro del data frame y tiene que combinarlos

**dfmerge <- data.frame(Country= Country_Code, Life_Expectancy_1960= Life_Expectancy_At_Birth_1960,
                     Life_Expectancy_2013= Life_Expectancy_At_Birth_2013)**

**merged <- merge(stats, dfmerge, by.x = "Country.Code", by.y = "Country")**

![img](https://i.imgur.com/Tv4FDdX.png)
![img](https://i.imgur.com/Q9ZqqZA.png)

ya que podemos llegar a tener datos repetidos en los vectores, esto podría afectar en el ploteo y crear un mal flujo de información, 
por lo tanto así un resultado final erróneo.

**stats1960 <-  stats[stats$Year == 1960,]**
**stats2013  <- stats[stats$Year == 2013,]**

![img](https://i.imgur.com/7oTn6mA.png)

ya que se ha manipulado la información nuestro ploteo sería más cercano a lo que se busca y más preciso, con la función plot generamos 
los gráficos que se buscan. indicando cada unos de los parámetros que va a utilizar para las columnas y la simbología que debe utilizar
para indicar el plot en el que seria asi ( x = fertilidad, y= esperanza de vida, color = los datos de cada país,  main= título del gráfico, 
shape = forma del gráfico/plot, alpha = la transparencia de los puntos en el plot y size = el tamaño ).

**qplot(data = merged, y=Life_Expectancy_1960, x=Fertility.Rate, color = Country.Name, 
      size=I(3), shape=I(19), alpha =I(.4),main = "Fertility Rate and Life Expectancy per Country 1960")**

**qplot(data = merged, y=Life_Expectancy_1960, x=Fertility.Rate, color = Country.Name, 
      size=I(3), shape=I(19), alpha =I(.4),main = "Fertility Rate and Life Expectancy per Country 2013")**


se puede observar en el grafico que la informacion esta muy extensa, esto es por que los datos están desplegados por cada país en la leyenda 
y no por los años que es lo que buscamos, igualmente al presionar en ellos no nos da la información de los años, tenemos que arreglar esto 
para poder obtener la información de la forma que se desea.

![img](https://i.imgur.com/L2QIFIz.png)![img](https://i.imgur.com/dKVoFwC.png)
                                       ![img](https://i.imgur.com/eNt4IQS.png)
                                       
para poder generar un plot mejor intentaremos hacerlo por región en lugar de hacerlo por país, para hacer esto le indicamos en “Color” que 
utilice el dato de “Región”, así generando un plot ahora con la información distribuida por región en lugar de país y creando una visualización 
de los datos más condensada. logrando notar ahora si las diferencias entre cada año pero aún nos falta algo importante para poder lograr un 
análisis correcto, esto sería la fertilidad de cada año.                                       

**qplot(data = merged, x = Fertility.Rate, y = Life_Expectancy_1960,
      color = Region, size=I(3), shape=I(19), alpha =I(.4), 
      main = "Fertility Rate vs Life Expectancy 1960")**

**qplot(data = merged, x = Fertility.Rate, y = Life_Expectancy_2013,
      color = Region, size=I(3), shape=I(19), alpha =I(.4), 
      main = "Fertility Rate vs Life Expectancy 2013")**
      
 ![img](https://i.imgur.com/lXZzCkt.png)     
 ![img](https://i.imgur.com/3GfbSlu.png)   

Es preferible indicar un filtro en el data frame y así evitar fallas e información errónea a la hora de plotear. hacemos esto agrupando con 
un filtro a los datos de 1960 y otro con los datos de 2013

con la esperanza de vida, los códigos de pais y la esperanza de vida al nacer creamos un merge por cada año, indicando que es diferente del 
anterior agregandole los dos ultimos digitos del año al final.

**dfmerge1960 <- data.frame(Country= Country_Code, Life_Expectancy_1960= Life_Expectancy_At_Birth_1960)
dfmerge2013 <- data.frame(Country= Country_Code, Life_Expectancy_2013= Life_Expectancy_At_Birth_2013)**

![img](https://i.imgur.com/iMze1a4.png)      

posteriormente haciendo el merge de los data frames con los stats y indicando las variables x, y para el ploteo.

**merged1960 <- merge(stats1960, dfmerge1960, by.x = "Country.Code", by.y = "Country")
merged2013 <- merge(stats2013, dfmerge2013, by.x = "Country.Code", by.y = "Country")**

![img](https://i.imgur.com/CQazFkc.png)     

Ahora deberíamos obtener un plot más específico y correcto, con la información y la precisión que se nos indico en el request. utilizando 
el nuevo data frame procedemos a crear nuevos plots para cada año.

**qplot(data = merged1960, x = Fertility.Rate, y = Life_Expectancy_1960,
      color = Region, size=I(3), shape=I(19), alpha =I(.4), 
      main = "Fertility Rate vs Life Expectancy 1960")**

**qplot(data = merged2013, x = Fertility.Rate, y = Life_Expectancy_2013,
      color = Region, size=I(3), shape=I(19), alpha =I(.4), 
      main = "Fertility Rate vs Life Expectancy 2013")**
      
y listo, nuestro plot se encuentra de una manera correcta y listo para ser presentado      

![img](https://i.imgur.com/tEuOxoK.png)      

![img](https://i.imgur.com/IWQbXNZ.png)     

# Observaciones

ya terminado este proyecto se puede ver en los gráficos obtenidos podemos observar como es que se genero un cambio tanto en la esperanza 
de vida como en la fertilidad con el paso de los años, para ahorrar tiempo abreviamos indice de fertilida como IF y esperanza de vida 
como EV, en africa se puede observar como es que en el año 1960 el IF y la EV eran altos e incluso comparados a lugares como asia donde 
es comun que las personas llegen a edades mayores y sus familias sean numerosas, se puede observar como es que con el paso de los año ambas 
se disminuyeron en cantidades enormes, igualmente en asia donde en años anteriores era comun entre los jovenes buscar tener decendencia 
y seguir con el legado de sus familias se puede obersvar como se ah dado un cambio radical, donde la EV de la gente sigue siendo alta pero 
las IF ah bajado, los jovenes del continente asiatico en estos dias buscarn satisfacer sus placeres de otras maneras y llevar sus vidas a 
su propio ritmo, sin preocuparse por seguir con sus lineajes o hacer crecer sus familias.


actualmente en el año 2020 se ha registrado casi más del 30% de reducción en la tasa de natalidad en varios países del continente asiatico
especialmente en japón, donde los jóvenes están más ocupados buscando como sobrevivir a esta año y a pesar que en años anteriores ya se 
había registrado una baja de la taza, los jóvenes insisten en llevar a cabo su estilo de vida, incluso se pronostica que para los próximos 
años los ancianos en japón sean mayores a los infantes o recién nacidos en el año 2020.


por otra parte tenemos el lado opuesto de la moneda europa y las americas, donde lo que se ah llegado a reducir es minimo e incluso la 
esperanza de vida en europa a aumentado por mucho, se puede ver a simple vista como es que en estos lugares las tradiciones aun siguen en 
pie y las personas buscan tener su propia familia, aunque no tenemos la informacion más actual de los año y en un lapso de más de 7 años
muchas de las personas jovenes estan descartando esta ideologia y adoptando una más nueva, en la que el aborto legal podria llegar a hacer 
cambios grandes en estas estadisticas puesto que muchos de los nacimientos por cuestiones fuera del concentimiento de las personas serian 
detenidos y asi se reducirian algunos de los indices altos de natalidas, especialmente en paises como latino america.


# Liga para video a YT

https://www.youtube.com/watch?v=thpcJrzyHOs&feature=youtu.be

