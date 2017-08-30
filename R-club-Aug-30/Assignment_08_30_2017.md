# Assignment_08_30_2017
Ruijuan Li  
8/30/2017  


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

### 20.4.6 Exercises

1. What does mean(is.na(x)) tell you about a vector x? What about sum(!is.finite(x))?

```r
set.seed(1)
x <- runif(10, 1, 100)
x <- c(x, NA, -Inf)
x
```

```
##  [1] 27.285358 37.840266 57.712483 90.912571 20.966511 89.940579 94.522852
##  [8] 66.418981 63.282290  7.116841        NA      -Inf
```

```r
mean(is.na(x)) # the proportion of missing data 
```

```
## [1] 0.08333333
```

```r
sum(!is.finite(x)) # the number of infinite in x  
```

```
## [1] 2
```

2. Carefully read the documentation of is.vector(). What does it actually test for? Why does is.atomic() not agree with the definition of atomic vectors above?

```r
# two types of vectors: atomic & list, atomic vectors are homogeneous, list vectors are hetergeneous. 

?is.vector
# is.vector returns TRUE if x is a vector of the specified mode having no attributes other than names. It returns FALSE otherwise.

df <- data.frame(x = 1:3, y = 5:7)
is.list(df)
```

```
## [1] TRUE
```

```r
! is.vector(df$x)
```

```
## [1] FALSE
```

```r
is.vector(df$x)
```

```
## [1] TRUE
```

```r
is.vector(list())
```

```
## [1] TRUE
```

```r
?is.atomic 
# is.atomic returns TRUE if x is of an atomic type (or NULL) and FALSE otherwise.
is.atomic(df)
```

```
## [1] FALSE
```

```r
is.atomic(df$x)
```

```
## [1] TRUE
```

```r
is.atomic(list())
```

```
## [1] FALSE
```

3. Compare and contrast setNames() with purrr::set_names().

```r
setNames( 1:3, c("foo", "bar", "baz") )
```

```
## foo bar baz 
##   1   2   3
```

```r
set_names(1:4, c("a", "b", "c", "d"))
```

```
## a b c d 
## 1 2 3 4
```

```r
# setNames(letters[1:5])
set_names(letters[1:5]) # allow missing name
```

```
##   a   b   c   d   e 
## "a" "b" "c" "d" "e"
```

```r
setNames(nm = c("First", "2nd")) # allow missing object
```

```
##   First     2nd 
## "First"   "2nd"
```

```r
set_names(nm = c("First", "2nd"))
```

```
## Error in typeof(x): argument "x" is missing, with no default
```

