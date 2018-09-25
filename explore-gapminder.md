---
title: "Explore gapminder"
author: "sukey"
date: "September 20, 2018"
output:
    html_document:
        keep_md: true
---

## Smell test the data
Explore the gapminder object:

```r
library(gapminder)
library(tidyverse)
library(dplyr)
```

  * #### Is it a data.frame, a matrix, a vector, a list?

```r
inherits(gapminder,"data.frame") 
### or we can also use "str()"
str(gapminder)
```
**<u> Answer: The function returns "True", so it is a data frame </u>. Using str() gives you that information plus extra goodies (such as the levels of your factors and the first few values of each variable)** 

  * #### What is its class?

```r
class(gapminder) 
```
**<u> Answer: The class of gapminder is  "data.frame" </u>. The function class prints the vector names of classes an object inherits from**  

  * #### How many variables/columns?

```r
ncol(gapminder) 
```
**<u> Answer: The number of columns is 6 </u>. Also we can use str() function and then count the number of columns**  

  * #### How many rows/observations?

```r
nrow(gapminder) 
```
**<u> Answer: The number of rows is 1704 </u>.**

  * #### Can you get these facts about “extent” or “size” in more than one way? Can you imagine different    functions being useful in different contexts?

```r
dim(gapminder) # this function can directly return the size
str(gapminder) # str() returns size and other info
nrow(gapminder) # nrow() can combine with ncol() to check the size of data
ncol(gapminder)
```
**<u> Answer:  1704 rows and 6 columns </u>. dim() returns the dimensions of an object. rowNumber = dim(object)[1]; colNumber = dim(object)[2]**  

  * ####  What data type is each variable?

```r
str(gapminder)
```

```
## Classes 'tbl_df', 'tbl' and 'data.frame':	1704 obs. of  6 variables:
##  $ country  : Factor w/ 142 levels "Afghanistan",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ continent: Factor w/ 5 levels "Africa","Americas",..: 3 3 3 3 3 3 3 3 3 3 ...
##  $ year     : int  1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 ...
##  $ lifeExp  : num  28.8 30.3 32 34 36.1 ...
##  $ pop      : int  8425333 9240934 10267083 11537966 13079460 14880372 12881816 13867957 16317921 22227415 ...
##  $ gdpPercap: num  779 821 853 836 740 ...
```
**<u> Answer: The type of each variable is shown as above </u>: ** 

  + Country is factor
  + continent is also factor
  + year is int
  + lifeExp is numberic
  + pop is int


---
## Explore individual variables  

Pick at least one categorical variable and at least one quantitative variable to explore: 

  * #### What are possible values (or range, whichever is appropriate) of each variable?
  

```r
summary(gapminder)
```

```
##         country        continent        year         lifeExp     
##  Afghanistan:  12   Africa  :624   Min.   :1952   Min.   :23.60  
##  Albania    :  12   Americas:300   1st Qu.:1966   1st Qu.:48.20  
##  Algeria    :  12   Asia    :396   Median :1980   Median :60.71  
##  Angola     :  12   Europe  :360   Mean   :1980   Mean   :59.47  
##  Argentina  :  12   Oceania : 24   3rd Qu.:1993   3rd Qu.:70.85  
##  Australia  :  12                  Max.   :2007   Max.   :82.60  
##  (Other)    :1632                                                
##       pop              gdpPercap       
##  Min.   :6.001e+04   Min.   :   241.2  
##  1st Qu.:2.794e+06   1st Qu.:  1202.1  
##  Median :7.024e+06   Median :  3531.8  
##  Mean   :2.960e+07   Mean   :  7215.3  
##  3rd Qu.:1.959e+07   3rd Qu.:  9325.5  
##  Max.   :1.319e+09   Max.   :113523.1  
## 
```
country and continent are categorical variables and year,lifeExp,pop,gdpPercap are quantitative variable; the possible values of each variable are shown as above.  

If we only want check the information of one value at each time, here are some functions we can use: 


```r
attach(gapminder)  # when using attach(), onjects in the database can be accesed by simply giving names. instead of using object$value

###################################  quantitative variable   #########################################
range(year)   # it is shown that the range of "year" is from 1952 to 2007

####  we can also use min() and max() to check the range
min(year)   # 1952
max(year)   # 2007

### what about summary？ 
summary(year)

#################################### categorical variable #########################################
summary(country) # unlike quantitative variable, summary(categorical variable) returns the frequenct of each category

### besides summary(), table() is also a nice try
table(country)
```


  * ####  What values are typical? What’s the spread? What’s the distribution? Etc., tailored to the variable at hand.
  

```r
summary(lifeExp)
table(continent)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##   23.60   48.20   60.71   59.47   70.85   82.60 
## continent
##   Africa Americas     Asia   Europe  Oceania 
##      624      300      396      360       24
```
  
**Answer: the typical values of lifeExp are: mean = 59.47 Median = 60.71; The overall spread of lifeExp is max-min = 1318939990, IQR = 3rd-1st = 16796000; There are 624 information from Africa, 300 from Americas, 396 from Asia, 360 from Europe and 24 from Oceania**

---
## Explore various plot types  


```r
### There is a lot of data, but I only want to foucs on the information from Asia

info_Asia <- gapminder %>% 
  filter(continent == 'Asia')
```

```
## Warning: package 'bindrcpp' was built under R version 3.5.1
```

