### **Practice 1**


##### for practice 1 we perform a test of large numbers for N randomly distributed numbers 
with mean = 0 and stdev = 1. they are counted between 1 and -1

```R

N <-1000
Counter <-0

for(i in rnorm(N, mean = 0, sd = 1 ))
{
  if(i >=-1 && i <=1){
    Counter<- Counter+1
  }
}
result <-Counter/N

print (result)

mean <- result*N


```
N is the size of the sample defined by choosing the number 1000 with the counter started at 0, 
the cycle i is defined in rnorm indicating the amount of random numbers we want in N.


### **Observaciones**
