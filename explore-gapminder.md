hw02
================

Smell test the data
-------------------

### Explore the gapminder object:

``` r
library(gapminder)
library(tidyverse)
library(dplyr)
```

-   #### Is it a data.frame, a matrix, a vector, a list?

``` r
inherits(gapminder,"data.frame") 
### or we can also use "str()"
str(gapminder)
```

  **<u> Answer: The function returns "True", so it is a data frame </u>. Using str() gives you that information plus extra goodies (such as the levels of your factors and the first few values of each variable)**

-   #### What is its class?

``` r
class(gapminder) 
```

  **<u> Answer: The class of gapminder is "data.frame" </u>. The function class prints the vector names of classes an object inherits from**

-   #### How many variables/columns?

``` r
ncol(gapminder) 
```

  **<u> Answer: The number of columns is 6 </u>. Also we can use str() function and then count the number of columns**

-   #### How many rows/observations?

``` r
nrow(gapminder) 
```

  **<u> Answer: The number of rows is 1704 </u>.**

-   #### Can you get these facts about “extent” or “size” in more than one way? Can you imagine different functions being useful in different contexts?

``` r
dim(gapminder) # this function can directly return the size
str(gapminder) # str() returns size and other info
nrow(gapminder) # nrow() can combine with ncol() to check the size of data
ncol(gapminder)
```

  **<u> Answer: 1704 rows and 6 columns </u>. dim() returns the dimensions of an object. rowNumber = dim(object)\[1\]; colNumber = dim(object)\[2\]**

-   #### What data type is each variable?

``` r
str(gapminder)
```

    ## Classes 'tbl_df', 'tbl' and 'data.frame':    1704 obs. of  6 variables:
    ##  $ country  : Factor w/ 142 levels "Afghanistan",..: 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ continent: Factor w/ 5 levels "Africa","Americas",..: 3 3 3 3 3 3 3 3 3 3 ...
    ##  $ year     : int  1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 ...
    ##  $ lifeExp  : num  28.8 30.3 32 34 36.1 ...
    ##  $ pop      : int  8425333 9240934 10267083 11537966 13079460 14880372 12881816 13867957 16317921 22227415 ...
    ##  $ gdpPercap: num  779 821 853 836 740 ...

  **<u> Answer: The type of each variable </u>:**

        + Country is factor
        + continent is also factor
        + year is int
        + lifeExp is numberic
        + pop is int

Explore various plot types
--------------------------

**There is a lot of data, but I only want to foucs on the information from Asia**

``` r
info_Asia <- gapminder %>% 
  filter(continent == 'Asia')
```

    ## Warning: package 'bindrcpp' was built under R version 3.5.1

``` r
summary(info_Asia$country)
info_Asia <-rename(info_Asia, cou = country)
ggplot(info_Asia, aes(cou, pop)) +
  geom_boxplot(aes(fill = cou)) +
  ggtitle("Distrubtion of pop in Asia")
```

