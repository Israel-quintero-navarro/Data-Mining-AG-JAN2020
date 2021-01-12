### **The directors of the movie review website are very happy with my previous installment and now have a new requirement.**

##### The previous consultant had created a chart for them which is illustrated in the image below.

<p align="center">
  <img width="460" height="300" src="https://i.imgur.com/plzb8AU.png">
  
</p>

However, the R code used to create the graph has been lost and cannot be recovered.

My task is to create the code that will recreate the same table making it look as close to the original as possible.

I will be provided with a new dataset which I can find at this link:

https://github.com/jcromerohdz/DataMining/blob/master/Datasets/Project-Data.csv 

Before starting to worl the data in the graph it is necessary to load the file, to optimize this first with the setwd 
function i indicate which one is the directory that will be used to work and confirm it with getwd.

```R
setwd("C:/Users/Xante/Desktop/DataMining/Unit 2/Exam")
getwd()

```
Ya una vez seleccionado el directorio y confirmado, le indicamos con Read.csv que nos lea el csv que fue proporcionado llamado **Project-Data.csv**

```R
Data <- read.csv("Project-Data.csv")
```

For reasons of later use in the software and to avoid it throwing us an error, we also indicate that we load the library for ggplot2 plotting.

```R
library(ggplot2)
```
We start by building the data in a data frame since the csv that was provided contains information in a structure and with symbols in the part of the columns 
that could cause conflicts when using them in R

```R
colnames(Data) <- c("Day_of_Week", "Director", "Genre", "Movie_Title", "Release_Date",
                                         "Studio", "Adjusted_Gross", "Budget",
                                         "Gross","IMDb_Rating","MovieLens_Rating",
                                         "Overseas_M", "Overseas", "Profit_M","Profit","Runtime",
                                         "US","Gross_US")                                         "US","Gross_US")


```


In the request we are told that it is necessary to reach 6 Flim Studios and 5 Genres, observing the csv it can be observed that it contains more data than 
required for the plot, in order to reduce these and reach a point where our new plot be similar, we create a filter for the studies and another for the genres, 
starting with gender in alphabetical order with the operator or we group all the genres into one.

```R
Dataframe <- Data[Data$Genre == "action" | Data$Genre == "adventure" | Data$Genre == "animation"
                 | Data$Genre == "comedy" | Data$Genre == "drama",]

```

We proceed to do the same with the studies but now we give it another name so as not to generate a conflict since we are going to tell it to also take the first data frame.

```R
Dataframe2 <- Dataframe[Dataframe$Studio == "Buena Vista Studios" | Dataframe$Studio == "Fox" 
   | Dataframe$Studio =="Paramount Pictures" | Dataframe$Studio == "Sony"
   | Dataframe$Studio =="Universal" | Dataframe$Studio =="WB",]

```
Once the information is structured, we proceed to generate the plot, for this we give it a structure using the ggplot options. 
telling it to use dataframe2. with aes we fix the aestethic of the plot.

Using the function and ggplot geom_jitter we add a jitter diagram for the representation and a boxplot to group it in boxes graphically, we indicate the parameters indicated 
for each option such as color, size, dispersion. source. etc. obtaining the result shown here.

```R
p <- ggplot(Dataframe2, aes(x=Genre, y=Gross_US, 
                             color=Studio, size=Budget))
 
p + geom_jitter() + geom_boxplot(size=0.2, color = "Black", alpha=0.4) +
     labs(title = "Domestic Gross % by Genre", x = "Genre", y = "Gross % US") + scale_size(name="Budget $M") +
     theme(axis.title.x = element_text(color = "BlueViolet", size = 15),
           axis.title.y = element_text(color = "BlueViolet", size = 15),
           plot.title = element_text(hjust = 0.5, size =19),
           text = element_text(family = "Comic Sans MS"))

```

<p align="center">
  <img width="960" height="509" src="https://i.imgur.com/aXC6rJp.png">
  
</p>

