---
title: 'MATH 216 - Notes: Transformation'
author: "Emily Malcolm-White"
output: 
  html_document:
    toc: true
    toc_float: true
    theme: yeti
---

# Loading the tidyverse

The tidyverse is an opinionated collection of R packages designed for data science. Make sure that you have the tidyverse installed by typing `install.packages("tidyverse")` into the Console in the bottom left corner. You only need to do this once. 


```r
#Within each document, it is important to call the tidyverse package so it knows you will be using functions/data/etc from inside that package
library(tidyverse)
```

```
## ── Attaching packages ──────────────────────────────────────────────────── tidyverse 1.3.0 ──
```

```
## ✔ ggplot2 3.2.1     ✔ purrr   0.3.3
## ✔ tibble  2.1.3     ✔ dplyr   0.8.3
## ✔ tidyr   1.0.0     ✔ stringr 1.4.0
## ✔ readr   1.3.1     ✔ forcats 0.4.0
```

```
## ── Conflicts ─────────────────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
```



# ![](https://github.com/rstudio/hex-stickers/blob/master/PNG/tibble.png?raw=true){width=50px} `tibble` 

For the next little while we will work with “tibbles” instead of R’s traditional data.frame. Tibbles are data frames, but they tweak some older behaviors to make life a little easier.

Tibbles have a refined print method that shows only the first 10 rows, and all the columns that fit on screen. This makes it much easier to work with large data. Tibbles are designed so that you don’t accidentally overwhelm your console when you print large data frames. 


We will be working with the `diamonds` dataset that is contained within the `tidyverse` package.


```r
#to load data
data(diamonds)

#to learn about dataset
?diamonds
```


# ![](https://github.com/maxogden/hexbin/blob/gh-pages/hexagons/dplyr.png?raw=true){width=50px} `Dplyr` 


## Choosing Columns with `select()`:

