# Assignment_09_06_2017
Ruijuan Li  
9/6/2017  

### 21.2.1 Exercises

1. Write for loops to:

      1. Compute the mean of every column in mtcars.
      2. Determine the type of each column in nycflights13::flights.
      3. Compute the number of unique values in each column of iris.
      4. Generate 10 random normals for each of μ=−10, 0, 10, and 100.
      
Think about the output, sequence, and body before you start writing the loop.

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
# 1) 
mean.mtcars <- vector()
for (i in colnames(mtcars)) {
  mean.mtcars[[i]] <- mean(mtcars[,i])  
}
mean.mtcars
```

```
##        mpg        cyl       disp         hp       drat         wt 
##  20.090625   6.187500 230.721875 146.687500   3.596563   3.217250 
##       qsec         vs         am       gear       carb 
##  17.848750   0.437500   0.406250   3.687500   2.812500
```

```r
# 2) 
type_flights <- vector()
for (i in colnames(nycflights13::flights)){
  type_flights[[i]] <- typeof(nycflights13::flights[[i]])
}
type_flights
```

```
##           year          month            day       dep_time sched_dep_time 
##      "integer"      "integer"      "integer"      "integer"      "integer" 
##      dep_delay       arr_time sched_arr_time      arr_delay        carrier 
##       "double"      "integer"      "integer"       "double"    "character" 
##         flight        tailnum         origin           dest       air_time 
##      "integer"    "character"    "character"    "character"       "double" 
##       distance           hour         minute      time_hour 
##       "double"       "double"       "double"       "double"
```

```r
# 3) 
uniq_num_iris <- vector()
for (i in colnames(iris)){
  uniq_num_iris[[i]] <- length(unique(iris[,i]))
}
uniq_num_iris
```

```
## Sepal.Length  Sepal.Width Petal.Length  Petal.Width      Species 
##           35           23           43           22            3
```

```r
# 4) 
ran_norm <- list()
mean <- c(-10, 0, 10, 100)
for (i in seq_along(mean)){
  ran_norm[[i]] <- rnorm(n = 10, mean = mean[[i]])
}
ran_norm
```

```
## [[1]]
##  [1]  -9.545245  -8.436723  -8.459541 -10.355783  -9.255910 -11.842583
##  [7]  -9.684475  -8.832702  -9.616203 -11.236991
## 
## [[2]]
##  [1] -0.5321379  0.2957798 -0.7474174  1.0893718  0.4669644 -0.2284675
##  [7]  1.1084708  1.2341820 -1.1896395  1.8851507
## 
## [[3]]
##  [1] 10.329253 10.281960 10.243860  9.000604  9.720684 10.182890 10.397745
##  [8]  7.835923  8.972059 10.876702
## 
## [[4]]
##  [1] 100.91357  99.23229  99.35228 100.00930  99.50363 101.03492  99.42985
##  [8] 101.43541  98.29479 102.09447
```

2. Eliminate the for loop in each of the following examples by taking advantage of an existing function that works with vectors:


```r
# out <- ""
# for (x in letters) {
#   out <- stringr::str_c(out, x)
# }

# str_c(letters, collapse = "")

set.seed(1)
x <- sample(100)
sd <- 0
for (i in seq_along(x)) {
  sd <- sd + (x[i] - mean(x)) ^ 2
}
sd <- sqrt(sd / (length(x) - 1))

