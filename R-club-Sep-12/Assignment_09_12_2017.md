# Assignment_09_12_2017
Ruijuan Li  
9/12/2017  


```r
library(tidyverse)
```

```
## Warning: package 'tidyverse' was built under R version 3.2.5
```

```
## Loading tidyverse: ggplot2
## Loading tidyverse: tibble
## Loading tidyverse: tidyr
## Loading tidyverse: readr
## Loading tidyverse: purrr
## Loading tidyverse: dplyr
```

```
## Warning: package 'ggplot2' was built under R version 3.2.5
```

```
## Warning: package 'tibble' was built under R version 3.2.5
```

```
## Warning: package 'tidyr' was built under R version 3.2.5
```

```
## Warning: package 'readr' was built under R version 3.2.5
```

```
## Warning: package 'purrr' was built under R version 3.2.5
```

```
## Warning: package 'dplyr' was built under R version 3.2.5
```

```
## Conflicts with tidy packages ----------------------------------------------
```

```
## filter(): dplyr, stats
## lag():    dplyr, stats
```

```r
library(nycflights13)
```

```
## Warning: package 'nycflights13' was built under R version 3.2.5
```

### 21.5.3 Exercises

1. Write code that uses one of the map functions to:

      1. Compute the mean of every column in mtcars.
      2. Determine the type of each column in nycflights13::flights.
      3. Compute the number of unique values in each column of iris.
      4. Generate 10 random normals for each of μ= −10, 0, 10, and 100.
      

```r
# 1) 
map(mtcars, mean)
```

```
## $mpg
## [1] 20.09062
## 
## $cyl
## [1] 6.1875
## 
## $disp
## [1] 230.7219
## 
## $hp
## [1] 146.6875
## 
## $drat
## [1] 3.596563
## 
## $wt
## [1] 3.21725
## 
## $qsec
## [1] 17.84875
## 
## $vs
## [1] 0.4375
## 
## $am
## [1] 0.40625
## 
## $gear
## [1] 3.6875
## 
## $carb
## [1] 2.8125
```

```r
# 2)
map(flights, typeof)
```

```
## $year
## [1] "integer"
## 
## $month
## [1] "integer"
## 
## $day
## [1] "integer"
## 
## $dep_time
## [1] "integer"
## 
## $sched_dep_time
## [1] "integer"
## 
## $dep_delay
## [1] "double"
## 
## $arr_time
## [1] "integer"
## 
## $sched_arr_time
## [1] "integer"
## 
## $arr_delay
## [1] "double"
## 
## $carrier
## [1] "character"
## 
## $flight
## [1] "integer"
## 
## $tailnum
## [1] "character"
## 
## $origin
## [1] "character"
## 
## $dest
## [1] "character"
## 
## $air_time
## [1] "double"
## 
## $distance
## [1] "double"
## 
## $hour
## [1] "double"
## 
## $minute
## [1] "double"
## 
## $time_hour
## [1] "double"
```

```r
# 3) 
map(iris, unique) %>% map(length)
```

```
## $Sepal.Length
## [1] 35
## 
## $Sepal.Width
## [1] 23
## 
## $Petal.Length
## [1] 43
## 
## $Petal.Width
## [1] 22
## 
## $Species
## [1] 3
```

```r
# 4) 
map(c(-10, 0, 10, 100), function(i) rnorm(n = 10, mean = i))
```

```
## [[1]]
##  [1] -11.458612  -8.734078  -9.240971 -10.521174 -11.244067 -10.485652
##  [7] -10.644800 -10.449331  -8.813286 -10.601788
## 
## [[2]]
##  [1]  1.6931105  1.1220280 -2.5378237 -0.6517515  1.8618478 -0.6147704
##  [7] -0.4574191 -0.5366750 -0.9811426  2.2167706
## 
## [[3]]
##  [1]  9.709597  8.520312 10.172329  9.485095  9.179921 10.559439 11.210876
##  [8] 10.098054  9.658353  9.293666
## 
## [[4]]
##  [1]  99.77012 101.58127  99.66003 100.75376  99.85961  98.41199  98.42513
##  [8] 100.90212 100.23641  98.26163
```

