# Assignment_05_10_2017
Ruijuan Li  
5/9/2017  

# import libs 

```r
library(nycflights13)
```

```
## Warning: package 'nycflights13' was built under R version 3.2.5
```

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
colnames(flights)
```

```
##  [1] "year"           "month"          "day"            "dep_time"      
##  [5] "sched_dep_time" "dep_delay"      "arr_time"       "sched_arr_time"
##  [9] "arr_delay"      "carrier"        "flight"         "tailnum"       
## [13] "origin"         "dest"           "air_time"       "distance"      
## [17] "hour"           "minute"         "time_hour"
```

# 5.2.4 Exercises
1) Find all flights that 

```r
# Had an arrival delay of two or more hours
arr_delay_over_2 <- filter(flights, arr_delay >= 120)
# Flew to Houston (IAH or HOU)
dest_houston <- filter(flights, dest == "IAH" | dest == "HOU")
# Were operated by United, American, or Delta
carrier_UA_AA_DL <- filter(flights, carrier == "UA" | carrier == "AA" | carrier == "DL")
# Departed in summer (July, August, and September)
month_789 <- filter(flights, month == 7 | month == 8 | month == 9)
# Arrived more than two hours late, but didn’t leave late
arr_delay_120_dep_delay_0 <- filter(flights, arr_delay > 120 & dep_delay <= 0)
# Were delayed by at least an hour, but made up over 30 minutes in flight
test <- filter(flights, dep_delay >= 60 & dep_delay-arr_delay > 30) 
# Departed between midnight and 6am (inclusive)
dep_time_midnight_6am <- filter(flights, dep_time >= 0 & dep_time <= 600)
```

2) Another useful dplyr filtering helper is between(). What does it do? Can you use it to simplify the code needed to answer the previous challenges?

```r
?between
dep_time_midnight_6am_2 <- filter(flights, between(dep_time, 0, 600)) 
identical(dep_time_midnight_6am, dep_time_midnight_6am_2)
```

```
## [1] TRUE
```

3) How many flights have a missing dep_time? What other variables are missing? What might these rows represent?

```r
sum(is.na(flights$dep_time))
```

```
## [1] 8255
```

```r
dep_time_missing <- flights[is.na(flights$dep_time),]
View(dep_time_missing) # dep_delay, arr_time, arr_delay, and air_time are all missing  
```

4) Why is NA ^ 0 not missing? Why is NA | TRUE not missing? Why is FALSE & NA not missing? Can you figure out the general rule? (NA * 0 is a tricky counterexample!) 

```r
NA ^ 0 # square 0 of any number is equal to 1 
```

```
## [1] 1
```

```r
NA | TRUE # | stands for OR, at least one TRUE leads to TRUE
```

```
## [1] TRUE
```

```r
FALSE & NA # & stands for AND, at least one FALSE leads to FALSE 
```

```
## [1] FALSE
```

```r
# the result of | and & must be "TRUE" or "FALSE"  
```

# 5.3.1 Exercises
1) How could you use arrange() to sort all missing values to the start? (Hint: use is.na()).

```r
arrange(flights, desc(is.na(dep_time)), dep_time) # don't understand... 
```

```
## # A tibble: 336,776 × 19
##     year month   day dep_time sched_dep_time dep_delay arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
## 1   2013     1     1       NA           1630        NA       NA
## 2   2013     1     1       NA           1935        NA       NA
## 3   2013     1     1       NA           1500        NA       NA
## 4   2013     1     1       NA            600        NA       NA
## 5   2013     1     2       NA           1540        NA       NA
## 6   2013     1     2       NA           1620        NA       NA
## 7   2013     1     2       NA           1355        NA       NA
## 8   2013     1     2       NA           1420        NA       NA
## 9   2013     1     2       NA           1321        NA       NA
## 10  2013     1     2       NA           1545        NA       NA
## # ... with 336,766 more rows, and 12 more variables: sched_arr_time <int>,
## #   arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
## #   minute <dbl>, time_hour <dttm>
```

2) Sort flights to find the most delayed flights. Find the flights that left earliest.

```r
head(arrange(flights, desc(dep_delay)), 1) 
```

```
## # A tibble: 1 × 19
##    year month   day dep_time sched_dep_time dep_delay arr_time
##   <int> <int> <int>    <int>          <int>     <dbl>    <int>
## 1  2013     1     9      641            900      1301     1242
## # ... with 12 more variables: sched_arr_time <int>, arr_delay <dbl>,
## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>,
## #   time_hour <dttm>
```

```r
head(arrange(flights, dep_time), 1)
```

```
## # A tibble: 1 × 19
##    year month   day dep_time sched_dep_time dep_delay arr_time
##   <int> <int> <int>    <int>          <int>     <dbl>    <int>
## 1  2013     1    13        1           2249        72      108
## # ... with 12 more variables: sched_arr_time <int>, arr_delay <dbl>,
## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>,
## #   time_hour <dttm>
```

3) Sort flights to find the fastest flights.

```r
head(arrange(flights, air_time), 1)
```

```
## # A tibble: 1 × 19
##    year month   day dep_time sched_dep_time dep_delay arr_time
##   <int> <int> <int>    <int>          <int>     <dbl>    <int>
## 1  2013     1    16     1355           1315        40     1442
## # ... with 12 more variables: sched_arr_time <int>, arr_delay <dbl>,
## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>,
## #   time_hour <dttm>
```

4) Which flights travelled the longest? Which travelled the shortest?

```r
head(arrange(flights, distance), 1)
```

```
## # A tibble: 1 × 19
##    year month   day dep_time sched_dep_time dep_delay arr_time
##   <int> <int> <int>    <int>          <int>     <dbl>    <int>
## 1  2013     7    27       NA            106        NA       NA
## # ... with 12 more variables: sched_arr_time <int>, arr_delay <dbl>,
## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>,
## #   time_hour <dttm>
```

```r
tail(arrange(flights, distance), 1)
```

```
## # A tibble: 1 × 19
##    year month   day dep_time sched_dep_time dep_delay arr_time
##   <int> <int> <int>    <int>          <int>     <dbl>    <int>
## 1  2013     9    30      959           1000        -1     1438
## # ... with 12 more variables: sched_arr_time <int>, arr_delay <dbl>,
## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>,
## #   time_hour <dttm>
```

# 5.4.1 Exercises
1) Brainstorm as many ways as possible to select dep_time, dep_delay, arr_time, and arr_delay from flights.

```r
colnames(flights)
```

```
##  [1] "year"           "month"          "day"            "dep_time"      
##  [5] "sched_dep_time" "dep_delay"      "arr_time"       "sched_arr_time"
##  [9] "arr_delay"      "carrier"        "flight"         "tailnum"       
## [13] "origin"         "dest"           "air_time"       "distance"      
## [17] "hour"           "minute"         "time_hour"
```

```r
tmp <- select(flights, dep_time, dep_delay, arr_time, arr_delay)
```

2) What happens if you include the name of a variable multiple times in a select() call?

```r
dim(select(flights, dep_time, dep_time)) # only take once 
```

```
## [1] 336776      1
```

3) What does the one_of() function do? Why might it be helpful in conjunction with this vector?

```r
vars <- c("year", "month", "day", "dep_delay", "arr_delay")
?one_of # variables in charactor vector 
tmp2 <- select(flights, one_of(vars)) # this way we take 
colnames(tmp2) # we can predefine the specific column that we want to select 
```

```
## [1] "year"      "month"     "day"       "dep_delay" "arr_delay"
```

4) Does the result of running the following code surprise you? How do the select helpers deal with case by default? How can you change that default?

```r
tmp3 <- select(flights, contains("TIME")) 
colnames(tmp3) 
```

```
## [1] "dep_time"       "sched_dep_time" "arr_time"       "sched_arr_time"
## [5] "air_time"       "time_hour"
```

```r
tmp4 <- select(flights, contains("time"))
identical(tmp3, tmp4) # case insensitive 
```

```
## [1] TRUE
```

```r
# make it case sensitive 
select(flights, contains("TIME", ignore.case = F)) 
```

```
## # A tibble: 336,776 × 0
```

#5.5.2 Exercises

1) Currently dep_time and sched_dep_time are convenient to look at, but hard to compute with because they’re not really continuous numbers. Convert them to a more convenient representation of number of minutes since midnight.

```r
colnames(flights)
```

```
##  [1] "year"           "month"          "day"            "dep_time"      
##  [5] "sched_dep_time" "dep_delay"      "arr_time"       "sched_arr_time"
##  [9] "arr_delay"      "carrier"        "flight"         "tailnum"       
## [13] "origin"         "dest"           "air_time"       "distance"      
## [17] "hour"           "minute"         "time_hour"
```

```r
head(flights$dep_time)
```

```
## [1] 517 533 542 544 554 554
```

```r
tmp5 <- mutate(flights, 
dep_time_2 = (dep_time %/% 100 * 60) +  (dep_time %% 100),
sched_dep_time_2 = (sched_dep_time %/% 100 * 60) +  (sched_dep_time %% 100)
)