sd(x)
```

```
## [1] 29.01149
```

```r
set.seed(1)
x <- runif(100)
out <- vector("numeric", length(x))
out[1] <- x[1]
for (i in 2:length(x)) {
  out[i] <- out[i - 1] + x[i]
}
out
```

```
##   [1]  0.2655087  0.6376326  1.2104859  2.1186937  2.3203756  3.2187653
##   [7]  4.1634406  4.8242384  5.4533524  5.5151387  5.7211133  5.8976700
##  [13]  6.5846929  6.9687966  7.7386380  8.2363373  8.9539558  9.9458619
##  [19] 10.3258970 11.1033423 12.0380475 12.2501900 12.9018638 13.0274189
##  [25] 13.2946395 13.6807536 13.6941440 14.0765319 14.9462228 15.2865718
##  [31] 15.7686519 16.3682177 16.8617590 17.0479766 17.8753499 18.5438167
##  [37] 19.3380565 19.4460002 20.1697111 20.5809855 21.4019318 22.0489920
##  [43] 22.8319248 23.3849611 23.9146807 24.7040369 24.7273681 25.2045982
##  [49] 25.9369119 26.6296435 27.1072631 27.9684726 28.4065697 28.6513670
##  [55] 28.7220460 28.8215122 29.1377839 29.6564181 30.3184232 30.7252534
##  [61] 31.6381293 31.9317327 32.3907984 32.7231931 33.3740636 33.6320803
##  [67] 34.1106256 34.8769363 34.9611832 35.8365045 36.1755774 37.0150178
##  [73] 37.3617013 37.6954762 38.1718275 39.0640258 39.9283653 40.3183548
##  [79] 41.0956755 42.0562935 42.4909530 43.2034677 43.6034620 43.9288142
##  [85] 44.6859013 44.8885936 45.5997148 45.7214067 45.9668953 46.1101996
##  [91] 46.3498291 46.4087634 47.0510517 47.9273209 48.7062356 49.5035444
##  [97] 49.9588189 50.3689029 51.1797732 51.7847065
```

```r
cumsum(x)
```

```
##   [1]  0.2655087  0.6376326  1.2104859  2.1186937  2.3203756  3.2187653
##   [7]  4.1634406  4.8242384  5.4533524  5.5151387  5.7211133  5.8976700
##  [13]  6.5846929  6.9687966  7.7386380  8.2363373  8.9539558  9.9458619
##  [19] 10.3258970 11.1033423 12.0380475 12.2501900 12.9018638 13.0274189
##  [25] 13.2946395 13.6807536 13.6941440 14.0765319 14.9462228 15.2865718
##  [31] 15.7686519 16.3682177 16.8617590 17.0479766 17.8753499 18.5438167
##  [37] 19.3380565 19.4460002 20.1697111 20.5809855 21.4019318 22.0489920
##  [43] 22.8319248 23.3849611 23.9146807 24.7040369 24.7273681 25.2045982
##  [49] 25.9369119 26.6296435 27.1072631 27.9684726 28.4065697 28.6513670
##  [55] 28.7220460 28.8215122 29.1377839 29.6564181 30.3184232 30.7252534
##  [61] 31.6381293 31.9317327 32.3907984 32.7231931 33.3740636 33.6320803
##  [67] 34.1106256 34.8769363 34.9611832 35.8365045 36.1755774 37.0150178
##  [73] 37.3617013 37.6954762 38.1718275 39.0640258 39.9283653 40.3183548
##  [79] 41.0956755 42.0562935 42.4909530 43.2034677 43.6034620 43.9288142
##  [85] 44.6859013 44.8885936 45.5997148 45.7214067 45.9668953 46.1101996
##  [91] 46.3498291 46.4087634 47.0510517 47.9273209 48.7062356 49.5035444
##  [97] 49.9588189 50.3689029 51.1797732 51.7847065
```

3. Combine your function writing and for loop skills:

      1. Write a for loop that prints() the lyrics to the children’s song “Alice the camel”.

      2. Convert the nursery rhyme “ten in the bed” to a function. Generalise it to any number of people in any sleeping structure.

      3. Convert the song “99 bottles of beer on the wall” to a function. Generalise to any number of any vessel containing any liquid on any surface.

```r
lyrics <- read.delim("~/Desktop/2017_summer/Rclub-r4ds_Ruijuan.Li/R-club-Sep-06/lyrics", header = F, stringsAsFactors = F)

