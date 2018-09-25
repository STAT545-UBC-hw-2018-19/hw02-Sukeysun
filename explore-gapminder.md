Explore gapminder
================
sukey
September 20, 2018

Smell test the data
===================

Explore the gapminder object:
-----------------------------

-   Is it a data.frame, a matrix, a vector, a list?

``` r
library(gapminder)
```

    ## Warning: package 'gapminder' was built under R version 3.5.1

``` r
library(tidyverse)
```

    ## Warning: package 'tidyverse' was built under R version 3.5.1

    ## -- Attaching packages ------------------------------------------------------------------ tidyverse 1.2.1 --

    ## v ggplot2 2.2.1     v purrr   0.2.5
    ## v tibble  1.4.2     v dplyr   0.7.6
    ## v tidyr   0.8.1     v stringr 1.3.1
    ## v readr   1.1.1     v forcats 0.3.0

    ## Warning: package 'tidyr' was built under R version 3.5.1

    ## Warning: package 'readr' was built under R version 3.5.1

    ## Warning: package 'purrr' was built under R version 3.5.1

    ## Warning: package 'dplyr' was built under R version 3.5.1

    ## Warning: package 'forcats' was built under R version 3.5.1

    ## -- Conflicts --------------------------------------------------------------------- tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
inherits(gapminder,"data.frame") # It is a data frame
```

    ## [1] TRUE

-   What is its class?

``` r
class(gapminder) # The class of gapminder is shown as "tbl_df" "tbl" "data.frame"
```

    ## [1] "tbl_df"     "tbl"        "data.frame"

-   How many variables/columns?

``` r
ncol(gapminder) # The number of columns is 6
```

    ## [1] 6

-   How many rows/observations?

``` r
nrow(gapminder) # The number of rows is 1704
```

    ## [1] 1704

-   Can you get these facts about “extent” or “size” in more than one way? Can you imagine different functions being useful in different contexts?

``` r
dim(gapminder)  # 1704 rows and 6 columns
```

    ## [1] 1704    6

-   What data type is each variable?

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

Be sure to justify your answers by calling the appropriate R functions.