head(tmp5[,c("dep_time", "dep_time_2", "sched_dep_time", "sched_dep_time_2")]) 
```

```
## # A tibble: 6 × 4
##   dep_time dep_time_2 sched_dep_time sched_dep_time_2
##      <int>      <dbl>          <int>            <dbl>
## 1      517        317            515              315
## 2      533        333            529              329
## 3      542        342            540              340
## 4      544        344            545              345
## 5      554        354            600              360
## 6      554        354            558              358
```

2) Compare air_time with arr_time - dep_time. What do you expect to see? What do you see? What do you need to do to fix it?

```r
tmp6<- mutate(flights,
          new = arr_time - dep_time)
tmp6[,c("arr_time", "new")] # not the same, they should be the same 
```

```
## # A tibble: 336,776 × 2
##    arr_time   new
##       <int> <int>
## 1       830   313
## 2       850   317
## 3       923   381
## 4      1004   460
## 5       812   258
## 6       740   186
## 7       913   358
## 8       709   152
## 9       838   281
## 10      753   195
## # ... with 336,766 more rows
```

```r
?flights
tmp7 <- mutate(flights, 
               arr_time_2 = (arr_time %/% 100 * 60) +  (arr_time %% 100),
               dep_time_2 = (dep_time %/% 100 * 60) +  (dep_time %% 100),
               air_time_2 = arr_time_2 - dep_time_2)