4. Create functions that take a vector as input and returns:

      1. The last value. Should you use [ or [[?

      2. The elements at even numbered positions.

      3. Every element except the last value.

      4. Only even numbers (and no missing values).
      

```r
set.seed(1)
x <- sample(20, 100, replace = TRUE)
x <- c(x, NA)
x
```

```
##   [1]  6  8 12 19  5 18 19 14 13  2  5  4 14  8 16 10 15 20  8 16 19  5 14
##  [24]  3  6  8  1  8 18  7 10 12 10  4 17 14 16  3 15  9 17 13 16 12 11 16
##  [47]  1 10 15 14 10 18  9  5  2  2  7 11 14  9 19  6 10  7 14  6 10 16  2
##  [70] 18  7 17  7  7 10 18 18  8 16 20  9 15  8  7 16  5 15  3  5  3  5  2
##  [93] 13 18 16 16 10  9 17 13 NA
```

```r
# 1
last <- function(x){x[length(x)]}
last(x)
```

```
## [1] NA
```

```r
# 2 
even_pos <- function(x){
  pos <- sapply(1: length(x), function(i) i %% 2 ==0)
  x[pos]
}
even_pos(x) 
```

```
##  [1]  8 19 18 14  2  4  8 10 20 16  5  3  8  8  7 12  4 14  3  9 13 12 16
## [24] 10 14 18  5  2 11  9  6  7  6 16 18 17  7 18  8 20 15  7  5  3  3  2
## [47] 18 16  9 13
```

```r
even_pos_1 <- function(x){
  x[c(FALSE,TRUE)]
}
even_pos_1(x)
```

```
##  [1]  8 19 18 14  2  4  8 10 20 16  5  3  8  8  7 12  4 14  3  9 13 12 16
## [24] 10 14 18  5  2 11  9  6  7  6 16 18 17  7 18  8 20 15  7  5  3  3  2
## [47] 18 16  9 13
```

```r
# 3
drop_last <- function(x){x[1:length(x)-1]}
drop_last(x)
```

```
##   [1]  6  8 12 19  5 18 19 14 13  2  5  4 14  8 16 10 15 20  8 16 19  5 14
##  [24]  3  6  8  1  8 18  7 10 12 10  4 17 14 16  3 15  9 17 13 16 12 11 16
##  [47]  1 10 15 14 10 18  9  5  2  2  7 11 14  9 19  6 10  7 14  6 10 16  2
##  [70] 18  7 17  7  7 10 18 18  8 16 20  9 15  8  7 16  5 15  3  5  3  5  2
##  [93] 13 18 16 16 10  9 17 13
```

```r
# 4
even <- function(x){
  x1 <- x[!is.na(x)]
  x1[x1 %% 2 == 0]}
even(x)
```

```
##  [1]  6  8 12 18 14  2  4 14  8 16 10 20  8 16 14  6  8  8 18 10 12 10  4
## [24] 14 16 16 12 16 10 14 10 18  2  2 14  6 10 14  6 10 16  2 18 10 18 18
## [47]  8 16 20  8 16  2 18 16 16 10
```

5. Why is x[-which(x > 0)] not the same as x[x <= 0]?

```r
x <- c(x, -4, -Inf)
x
```

```
##   [1]    6    8   12   19    5   18   19   14   13    2    5    4   14    8
##  [15]   16   10   15   20    8   16   19    5   14    3    6    8    1    8
##  [29]   18    7   10   12   10    4   17   14   16    3   15    9   17   13
##  [43]   16   12   11   16    1   10   15   14   10   18    9    5    2    2
##  [57]    7   11   14    9   19    6   10    7   14    6   10   16    2   18
##  [71]    7   17    7    7   10   18   18    8   16   20    9   15    8    7
##  [85]   16    5   15    3    5    3    5    2   13   18   16   16   10    9
##  [99]   17   13   NA   -4 -Inf
```

```r
x[-which(x > 0)] 
```

```
## [1]   NA   -4 -Inf
```

```r
x[x <= 0] 
```

```
## [1]   NA   -4 -Inf
```

```r
# why? 
```

6. What happens when you subset with a positive integer that’s bigger than the length of the vector? What happens when you subset with a name that doesn’t exist?

```r
length(x)
```

```
## [1] 103
```

```r
x[length(x) + 1]
```

```
## [1] NA
```

```r
x <- setNames(x, nm = c(1:length(x)))
x["104"] 
```

```
## <NA> 
##   NA
```

### 20.5.4 Exercises

1 Draw the following lists as nested sets:

      1. list(a, b, list(c, d), list(e, f))
      2. list(list(list(list(list(list(a))))))
      
2. What happens if you subset a tibble as if you’re subsetting a list? What are the key differences between a list and a tibble?

```r
iris_tibble <- as_tibble(iris)
identical(iris_tibble[[1]], iris[[1]]) # return the same thing. 
```

```
## [1] TRUE
```

```r
# data structures of tibble and list are different. tibble is more like data frame whereas list is not.  
```

### 20.7.4 Exercises

1. What does hms::hms(3600) return? How does it print? What primitive type is the augmented vector built on top of? What attributes does it use?

```r
x <- hms::hms(3600)
x
```

```
## 01:00:00
```

```r
attributes(x) 
```

```
## $units
## [1] "secs"
## 
## $class
## [1] "hms"      "difftime"
```

```r
typeof(x) # double 
```

```
## [1] "double"
```

2. Try and make a tibble that has columns with different lengths. What happens?

```r
tb <- tibble::tibble(x = 1:5, y = 5:0)
```

```
## Error: Variables must be length 1 or 6.
## Problem variables: 'x'
```

3. Based on the definition above, is it ok to have a list as a column of a tibble?

```r
tb <- tibble::tibble(x = 1:5, y = 5:1, c = list(1:5))
# yes, as long as it is the same length as other columns
```