```r
summary(info_Asia$country)
info_Asia <-rename(info_Asia, cou = country)
ggplot(info_Asia, aes(cou, pop)) +
  geom_boxplot(aes(fill = cou)) +
  ggtitle("Distrubtion of pop in Asia")
```

![](explore-gapminder_files/figure-html/unnamed-chunk-11-1.png)<!-- -->

***There are too many countries in my graph, but I only have intrest in country with huge population***


```r
info_Asia <- gapminder %>% 
  filter(continent == 'Asia' & pop > 1000000000)
summary(info_Asia$country)
info_Asia <-rename(info_Asia, cou = country)
ggplot(info_Asia, aes(cou, pop)) +
  geom_boxplot(aes(fill = cou)) +
  ggtitle("Distrubtion of pop in Asia")
```

![](explore-gapminder_files/figure-html/unnamed-chunk-12-1.png)<!-- -->


**According to the garph above, we can find that China and India are the countries with large population in Asia**


***Now I want to get more information of China and India, and find some differences***


```r
China_India <- gapminder %>% 
  filter(country %in% c("China","India"))
dim(China_India)  ## check the size of China_India
```

```
## [1] 24  6
```

```r
knitr::kable(China_India) ## use table presentation
```



country   continent    year    lifeExp          pop   gdpPercap
--------  ----------  -----  ---------  -----------  ----------
China     Asia         1952   44.00000    556263527    400.4486
China     Asia         1957   50.54896    637408000    575.9870
China     Asia         1962   44.50136    665770000    487.6740
China     Asia         1967   58.38112    754550000    612.7057
China     Asia         1972   63.11888    862030000    676.9001
China     Asia         1977   63.96736    943455000    741.2375
China     Asia         1982   65.52500   1000281000    962.4214
China     Asia         1987   67.27400   1084035000   1378.9040
China     Asia         1992   68.69000   1164970000   1655.7842
China     Asia         1997   70.42600   1230075000   2289.2341
China     Asia         2002   72.02800   1280400000   3119.2809
China     Asia         2007   72.96100   1318683096   4959.1149
India     Asia         1952   37.37300    372000000    546.5657
India     Asia         1957   40.24900    409000000    590.0620
India     Asia         1962   43.60500    454000000    658.3472
India     Asia         1967   47.19300    506000000    700.7706
India     Asia         1972   50.65100    567000000    724.0325
India     Asia         1977   54.20800    634000000    813.3373
India     Asia         1982   56.59600    708000000    855.7235
India     Asia         1987   58.55300    788000000    976.5127
India     Asia         1992   60.22300    872000000   1164.4068
India     Asia         1997   61.76500    959000000   1458.8174
India     Asia         2002   62.87900   1034172547   1746.7695
India     Asia         2007   64.69800   1110396331   2452.2104

**I would to use tabke to have a first look and it seems that there are somthing intresting among population, year and gdp. Let's check it!**


```r
#### take China as an example
China <- gapminder %>% 
  filter(country == 'China') %>% 
  arrange(year,pop)
#knitr::kable(China)

ggplot(China, aes(pop, gdpPercap)) +
  geom_point(alpha = 0.5,colour = "blue") +
  ggtitle("Relationship between population and gdp")
```

![](explore-gapminder_files/figure-html/unnamed-chunk-14-1.png)<!-- -->

```r
ggplot(China, aes(year, gdpPercap)) +
  geom_point(alpha = 0.5,colour = "blue") +
  ggtitle("Relationship between year and gdp")
```

![](explore-gapminder_files/figure-html/unnamed-chunk-14-2.png)<!-- -->









**As I guessed before, gdp grows up with year and population**

***if we want to see the all relationships between variables, use cool pairs()***


```r
pairs(gapminder)
```

![](explore-gapminder_files/figure-html/unnamed-chunk-15-1.png)<!-- -->







***let's try put rainbow on garph***


```r
myData <- gapminder %>% dplyr::select(lifeExp)
binwidth = 0.5
library(ggplot2)   # CRAN version 2.2.1 used
n_bins <- length(ggplot2:::bin_breaks_width(range(myData), width = binwidth)$breaks) - 1L
ggplot() + 
  geom_histogram(aes(x = myData), binwidth = binwidth, fill = rainbow(n_bins)) +
  ggtitle("try rainbow()")
```

```
## Don't know how to automatically pick scale for object of type tbl_df/tbl/data.frame. Defaulting to continuous.
```

![](explore-gapminder_files/figure-html/unnamed-chunk-16-1.png)<!-- -->


***one graph first and then put on another***


```r
ggplot(gapminder, aes(lifeExp)) +
  geom_histogram(aes(y =..density..),fill = "blue",alpha = 0.1)+
  geom_density(color = "red")
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

![](explore-gapminder_files/figure-html/unnamed-chunk-17-1.png)<!-- -->



```r
gapminder %>% 
  filter(country == "Canada") %>% 
  ggplot(aes(year, pop)) +
  geom_jitter( colour = "green")+
  geom_violin(colour ="red")
```

![](explore-gapminder_files/figure-html/unnamed-chunk-18-1.png)<!-- -->

---
## Use filter(), select() and %>%
I used these functions in my hw02, expecially in **Explore various plot types**

 
 

 
---
## But I want to do more!


```r
afterFilter <- filter(gapminder, country == c("Rwanda", "Afghanistan"))
unique(afterFilter$country)
```

```
## [1] Afghanistan Rwanda     
## 142 Levels: Afghanistan Albania Algeria Angola Argentina ... Zimbabwe
```
**Answer: yes it is a correct way**