2. How can you create a single vector that for each column in a data frame indicates whether or not it’s a factor?

```r
map_lgl(mtcars, is.factor) # ??? don't understand the Q. 
```

```
##   mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb 
## FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
```

3. What happens when you use the map functions on vectors that aren’t lists? What does map(1:5, runif) do? Why?

```r
map(1:5, runif) 
```

```
## [[1]]
## [1] 0.7374035
## 
## [[2]]
## [1] 0.9573150 0.6728395
## 
## [[3]]
## [1] 0.3837269 0.8300718 0.6594728
## 
## [[4]]
## [1] 0.4349473 0.2594982 0.1977375 0.3023285
## 
## [[5]]
## [1] 0.3322863 0.7086670 0.5461994 0.2341886 0.5918909
```

```r
?map
```
still gives list output, because "map() returns a list"

4. What does map(-2:2, rnorm, n = 5) do? Why? What does map_dbl(-2:2, rnorm, n = 5) do? Why?

```r
map(-2:2, rnorm, n = 5) # generate 5 normal number using mean from -2 to 2, output as a list 
```

```
## [[1]]
## [1] -2.681893 -3.124345 -2.095098 -1.924127 -3.877516
## 
## [[2]]
## [1] -0.7751768 -0.7697415 -1.6089894 -1.7372440 -0.4863339
## 
## [[3]]
## [1]  0.6472948 -0.0908395 -0.3347212 -0.4830433 -0.6449730
## 
## [[4]]
## [1]  0.75583838 -0.01967176  2.17414110  2.84841222  5.53673458
## 
## [[5]]
## [1] 1.2794915 2.4463026 0.8616865 0.3347909 2.3222071
```

```r
map_dbl(-2:2, rnorm, n = 5)  
```

```
## Error: Result 1 is not a length 1 atomic vector
```

```r
map_dbl(-2:2, rnorm, n = 1) 
```

```
## [1] -2.50217243  0.77743476  0.02332315  0.33744404  3.21400852
```

```r
# map_dbl() returns a double vector which is the same length as the input, when n is 5, map_dbl() cannot satisfy both 
```

5. Rewrite map(x, function(df) lm(mpg ~ wt, data = df)) to eliminate the anonymous function.

```r
mtcars %>% 
  split(.$cyl) %>% 
  map(function(df) lm(mpg ~ wt, data = df)) 
```

```
## $`4`
## 
## Call:
## lm(formula = mpg ~ wt, data = df)
## 
## Coefficients:
## (Intercept)           wt  
##      39.571       -5.647  
## 
## 
## $`6`
## 
## Call:
## lm(formula = mpg ~ wt, data = df)
## 
## Coefficients:
## (Intercept)           wt  
##       28.41        -2.78  
## 
## 
## $`8`
## 
## Call:
## lm(formula = mpg ~ wt, data = df)
## 
## Coefficients:
## (Intercept)           wt  
##      23.868       -2.192
```

```r
mtcars %>% 
  split(.$cyl) %>% 
  map(~lm(mpg ~ wt, data = .))  
```

```
## $`4`
## 
## Call:
## lm(formula = mpg ~ wt, data = .)
## 
## Coefficients:
## (Intercept)           wt  
##      39.571       -5.647  
## 
## 
## $`6`
## 
## Call:
## lm(formula = mpg ~ wt, data = .)
## 
## Coefficients:
## (Intercept)           wt  
##       28.41        -2.78  
## 
## 
## $`8`
## 
## Call:
## lm(formula = mpg ~ wt, data = .)
## 
## Coefficients:
## (Intercept)           wt  
##      23.868       -2.192
```

### 21.9.3 Exercises

1. Implement your own version of every() using a for loop. Compare it with purrr::every(). What does purrr’s version do that your version doesn’t?

```r
x <- list(1:5, letters, list(10))

x %>% 
  every(is_character)
```

```
## [1] FALSE
```

```r
for (i in x){
  if(is_character(i)){
    print("T")
  } else {
    print("F")
  }
}
```