for (i in rownames(lyrics)){
  print(lyrics[i,])
} 
```

```
## [1] "Alice the camel has five humps."
## [1] "Alice the camel has five humps."
## [1] "Alice the camel has five humps."
## [1] "So go, Alice, go."
## [1] "Alice the camel has four humps."
## [1] "Alice the camel has four humps."
## [1] "Alice the camel has four humps."
## [1] "So go, Alice, go."
## [1] "Alice the camel has three humps."
## [1] "Alice the camel has three humps."
## [1] "Alice the camel has three humps."
## [1] "So go, Alice, go."
## [1] "Alice the camel has two humps."
## [1] "Alice the camel has two humps."
## [1] "Alice the camel has two humps."
## [1] "So go, Alice, go."
## [1] "Alice the camel has one hump."
## [1] "Alice the camel has one hump."
## [1] "Alice the camel has one hump."
## [1] "So go, Alice, go."
## [1] "Alice the camel has no humps."
## [1] "Alice the camel has no humps."
## [1] "Alice the camel has no humps."
## [1] "Now Alice is a horse"
```

```r
# skip... 
```

4. It’s common to see for loops that don’t preallocate the output and instead increase the length of a vector at each step:


```r
output <- vector("integer", 0)
system.time(
for (i in seq_along(x)) {
  output <- c(output, lengths(x[[i]]))
})
```

```
##    user  system elapsed 
##       0       0       0
```

```r
output <- vector()
system.time(
for (i in seq_along(x)) {
  output <- c(output, lengths(x[[i]]))
})
```

```
##    user  system elapsed 
##       0       0       0
```

```r
# how does this affect permformance? 
# system time? no. memory usage? ... skip 
```
How does this affect performance? Design and execute an experiment. 

### 21.3.5 Exercises

1. Imagine you have a directory full of CSV files that you want to read in. You have their paths in a vector, files <- dir("data/", pattern = "\\.csv$", full.names = TRUE), and now want to read each one with read_csv(). Write the for loop that will load them into a single data frame.

```r
# output <- data_frame() 
# files <- dir("data/", pattern = "\\.csv$", full.names = TRUE) 
# for (i in files){
#   output[[i]] <- read_csv(i) # something like this... 
# }
# output 

# a single data frame ? how??? 
```

2. What happens if you use for (nm in names(x)) and x has no names? What if only some of the elements are named? What if the names are not unique?

```r
# no name 
names(letters)
```

```
## NULL
```

```r
for (i in names(letters)){
  print(letters[[i]])
}

names(letters)[1:3] <- c("A", "B", "C")

for (i in names(letters)){
  print(letters[[i]])
}
```

```
## [1] "a"
## [1] "b"
## [1] "c"
```

```
## Error in letters[[i]]: subscript out of bounds
```

```r
names(letters) <- c(LETTERS[1:24], "A", "B")

for (i in names(letters)){
  print(letters[[i]])
}
```

```
## [1] "a"
## [1] "b"
## [1] "c"
## [1] "d"
## [1] "e"
## [1] "f"
## [1] "g"
## [1] "h"
## [1] "i"
## [1] "j"
## [1] "k"
## [1] "l"
## [1] "m"
## [1] "n"
## [1] "o"
## [1] "p"
## [1] "q"
## [1] "r"
## [1] "s"
## [1] "t"
## [1] "u"
## [1] "v"
## [1] "w"
## [1] "x"
## [1] "a"
## [1] "b"
```

3. Write a function that prints the mean of each numeric column in a data frame, along with its name. For example, show_mean(iris) would print:


```r
# show_mean(iris)
#> Sepal.Length: 5.84
#> Sepal.Width:  3.06
#> Petal.Length: 3.76
#> Petal.Width:  1.20
```
(Extra challenge: what function did I use to make sure that the numbers lined up nicely, even though the variable names had different lengths?)

4. What does this code do? How does it work?


```r
trans <- list( 
  disp = function(x) x * 0.0163871,
  am = function(x) {
    factor(x, labels = c("auto", "manual"))
  }
)
for (var in names(trans)) {
  mtcars[[var]] <- trans[[var]](mtcars[[var]])
}
```