![](explore-gapminder_files/figure-markdown_github/unnamed-chunk-11-1.png) ![](https://github.com/STAT545-UBC-students/hw02-Sukeysun/blob/master/pictures/unnamed-chunk-11-1.png)

***There are too many countries in my graph, but I only have interest in countries with huge population***

``` r
info_Asia <- gapminder %>% 
  filter(continent == 'Asia' & pop > 1000000000)
summary(info_Asia$country)
info_Asia <-rename(info_Asia, cou = country)
ggplot(info_Asia, aes(cou, pop)) +
  geom_boxplot(aes(fill = cou)) +
  ggtitle("Distrubtion of pop in Asia")
```

![](explore-gapminder_files/figure-markdown_github/unnamed-chunk-12-1.png) ![](https://github.com/STAT545-UBC-students/hw02-Sukeysun/blob/master/pictures/unnamed-chunk-12-1.png)

**According to the garph above, we can find that China and India are the countries with large population in Asia**

***Now I want to get more information of China and India, and find some differences***

``` r
China_India <- gapminder %>% 
  filter(country %in% c("China","India"))
dim(China_India)  ## check the size of China_India
```

    ## [1] 24  6

``` r
knitr::kable(China_India) ## use table presentation
```

| country | continent |  year|   lifeExp|         pop|  gdpPercap|
|:--------|:----------|-----:|---------:|-----------:|----------:|
| China   | Asia      |  1952|  44.00000|   556263527|   400.4486|
| China   | Asia      |  1957|  50.54896|   637408000|   575.9870|
| China   | Asia      |  1962|  44.50136|   665770000|   487.6740|
| China   | Asia      |  1967|  58.38112|   754550000|   612.7057|
| China   | Asia      |  1972|  63.11888|   862030000|   676.9001|
| China   | Asia      |  1977|  63.96736|   943455000|   741.2375|
| China   | Asia      |  1982|  65.52500|  1000281000|   962.4214|
| China   | Asia      |  1987|  67.27400|  1084035000|  1378.9040|
| China   | Asia      |  1992|  68.69000|  1164970000|  1655.7842|
| China   | Asia      |  1997|  70.42600|  1230075000|  2289.2341|
| China   | Asia      |  2002|  72.02800|  1280400000|  3119.2809|
| China   | Asia      |  2007|  72.96100|  1318683096|  4959.1149|
| India   | Asia      |  1952|  37.37300|   372000000|   546.5657|
| India   | Asia      |  1957|  40.24900|   409000000|   590.0620|
| India   | Asia      |  1962|  43.60500|   454000000|   658.3472|
| India   | Asia      |  1967|  47.19300|   506000000|   700.7706|
| India   | Asia      |  1972|  50.65100|   567000000|   724.0325|
| India   | Asia      |  1977|  54.20800|   634000000|   813.3373|
| India   | Asia      |  1982|  56.59600|   708000000|   855.7235|
| India   | Asia      |  1987|  58.55300|   788000000|   976.5127|
| India   | Asia      |  1992|  60.22300|   872000000|  1164.4068|
| India   | Asia      |  1997|  61.76500|   959000000|  1458.8174|
| India   | Asia      |  2002|  62.87900|  1034172547|  1746.7695|
| India   | Asia      |  2007|  64.69800|  1110396331|  2452.2104|

**I would to use tabke to have a first look and it seems that there are somthing intresting among population, year and gdp. Let's check it!**

``` r
#### take China as an example
China <- gapminder %>% 
  filter(country == 'China') %>% 
  arrange(year,pop)
#knitr::kable(China)

ggplot(China, aes(pop, gdpPercap)) +
  geom_point(alpha = 0.5,colour = "blue") +
  ggtitle("Relationship between population and gdp")
```

![](explore-gapminder_files/figure-markdown_github/unnamed-chunk-14-1.png)

``` r
ggplot(China, aes(year, gdpPercap)) +
  geom_point(alpha = 0.5,colour = "blue") +
  ggtitle("Relationship between year and gdp")
```

![](explore-gapminder_files/figure-markdown_github/unnamed-chunk-14-2.png)

![](https://github.com/STAT545-UBC-students/hw02-Sukeysun/blob/master/pictures/unnamed-chunk-14-1.png) ![](https://github.com/STAT545-UBC-students/hw02-Sukeysun/blob/master/pictures/unnamed-chunk-14-2.png)

**As I guessed before, gdp grows up with year and population**

***if we want to see the all relationships between variables, use cool pairs()***

``` r
pairs(gapminder)
```

![](explore-gapminder_files/figure-markdown_github/unnamed-chunk-15-1.png)

![](https://github.com/STAT545-UBC-students/hw02-Sukeysun/blob/master/pictures/unnamed-chunk-15-1.png)

***let's try put rainbow on garph***

``` r
myData <- gapminder %>% dplyr::select(lifeExp)
binwidth = 0.5
library(ggplot2)   # CRAN version 2.2.1 used
n_bins <- length(ggplot2:::bin_breaks_width(range(myData), width = binwidth)$breaks) - 1L
ggplot() + 
  geom_histogram(aes(x = myData), binwidth = binwidth, fill = rainbow(n_bins)) +
  ggtitle("try rainbow()")
```

    ## Don't know how to automatically pick scale for object of type tbl_df/tbl/data.frame. Defaulting to continuous.

![](explore-gapminder_files/figure-markdown_github/unnamed-chunk-16-1.png) ![](https://github.com/STAT545-UBC-students/hw02-Sukeysun/blob/master/pictures/unnamed-chunk-16-1.png)

***one graph first and then put on another***

``` r
ggplot(gapminder, aes(lifeExp)) +
  geom_histogram(aes(y =..density..),fill = "blue",alpha = 0.1)+
  geom_density(color = "red")
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](explore-gapminder_files/figure-markdown_github/unnamed-chunk-17-1.png)

![](https://github.com/STAT545-UBC-students/hw02-Sukeysun/blob/master/pictures/unnamed-chunk-17-1.png)

``` r
gapminder %>% 
  filter(country == "Canada") %>% 
  ggplot(aes(year, pop)) +
  geom_jitter( colour = "green")+
  geom_violin(colour ="red")
```

![](explore-gapminder_files/figure-markdown_github/unnamed-chunk-18-1.png) ![](https://github.com/STAT545-UBC-students/hw02-Sukeysun/blob/master/pictures/unnamed-chunk-18-1.png)

But I want to do more!
----------------------

``` r
afterFilter <- filter(gapminder, country == c("Rwanda", "Afghanistan"))
unique(afterFilter$country)
```

    ## [1] Afghanistan Rwanda     
    ## 142 Levels: Afghanistan Albania Algeria Angola Argentina ... Zimbabwe

**Answer: yes it is a correct way. By using unique(), we can find that after filtering, only information from "Rwanda" and "Afghanistan" left. Let's check it at a look at table**

``` r
knitr::kable(afterFilter)
```

| country     | continent |  year|  lifeExp|       pop|  gdpPercap|
|:------------|:----------|-----:|--------:|---------:|----------:|
| Afghanistan | Asia      |  1957|   30.332|   9240934|   820.8530|
| Afghanistan | Asia      |  1967|   34.020|  11537966|   836.1971|
| Afghanistan | Asia      |  1977|   38.438|  14880372|   786.1134|
| Afghanistan | Asia      |  1987|   40.822|  13867957|   852.3959|
| Afghanistan | Asia      |  1997|   41.763|  22227415|   635.3414|
| Afghanistan | Asia      |  2007|   43.828|  31889923|   974.5803|
| Rwanda      | Africa    |  1952|   40.000|   2534927|   493.3239|
| Rwanda      | Africa    |  1962|   43.000|   3051242|   597.4731|
| Rwanda      | Africa    |  1972|   44.600|   3992121|   590.5807|
| Rwanda      | Africa    |  1982|   46.218|   5507565|   881.5706|
| Rwanda      | Africa    |  1992|   23.599|   7290203|   737.0686|
| Rwanda      | Africa    |  2002|   43.413|   7852401|   785.6538|

**Use more of the dplyr functions for operating on a single table.**
**Now, I would like to use filter() to choose the information from "Asia", and then sort the information according to year**

``` r
temp1 <- filter(afterFilter, continent == "Asia") %>% 
  arrange(year)

knitr::kable(temp1)
```

| country     | continent |  year|  lifeExp|       pop|  gdpPercap|
|:------------|:----------|-----:|--------:|---------:|----------:|
| Afghanistan | Asia      |  1957|   30.332|   9240934|   820.8530|
| Afghanistan | Asia      |  1967|   34.020|  11537966|   836.1971|
| Afghanistan | Asia      |  1977|   38.438|  14880372|   786.1134|
| Afghanistan | Asia      |  1987|   40.822|  13867957|   852.3959|
| Afghanistan | Asia      |  1997|   41.763|  22227415|   635.3414|
| Afghanistan | Asia      |  2007|   43.828|  31889923|   974.5803|