```
## [1] "F"
## [1] "T"
## [1] "F"
```

2. Create an enhanced col_sum() that applies a summary function to every numeric column in a data frame.

```r
col_sum <- function(df, f){
  keep(df, is.numeric) %>% summary()
}

col_sum(nycflights13::flights)
```

```
##       year          month             day           dep_time   
##  Min.   :2013   Min.   : 1.000   Min.   : 1.00   Min.   :   1  
##  1st Qu.:2013   1st Qu.: 4.000   1st Qu.: 8.00   1st Qu.: 907  
##  Median :2013   Median : 7.000   Median :16.00   Median :1401  
##  Mean   :2013   Mean   : 6.549   Mean   :15.71   Mean   :1349  
##  3rd Qu.:2013   3rd Qu.:10.000   3rd Qu.:23.00   3rd Qu.:1744  
##  Max.   :2013   Max.   :12.000   Max.   :31.00   Max.   :2400  
##                                                  NA's   :8255  
##  sched_dep_time   dep_delay          arr_time    sched_arr_time
##  Min.   : 106   Min.   : -43.00   Min.   :   1   Min.   :   1  
##  1st Qu.: 906   1st Qu.:  -5.00   1st Qu.:1104   1st Qu.:1124  
##  Median :1359   Median :  -2.00   Median :1535   Median :1556  
##  Mean   :1344   Mean   :  12.64   Mean   :1502   Mean   :1536  
##  3rd Qu.:1729   3rd Qu.:  11.00   3rd Qu.:1940   3rd Qu.:1945  
##  Max.   :2359   Max.   :1301.00   Max.   :2400   Max.   :2359  
##                 NA's   :8255      NA's   :8713                 
##    arr_delay            flight        air_time        distance   
##  Min.   : -86.000   Min.   :   1   Min.   : 20.0   Min.   :  17  
##  1st Qu.: -17.000   1st Qu.: 553   1st Qu.: 82.0   1st Qu.: 502  
##  Median :  -5.000   Median :1496   Median :129.0   Median : 872  
##  Mean   :   6.895   Mean   :1972   Mean   :150.7   Mean   :1040  
##  3rd Qu.:  14.000   3rd Qu.:3465   3rd Qu.:192.0   3rd Qu.:1389  
##  Max.   :1272.000   Max.   :8500   Max.   :695.0   Max.   :4983  
##  NA's   :9430                      NA's   :9430                  
##       hour           minute     
##  Min.   : 1.00   Min.   : 0.00  
##  1st Qu.: 9.00   1st Qu.: 8.00  
##  Median :13.00   Median :29.00  
##  Mean   :13.18   Mean   :26.23  
##  3rd Qu.:17.00   3rd Qu.:44.00  
##  Max.   :23.00   Max.   :59.00  
## 
```

3. A possible base R equivalent of col_sum() is:


```r
col_sum3 <- function(df, f) {
  is_num <- sapply(df, is.numeric)
  df_num <- df[, is_num]
  sapply(df_num, f) # apply f function to each numeric column 
} 

col_sum4 <- function(df, f) {
  df_num <- keep(df, is.numeric) 
  map_dbl(df_num, f)
} 
```

But it has a number of bugs as illustrated with the following inputs:


```r
df <- tibble(
  x = 1:3, 
  y = 3:1,
  z = c("a", "b", "c")
)
# OK
col_sum3(df, mean) 
```

```
## x y 
## 2 2
```

```r
# Has problems: don't always return numeric vector
col_sum3(df[1:2], mean) 
```

```
## x y 
## 2 2
```

```r
col_sum3(df[1], mean) 
```

```
## x 
## 2
```

```r
col_sum3(df[0], mean) 
```

```
## Error: Unsupported index type: list
```

```r
col_sum4(df, mean) %>% typeof()
```

```
## [1] "double"
```

```r
col_sum4(df[1:2], mean)
```

```
## x y 
## 2 2
```

```r
col_sum4(df[1], mean)
```

```
## x 
## 2
```

```r
col_sum4(df[0], mean)  
```

```
## named numeric(0)
```

What causes the bugs?
