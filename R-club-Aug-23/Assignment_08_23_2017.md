# Assignment_08_23_2017
Ruijuan Li  
8/23/2017  

### 19.5.5 Exercises

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

1. What does commas(letters, collapse = "-") do? Why?

```r
commas <- function(...) stringr::str_c(..., collapse = ", ")
commas(letters, collapse="-") 
```

```
## Error in stringr::str_c(..., collapse = ", "): formal argument "collapse" matched by multiple actual arguments
```

```r
# because collapse is not an argument in commas function
```

2. It’d be nice if you could supply multiple characters to the pad argument, e.g. rule("Title", pad = "-+"). Why doesn’t this currently work? How could you fix it?

```r
rule <- function(..., pad = "-") {
  title <- paste0(...) 
  # paste0(..., collapse) is equivalent to paste(..., sep = "", collapse), slightly more efficiently 
  width <- getOption("width") - nchar(title) - 5 
  # The width option get the number of R put on a line.  
  cat(title, " ", stringr::str_dup(pad, width), "\n", sep = "")
}

rule("Title", pad = "-")
```

```
## Title -----------------------------------------------------------------
```

```r
rule("Title", pad = "-+")
```

```
## Title -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

```r
# multiple characters works but I guess the question is when supplying multiple characters, how to still keep the width the same as when using a single character 

length(unlist(stringr::str_split("+-", "")))
```

```
## [1] 2
```

```r
rule2 <- function(..., pad = "-") {
  title <- paste0(...) 
  # paste0(..., collapse) is equivalent to paste(..., sep = "", collapse), slightly more efficiently 
  width <- getOption("width") - nchar(title) - 5 
  # The width option get the number of R put on a line.  
  pad_len <- length(unlist(stringr::str_split(pad, "")))
  if(pad_len == 1){ 
  cat(title, " ", stringr::str_dup(pad, width), "\n", sep = "")
    } else {
  cat(title, " ", stringr::str_dup(pad, width/pad_len), "\n", sep = "") 
  }
}

rule2("Title", pad = "-")
```

```
## Title -----------------------------------------------------------------
```

```r
rule2("Title", pad = "-+")
```

```
## Title -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

3. What does the trim argument to mean() do? When might you use it?

```r
?mean
x <- c(0:10, 50)
xm <- mean(x)
c(xm, mean(x, trim = 0.10))
```

```
## [1] 8.75 5.50
```

```r
x
```

```
##  [1]  0  1  2  3  4  5  6  7  8  9 10 50
```

```r
mean(x, trim = 0.10) 
```

```
## [1] 5.5
```

```r
mean(x)
```

```
## [1] 8.75
```

```r
# The trim arguments trims a fraction of observations from each end of the vector (meaning the range) before calculating the mean. This is useful for calculating a measure of central tendancy that is robust to outliers.
```

4. The default value for the method argument to cor() is c("pearson", "kendall", "spearman"). What does that mean? What value is used by default?

```r
?cor
cor(diamonds$carat, diamonds$price, method = "pearson")
```

```
## [1] 0.9215913
```

```r
cor(diamonds$carat, diamonds$price, method = "spearman")
```

```
## [1] 0.9628828
```

```r
cor(diamonds$carat, diamonds$price, method = "kendall") 
```

```
## [1] 0.8341049
```

* A correlation coefficient measures the extent to which two variables tend to change together. The coefficient describes both the strength and the direction of the relationship. 

* The Pearson correlation evaluates the linear relationship between two continuous variables. A relationship is linear when a change in one variable is associated with a proportional change in the other variable.
![Pearson](https://github.com/UCD-pbio-rclub/Rclub-r4ds_Ruijuan.Li/blob/master/R-club-Aug-23/pearson.png)

* The Spearman correlation evaluates the monotonic (linear or not) relationship between two continuous or ordinal variables. In a monotonic relationship, the variables tend to change together, but not necessarily at a constant rate. The Spearman correlation coefficient is based on the ranked values for each variable rather than the raw data. 
![Spearman](https://github.com/UCD-pbio-rclub/Rclub-r4ds_Ruijuan.Li/blob/master/R-club-Aug-23/spearman.png)
![Spearman2](https://github.com/UCD-pbio-rclub/Rclub-r4ds_Ruijuan.Li/blob/master/R-club-Aug-23/spearman2.png)

* kendall correlation: also based on ranked values, it is the difference between the probability that the two variables are in the same order in the observed data versus the probability that the two variables are in different orders. 
![Kendall](https://github.com/UCD-pbio-rclub/Rclub-r4ds_Ruijuan.Li/blob/master/R-club-Aug-23/kendall.png)