identical(tmp7$air_time_2, tmp7$air_time) 
```

```
## [1] FALSE
```

```r
colnames(flights) 
```

```
##  [1] "year"           "month"          "day"            "dep_time"      
##  [5] "sched_dep_time" "dep_delay"      "arr_time"       "sched_arr_time"
##  [9] "arr_delay"      "carrier"        "flight"         "tailnum"       
## [13] "origin"         "dest"           "air_time"       "distance"      
## [17] "hour"           "minute"         "time_hour"
```

```r
###### 
mutate(flights,
       air_time2 = arr_time - dep_time,
       air_time_diff = air_time2 - air_time) %>%
  filter(air_time_diff != 0) %>%
  select(air_time, air_time2, dep_time, arr_time, dest)
```

```
## # A tibble: 326,128 × 5
##    air_time air_time2 dep_time arr_time  dest
##       <dbl>     <int>    <int>    <int> <chr>
## 1       227       313      517      830   IAH
## 2       227       317      533      850   IAH
## 3       160       381      542      923   MIA
## 4       183       460      544     1004   BQN
## 5       116       258      554      812   ATL
## 6       150       186      554      740   ORD
## 7       158       358      555      913   FLL
## 8        53       152      557      709   IAD
## 9       140       281      557      838   MCO
## 10      138       195      558      753   ORD
## # ... with 326,118 more rows
```

3) Compare dep_time, sched_dep_time, and dep_delay. How would you expect those three numbers to be related?

```r
mutate(flights,
       dep_delay2 = dep_time - sched_dep_time) %>%
  filter(dep_delay2 != dep_delay) %>%
  select(dep_time, sched_dep_time, dep_delay, dep_delay2)
```

```
## # A tibble: 99,777 × 4
##    dep_time sched_dep_time dep_delay dep_delay2
##       <int>          <int>     <dbl>      <int>
## 1       554            600        -6        -46
## 2       555            600        -5        -45
## 3       557            600        -3        -43
## 4       557            600        -3        -43
## 5       558            600        -2        -42
## 6       558            600        -2        -42
## 7       558            600        -2        -42
## 8       558            600        -2        -42
## 9       558            600        -2        -42
## 10      559            600        -1        -41
## # ... with 99,767 more rows
```

4) Find the 10 most delayed flights using a ranking function. How do you want to handle ties? Carefully read the documentation for min_rank().

```r
mutate(flights,
       dep_delay_rank = min_rank(-dep_delay)) %>%
  arrange(dep_delay_rank) %>% 
  filter(dep_delay_rank <= 10) 
```

```
## # A tibble: 10 × 20
##     year month   day dep_time sched_dep_time dep_delay arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
## 1   2013     1     9      641            900      1301     1242
## 2   2013     6    15     1432           1935      1137     1607
## 3   2013     1    10     1121           1635      1126     1239
## 4   2013     9    20     1139           1845      1014     1457
## 5   2013     7    22      845           1600      1005     1044
## 6   2013     4    10     1100           1900       960     1342
## 7   2013     3    17     2321            810       911      135
## 8   2013     6    27      959           1900       899     1236
## 9   2013     7    22     2257            759       898      121
## 10  2013    12     5      756           1700       896     1058
## # ... with 13 more variables: sched_arr_time <int>, arr_delay <dbl>,
## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>,
## #   time_hour <dttm>, dep_delay_rank <int>
```

5) What does 1:3 + 1:10 return? Why?

```r
# 1:3 + 1:10
1:3
```

```
## [1] 1 2 3
```

```r
1:10
```

```
##  [1]  1  2  3  4  5  6  7  8  9 10
```

```r
11:20 + 1:10 # because they need to be vectorized 
```

```
##  [1] 12 14 16 18 20 22 24 26 28 30
```

6) What trigonometric functions does R provide?

```r
# All the classics: cos, sin, tan, acos, asin, atan, plus a few others that are drive by numerical or computational issues
```








