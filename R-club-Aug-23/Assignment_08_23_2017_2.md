# Assignment_08_23_2017_2
Ruijuan Li  
8/23/2017  

```r
library(readr)
```

```
## Warning: package 'readr' was built under R version 3.2.5
```

### 20.3.5 Exercises

1. Describe the difference between is.finite(x) and !is.infinite(x).

```r
class(is.finite(1))
```

```
## [1] "logical"
```

```r
class(!is.infinite(1))
```

```
## [1] "logical"
```

2. Read the source code for dplyr::near() (Hint: to see the source code, drop the ()). How does it work?

```r
# near(1,1)
# .Machine$double.eps^0.5 # compare the abs of (a-b) with this value 
```

3. A logical vector can take 3 possible values. How many possible values can an integer vector take? How many possible values can a double take? Use google to do some research.


4. Brainstorm at least four functions that allow you to convert a double to an integer. How do they differ? Be precise.

```r
doub_to_int1 <- function(x){
  if(typeof(x) != "double"){
    warning("input is not double, stop")
  } else {
    as.integer(x)
  }
}

doub_to_int2 <- function(x){
  if(typeof(x) != "double"){
    warning("input is not double, stop")
  } else {
    parse_integer(x)
  }
}

typeof(1)
```

```
## [1] "double"
```

```r
doub_to_int1(1)
```

```
## [1] 1
```

```r
doub_to_int2(1)
```

```
## [1] 1
```

```r
doub_to_int1(as.integer(1)) 
```

```
## Warning in doub_to_int1(as.integer(1)): input is not double, stop
```

```r
# other method? 
```

5. What functions from the readr package allow you to turn a string into logical, integer, and double vector?

```r
parse_logical(c("TRUE", "FALSE", "1", "0", "true", "t", "NA"))
```

```
## [1]  TRUE FALSE  TRUE FALSE  TRUE  TRUE    NA
```

```r
parse_integer(c("1235", "0134", "NA"))
```

```
## [1] 1235  134   NA
```

```r
parse_number(c("1.0", "3.5", "1,000", "NA"))
```

```
## [1]    1.0    3.5 1000.0     NA
```
copy and paste from: https://jrnold.github.io/e4qf/vectors.html#exercises-44 