![swcarpentry](http://swcarpentry.github.io/r-novice-gapminder/fig/13-dplyr-fig1.png){width=200pt}


```r
#select( dataset, columns wanted)
# selects from the diamonds dataset only 4 columns (carot, cut, color, and clarity)
select(.data = diamonds, carat, cut, color, clarity ) 
```

```
## # A tibble: 53,940 x 4
##    carat cut       color clarity
##    <dbl> <ord>     <ord> <ord>  
##  1 0.23  Ideal     E     SI2    
##  2 0.21  Premium   E     SI1    
##  3 0.23  Good      E     VS1    
##  4 0.290 Premium   I     VS2    
##  5 0.31  Good      J     SI2    
##  6 0.24  Very Good J     VVS2   
##  7 0.24  Very Good I     VVS1   
##  8 0.26  Very Good H     SI1    
##  9 0.22  Fair      E     VS2    
## 10 0.23  Very Good H     VS1    
## # … with 53,930 more rows
```


## Renaming variables with `rename()`:


```r
rename(.data=diamonds, 
        table_in_mm = table)
```

```
## # A tibble: 53,940 x 10
##    carat cut       color clarity depth table_in_mm price     x     y     z
##    <dbl> <ord>     <ord> <ord>   <dbl>       <dbl> <int> <dbl> <dbl> <dbl>
##  1 0.23  Ideal     E     SI2      61.5          55   326  3.95  3.98  2.43
##  2 0.21  Premium   E     SI1      59.8          61   326  3.89  3.84  2.31
##  3 0.23  Good      E     VS1      56.9          65   327  4.05  4.07  2.31
##  4 0.290 Premium   I     VS2      62.4          58   334  4.2   4.23  2.63
##  5 0.31  Good      J     SI2      63.3          58   335  4.34  4.35  2.75
##  6 0.24  Very Good J     VVS2     62.8          57   336  3.94  3.96  2.48
##  7 0.24  Very Good I     VVS1     62.3          57   336  3.95  3.98  2.47
##  8 0.26  Very Good H     SI1      61.9          55   337  4.07  4.11  2.53
##  9 0.22  Fair      E     VS2      65.1          61   337  3.87  3.78  2.49
## 10 0.23  Very Good H     VS1      59.4          61   338  4     4.05  2.39
## # … with 53,930 more rows
```


## Sorting and Reordering with `arrange()`:


```r
#displays table with carrots from smallest to largest
arrange(.data=diamonds, 
        carat)
```

```
## # A tibble: 53,940 x 10
##    carat cut       color clarity depth table price     x     y     z
##    <dbl> <ord>     <ord> <ord>   <dbl> <dbl> <int> <dbl> <dbl> <dbl>
##  1   0.2 Premium   E     SI2      60.2    62   345  3.79  3.75  2.27
##  2   0.2 Premium   E     VS2      59.8    62   367  3.79  3.77  2.26
##  3   0.2 Premium   E     VS2      59      60   367  3.81  3.78  2.24
##  4   0.2 Premium   E     VS2      61.1    59   367  3.81  3.78  2.32
##  5   0.2 Premium   E     VS2      59.7    62   367  3.84  3.8   2.28
##  6   0.2 Ideal     E     VS2      59.7    55   367  3.86  3.84  2.3 
##  7   0.2 Premium   F     VS2      62.6    59   367  3.73  3.71  2.33
##  8   0.2 Ideal     D     VS2      61.5    57   367  3.81  3.77  2.33
##  9   0.2 Very Good E     VS2      63.4    59   367  3.74  3.71  2.36
## 10   0.2 Ideal     E     VS2      62.2    57   367  3.76  3.73  2.33
## # … with 53,930 more rows
```

```r
#displays table with carrots from largest to smallest
arrange(.data=diamonds, 
        -carat)
```

```
## # A tibble: 53,940 x 10
##    carat cut       color clarity depth table price     x     y     z
##    <dbl> <ord>     <ord> <ord>   <dbl> <dbl> <int> <dbl> <dbl> <dbl>
##  1  5.01 Fair      J     I1       65.5    59 18018 10.7  10.5   6.98
##  2  4.5  Fair      J     I1       65.8    58 18531 10.2  10.2   6.72
##  3  4.13 Fair      H     I1       64.8    61 17329 10     9.85  6.43
##  4  4.01 Premium   I     I1       61      61 15223 10.1  10.1   6.17
##  5  4.01 Premium   J     I1       62.5    62 15223 10.0   9.94  6.24
##  6  4    Very Good I     I1       63.3    58 15984 10.0   9.94  6.31
##  7  3.67 Premium   I     I1       62.4    56 16193  9.86  9.81  6.13
##  8  3.65 Fair      H     I1       67.1    53 11668  9.53  9.48  6.38
##  9  3.51 Premium   J     VS2      62.5    59 18701  9.66  9.63  6.03
## 10  3.5  Ideal     H     I1       62.8    57 12587  9.65  9.59  6.03
## # … with 53,930 more rows
```

## Adding new columns using `dplyr`'s `mutate()`:


```r
mutate(.data=diamonds, volume=x*y*z)
```

```
## # A tibble: 53,940 x 11
##    carat cut       color clarity depth table price     x     y     z volume
##    <dbl> <ord>     <ord> <ord>   <dbl> <dbl> <int> <dbl> <dbl> <dbl>  <dbl>
##  1 0.23  Ideal     E     SI2      61.5    55   326  3.95  3.98  2.43   38.2
##  2 0.21  Premium   E     SI1      59.8    61   326  3.89  3.84  2.31   34.5
##  3 0.23  Good      E     VS1      56.9    65   327  4.05  4.07  2.31   38.1
##  4 0.290 Premium   I     VS2      62.4    58   334  4.2   4.23  2.63   46.7
##  5 0.31  Good      J     SI2      63.3    58   335  4.34  4.35  2.75   51.9
##  6 0.24  Very Good J     VVS2     62.8    57   336  3.94  3.96  2.48   38.7
##  7 0.24  Very Good I     VVS1     62.3    57   336  3.95  3.98  2.47   38.8
##  8 0.26  Very Good H     SI1      61.9    55   337  4.07  4.11  2.53   42.3
##  9 0.22  Fair      E     VS2      65.1    61   337  3.87  3.78  2.49   36.4
## 10 0.23  Very Good H     VS1      59.4    61   338  4     4.05  2.39   38.7
## # … with 53,930 more rows
```


## Subsetting and Filtering Data with `filter()`:


```r
#displays all rows in diamonds dataset whose price is more than 12000
filter(.data = diamonds, 
       price > 12000) 
```

```
## # A tibble: 3,463 x 10
##    carat cut       color clarity depth table price     x     y     z
##    <dbl> <ord>     <ord> <ord>   <dbl> <dbl> <int> <dbl> <dbl> <dbl>
##  1  1.57 Ideal     H     VS2      61.8    55 12004  7.45  7.49  4.62
##  2  1.5  Very Good G     VS1      63.4    59 12005  7.25  7.19  4.58
##  3  1.31 Ideal     G     VS1      61.6    57 12008  6.99  7.04  4.32
##  4  1.5  Ideal     G     SI1      61      57 12009  7.38  7.41  4.51
##  5  1.75 Very Good D     SI2      60.7    57 12012  7.78  7.83  4.74
##  6  1.52 Premium   H     VVS2     63      60 12013  7.3   7.25  4.58
##  7  1.5  Very Good G     VS2      60.5    57 12014  7.39  7.43  4.48
##  8  1.11 Ideal     D     VVS2     63      57 12016  6.58  6.65  4.17
##  9  2.03 Premium   F     SI2      60.9    59 12021  8.15  8.11  4.95
## 10  1.61 Very Good G     SI1      62.6    56 12028  7.44  7.54  4.69
## # … with 3,453 more rows
```

```r
#creates a new dataset called `expensive.diamonds` 
expensive.diamonds <- filter(.data = diamonds,
                             price > 12000)
```



```r
#Find color D or E diamonds
expensive.pretty.diamonds <- filter(expensive.diamonds, 
                                    color == "D" | color == "E")
```


```r
expensive.pretty.diamonds
```

```
## # A tibble: 624 x 10
##    carat cut       color clarity depth table price     x     y     z
##    <dbl> <ord>     <ord> <ord>   <dbl> <dbl> <int> <dbl> <dbl> <dbl>
##  1  1.75 Very Good D     SI2      60.7    57 12012  7.78  7.83  4.74
##  2  1.11 Ideal     D     VVS2     63      57 12016  6.58  6.65  4.17
##  3  1.7  Very Good E     SI2      63.3    57 12030  7.59  7.51  4.78
##  4  1.02 Ideal     E     IF       62.2    56 12030  6.44  6.38  3.99
##  5  1.07 Ideal     E     VVS2     61.3    56 12031  6.57  6.62  4.04
##  6  1.02 Ideal     E     VVS1     62.2    58 12035  6.42  6.44  4   
##  7  1.22 Ideal     E     VVS2     63      55 12036  6.83  6.78  4.29
##  8  1.74 Premium   D     SI2      61.9    58 12052  7.73  7.67  4.77
##  9  1.06 Ideal     D     VVS2     62      56 12053  6.53  6.57  4.06
## 10  1.5  Very Good D     SI1      60      59 12060  7.41  7.46  4.46
## # … with 614 more rows
```



```r
# is_tibble (check whether an data object is a tibble)
# as_tibble (treat the data object like a tibble)
```

### RStudio's `dplyr` cheatsheet
[https://github.com/rstudio/cheatsheets/raw/master/data-transformation.pdf](https://github.com/rstudio/cheatsheets/raw/master/data-transformation.pdf)


#  ![](https://github.com/maxogden/hexbin/blob/gh-pages/hexagons/pipe.png?raw=true){width=50px} `%>%` (Piping) 

The pipe, `%>%`, comes from the `magrittr` package by Stefan Milton Bache. Packages in the tidyverse load `%>%` for you automatically, so you don’t usually load `magrittr` explicitly. 

The point of the pipe is to help you write code in a way that is easier to read and understand. 


```r
# without piping
filter(.data = diamonds, 
       price > 12000) 
```

```
## # A tibble: 3,463 x 10
##    carat cut       color clarity depth table price     x     y     z
##    <dbl> <ord>     <ord> <ord>   <dbl> <dbl> <int> <dbl> <dbl> <dbl>
##  1  1.57 Ideal     H     VS2      61.8    55 12004  7.45  7.49  4.62
##  2  1.5  Very Good G     VS1      63.4    59 12005  7.25  7.19  4.58
##  3  1.31 Ideal     G     VS1      61.6    57 12008  6.99  7.04  4.32
##  4  1.5  Ideal     G     SI1      61      57 12009  7.38  7.41  4.51
##  5  1.75 Very Good D     SI2      60.7    57 12012  7.78  7.83  4.74
##  6  1.52 Premium   H     VVS2     63      60 12013  7.3   7.25  4.58
##  7  1.5  Very Good G     VS2      60.5    57 12014  7.39  7.43  4.48
##  8  1.11 Ideal     D     VVS2     63      57 12016  6.58  6.65  4.17
##  9  2.03 Premium   F     SI2      60.9    59 12021  8.15  8.11  4.95
## 10  1.61 Very Good G     SI1      62.6    56 12028  7.44  7.54  4.69
## # … with 3,453 more rows
```

```r
# with piping
diamonds %>%
  filter(price >12000)
```

```
## # A tibble: 3,463 x 10
##    carat cut       color clarity depth table price     x     y     z
##    <dbl> <ord>     <ord> <ord>   <dbl> <dbl> <int> <dbl> <dbl> <dbl>
##  1  1.57 Ideal     H     VS2      61.8    55 12004  7.45  7.49  4.62
##  2  1.5  Very Good G     VS1      63.4    59 12005  7.25  7.19  4.58
##  3  1.31 Ideal     G     VS1      61.6    57 12008  6.99  7.04  4.32
##  4  1.5  Ideal     G     SI1      61      57 12009  7.38  7.41  4.51
##  5  1.75 Very Good D     SI2      60.7    57 12012  7.78  7.83  4.74
##  6  1.52 Premium   H     VVS2     63      60 12013  7.3   7.25  4.58
##  7  1.5  Very Good G     VS2      60.5    57 12014  7.39  7.43  4.48
##  8  1.11 Ideal     D     VVS2     63      57 12016  6.58  6.65  4.17
##  9  2.03 Premium   F     SI2      60.9    59 12021  8.15  8.11  4.95
## 10  1.61 Very Good G     SI1      62.6    56 12028  7.44  7.54  4.69
## # … with 3,453 more rows
```

This can be particularly useful when you want to do multiple operations. 


```r
#Most efficient way
#prints out diamonds that are more than $12000, have colors D and E, and only prints out four columns
diamonds %>%
  filter(price > 12000) %>%
  filter(color == "D" | color == "E") %>%
  select(carat, cut, color, price)
```

```
## # A tibble: 624 x 4
##    carat cut       color price
##    <dbl> <ord>     <ord> <int>
##  1  1.75 Very Good D     12012
##  2  1.11 Ideal     D     12016
##  3  1.7  Very Good E     12030
##  4  1.02 Ideal     E     12030
##  5  1.07 Ideal     E     12031
##  6  1.02 Ideal     E     12035
##  7  1.22 Ideal     E     12036
##  8  1.74 Premium   D     12052
##  9  1.06 Ideal     D     12053
## 10  1.5  Very Good D     12060
## # … with 614 more rows
```



## `summarize()` and `group_by()`


```r
diamonds %>%
  summarize(mean.price = mean(price))
```

```
## # A tibble: 1 x 1
##   mean.price
##        <dbl>
## 1      3933.
```

```r
diamonds %>%
  group_by(color) %>%
  summarize(mean.price = mean(price))
```

```
## # A tibble: 7 x 2
##   color mean.price
##   <ord>      <dbl>
## 1 D          3170.
## 2 E          3077.
## 3 F          3725.
## 4 G          3999.
## 5 H          4487.
## 6 I          5092.
## 7 J          5324.
```

```r
diamonds %>%
  group_by(color, cut) %>%
  summarize(mean.price = mean(price),
            max.price = max(price),
            min.price = min(price),
            count = n())
```

```
## # A tibble: 35 x 6
## # Groups:   color [7]
##    color cut       mean.price max.price min.price count
##    <ord> <ord>          <dbl>     <int>     <int> <int>
##  1 D     Fair           4291.     16386       536   163
##  2 D     Good           3405.     18468       361   662
##  3 D     Very Good      3470.     18542       357  1513
##  4 D     Premium        3631.     18575       367  1603
##  5 D     Ideal          2629.     18693       367  2834
##  6 E     Fair           3682.     15584       337   224
##  7 E     Good           3424.     18236       327   933
##  8 E     Very Good      3215.     18731       352  2400
##  9 E     Premium        3539.     18477       326  2337
## 10 E     Ideal          2598.     18729       326  3903
## # … with 25 more rows
```

## Challenge: 

Identify the most expensive diamond with greater than 2 carats, that doesn't belong to the "worst" 2 colors.


```r
#many possible different answers (see Slack)
diamonds %>%
  filter(carat > 2) %>%
  filter(color != "I",color != "J") %>%
  filter(price == max(price))
```

```
## # A tibble: 1 x 10
##   carat cut   color clarity depth table price     x     y     z
##   <dbl> <ord> <ord> <ord>   <dbl> <dbl> <int> <dbl> <dbl> <dbl>
## 1  2.07 Ideal G     SI2      62.5    55 18804   8.2  8.13  5.11
```


# ![](https://github.com/rstudio/hex-stickers/blob/master/PNG/tidyr.png?raw=true){width=50px} `tidyr` 

The goal of tidyr is to help you create tidy data. Tidy data is data where:
- Every column is variable.
- Every row is an observation..
- Every cell is a single value.

Wide Data and Long Data: 
![](https://swcarpentry.github.io/r-novice-gapminder/fig/14-tidyr-fig1.png)


```r
#if you haven't already run install.packages("tidyr"), you only need to do this once
#load in the tidyr package, you need to do this once in each .Rmd you plan to use these commands for
library("tidyr")
```


```r
#create a wide dataset 
set.seed(1)
stocks_wide <- data.frame(
   time = as.Date('2009-01-01') + 0:9,
   X = rnorm(10, 20, 1),
   Y = rnorm(10, 20, 2),
   Z = rnorm(10, 20, 4)
 )
stocks_wide
```

```
##          time        X        Y        Z
## 1  2009-01-01 19.37355 23.02356 23.67591
## 2  2009-01-02 20.18364 20.77969 23.12855
## 3  2009-01-03 19.16437 18.75752 20.29826
## 4  2009-01-04 21.59528 15.57060 12.04259
## 5  2009-01-05 20.32951 22.24986 22.47930
## 6  2009-01-06 19.17953 19.91013 19.77549
## 7  2009-01-07 20.48743 19.96762 19.37682
## 8  2009-01-08 20.73832 21.88767 14.11699
## 9  2009-01-09 20.57578 21.64244 18.08740
## 10 2009-01-10 19.69461 21.18780 21.67177
```
## `gather()` is used to convert from wide to long

```r
# gather(.data = data, key, value)
# OR
# data %>%  
#   gather(key = "key", value = "value")


#stocks_wide %>% 
#  gather(key = stock, value = price, X, Y,Z) 

stocks_long <- stocks_wide %>% 
  gather(key = stock, value = price, X:Z)

stocks_long
```

```
##          time stock    price
## 1  2009-01-01     X 19.37355
## 2  2009-01-02     X 20.18364
## 3  2009-01-03     X 19.16437
## 4  2009-01-04     X 21.59528
## 5  2009-01-05     X 20.32951
## 6  2009-01-06     X 19.17953
## 7  2009-01-07     X 20.48743
## 8  2009-01-08     X 20.73832
## 9  2009-01-09     X 20.57578
## 10 2009-01-10     X 19.69461
## 11 2009-01-01     Y 23.02356
## 12 2009-01-02     Y 20.77969
## 13 2009-01-03     Y 18.75752
## 14 2009-01-04     Y 15.57060
## 15 2009-01-05     Y 22.24986
## 16 2009-01-06     Y 19.91013
## 17 2009-01-07     Y 19.96762
## 18 2009-01-08     Y 21.88767
## 19 2009-01-09     Y 21.64244
## 20 2009-01-10     Y 21.18780
## 21 2009-01-01     Z 23.67591
## 22 2009-01-02     Z 23.12855
## 23 2009-01-03     Z 20.29826
## 24 2009-01-04     Z 12.04259
## 25 2009-01-05     Z 22.47930
## 26 2009-01-06     Z 19.77549
## 27 2009-01-07     Z 19.37682
## 28 2009-01-08     Z 14.11699
## 29 2009-01-09     Z 18.08740
## 30 2009-01-10     Z 21.67177
```

## `spread()` reshapes long data into wide

```r
# spread(.data=data, key, value)
# OR
# data %>% 
#     spread(key, value)

stocks_long %>% 
  spread(key=stock, value=price)
```

```
##          time        X        Y        Z
## 1  2009-01-01 19.37355 23.02356 23.67591
## 2  2009-01-02 20.18364 20.77969 23.12855
## 3  2009-01-03 19.16437 18.75752 20.29826
## 4  2009-01-04 21.59528 15.57060 12.04259
## 5  2009-01-05 20.32951 22.24986 22.47930
## 6  2009-01-06 19.17953 19.91013 19.77549
## 7  2009-01-07 20.48743 19.96762 19.37682
## 8  2009-01-08 20.73832 21.88767 14.11699
## 9  2009-01-09 20.57578 21.64244 18.08740
## 10 2009-01-10 19.69461 21.18780 21.67177
```
These commands can be utilized in conjunction with the `dplyr` commands we were discussing previously. 

```r
#Ex: 

stocks_wide %>% 
  gather(stock, price, X, Y, Z) %>% 
  group_by(stock) %>% 
  summarise(min=min(price), max=max(price))
```

```
## # A tibble: 3 x 3
##   stock   min   max
##   <chr> <dbl> <dbl>
## 1 X      19.2  21.6
## 2 Y      15.6  23.0
## 3 Z      12.0  23.7
```
There are other similar functions available. 
## `separate()` splits a single variable into two

```r
#separate(data, col, into, sep)
#to split up date
```
## `unite()` merges two variables into one

```r
#unite(data, col, sep)
```



# ![](https://github.com/rstudio/hex-stickers/blob/master/PNG/stringr.png?raw=true){width=50px} `stringr` 

The `stringr` package provide a set of functions designed to make working with strings as easy as possible. 

### RStudio's `stringr` cheatsheet
[https://github.com/rstudio/cheatsheets/raw/master/strings.pdf](https://github.com/rstudio/cheatsheets/raw/master/strings.pdf)
