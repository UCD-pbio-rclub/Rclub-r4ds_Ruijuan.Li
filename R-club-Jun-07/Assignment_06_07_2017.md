# Assignment_06_07_2017
Ruijuan Li  
6/3/2017  

# 11.2.2 Exercises


```r
library(tidyverse)
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
## Conflicts with tidy packages ----------------------------------------------
```

```
## filter(): dplyr, stats
## lag():    dplyr, stats
```

1. What function would you use to read a file where fields were separated with
“|”?

      read_delim(file, delim = "|")


2. Apart from file, skip, and comment, what other arguments do read_csv() and read_tsv() have in common?

      read_csv(file, col_names = TRUE, col_types = NULL,
  locale = default_locale(), na = c("", "NA"), quoted_na = TRUE,
  quote = "\"", comment = "", trim_ws = TRUE, skip = 0, n_max = Inf,
  guess_max = min(1000, n_max), progress = show_progress())

      read_tsv(file, col_names = TRUE, col_types = NULL,
  locale = default_locale(), na = c("", "NA"), quoted_na = TRUE,
  quote = "\"", comment = "", trim_ws = TRUE, skip = 0, n_max = Inf,
  guess_max = min(1000, n_max), progress = show_progress())
  
      delim; col_names; na; trim_ws, etc. 

3. What are the most important arguments to read_fwf()?

      read_fwf(file, col_positions, col_types = NULL, locale = default_locale(),
  na = c("", "NA"), comment = "", skip = 0, n_max = Inf,
  guess_max = min(n_max, 1000), progress = show_progress())

      col_positions; widths; start, end...
      

```r
fwf_sample <- readr_example("fwf-sample.txt")
cat(read_lines(fwf_sample))
```

```
## John Smith          WA        418-Y11-4111 Mary Hartford       CA        319-Z19-4341 Evan Nolan          IL        219-532-c301
```

```r
# You can specify column positions in several ways:
# 1. Guess based on position of empty columns
read_fwf(fwf_sample, fwf_empty(fwf_sample, col_names = c("first", "last", "state", "ssn")))
```

```
## Parsed with column specification:
## cols(
##   first = col_character(),
##   last = col_character(),
##   state = col_character(),
##   ssn = col_character()
## )
```

```
## # A tibble: 3 × 4
##   first     last state          ssn
##   <chr>    <chr> <chr>        <chr>
## 1  John    Smith    WA 418-Y11-4111
## 2  Mary Hartford    CA 319-Z19-4341
## 3  Evan    Nolan    IL 219-532-c301
```

```r
# 2. A vector of field widths
read_fwf(fwf_sample, fwf_widths(c(20, 10, 12), c("name", "state", "ssn")))
```

```
## Parsed with column specification:
## cols(
##   name = col_character(),
##   state = col_character(),
##   ssn = col_character()
## )
```

```
## # A tibble: 3 × 3
##            name state          ssn
##           <chr> <chr>        <chr>
## 1    John Smith    WA 418-Y11-4111
## 2 Mary Hartford    CA 319-Z19-4341
## 3    Evan Nolan    IL 219-532-c301
```

```r
# 3. Paired vectors of start and end positions
read_fwf(fwf_sample, fwf_positions(c(1, 30), c(10, 42), c("name", "ssn")))
```

```
## Parsed with column specification:
## cols(
##   name = col_character(),
##   ssn = col_character()
## )
```

```
## # A tibble: 3 × 2
##         name          ssn
##        <chr>        <chr>
## 1 John Smith 418-Y11-4111
## 2 Mary Hartf 319-Z19-4341
## 3 Evan Nolan 219-532-c301
```

```r
# 4. Named arguments with start and end positions
read_fwf(fwf_sample, fwf_cols(name = c(1, 10), ssn = c(30, 42)))
```

```
## Parsed with column specification:
## cols(
##   name = col_character(),
##   ssn = col_character()
## )
```

```
## # A tibble: 3 × 2
##         name          ssn
##        <chr>        <chr>
## 1 John Smith 418-Y11-4111
## 2 Mary Hartf 319-Z19-4341
## 3 Evan Nolan 219-532-c301
```

```r
# 5. Named arguments with column widths
read_fwf(fwf_sample, fwf_cols(name = 20, state = 10, ssn = 12))
```

```
## Parsed with column specification:
## cols(
##   name = col_character(),
##   state = col_character(),
##   ssn = col_character()
## )
```

```
## # A tibble: 3 × 3
##            name state          ssn
##           <chr> <chr>        <chr>
## 1    John Smith    WA 418-Y11-4111
## 2 Mary Hartford    CA 319-Z19-4341
## 3    Evan Nolan    IL 219-532-c301
```

```r
# don't know how this can be useful for my analysis for this moment 
# can be useful for barcoding??? RNA-seq? fixed width... 
```

4. Sometimes strings in a CSV file contain commas. To prevent them from causing problems they need to be surrounded by a quoting character, like " or '. By convention, read_csv() assumes that the quoting character will be ", and if you want to change it you’ll need to use read_delim() instead. What arguments do you need to specify to read the following text into a data frame?


```r
"x,y\n1,'a,b'"

x <- "x,y\n1,'a,b'"
read_delim(x, ",", quote = "'")
read_csv(x, quote = "'") # this also works 
```

5. Identify what is wrong with each of the following inline CSV files. What happens when you run the code?


```r
read_csv("a,b\n1,2,3\n4,5,6") # 3 and 6 could not be read bc. only two colomns
read_csv("a,b,c\n1,2,3\n4,5,6") 

read_csv("a,b,c\n1,2\n1,2,3,4") # same, incosistent row length
read_csv("a,b\n\"1") # same 
read_csv("a,b\n1,2\na,b") # ???
read_csv("a;b\n1;3")
read_delim("a;b\n1;3", delim=";") 
```

# 11.3.5 Exercises

1. What are the most important arguments to locale()?

```r
?locale
```

2. What happens if you try and set decimal_mark and grouping_mark to the same character? What happens to the default value of grouping_mark when you set decimal_mark to “,”? What happens to the default value of decimal_mark when you set the grouping_mark to “.”?

      parse_double("1,23", locale = locale(decimal_mark = ",", grouping_mark = ","))
      
      Error: `decimal_mark` and `grouping_mark` must be different

      If the decimal_mark is set to the comma “,", then the grouping mark is set to the period ".":
      If the grouping mark is set to a period, then the decimal mark is set to a comma 

3. I didn’t discuss the date_format and time_format options to locale(). What do they do? Construct an example that shows when they might be useful.

```r
# copied 
parse_date("1 janvier 2015", "%d %B %Y", locale = locale("fr"))
```

```
## [1] "2015-01-01"
```

```r
#> [1] "2015-01-01"
parse_date("14 oct. 1979", "%d %b %Y", locale = locale("fr"))
```

```
## [1] "1979-10-14"
```

```r
#> [1] "1979-10-14"
# Apparently the time format is not used for anything, date format is used for guessing column types. 
```

4. If you live outside the US, create a new locale object that encapsulates the settings for the types of file you read most commonly.

```r
date_names_lang("zh") 
```

```
## <date_names>
## Days:   星期日 (周日), 星期一 (周一), 星期二 (周二), 星期三 (周三), 星期四
##         (周四), 星期五 (周五), 星期六 (周六)
## Months: 一月 (1月), 二月 (2月), 三月 (3月), 四月 (4月), 五月 (5月), 六月
##         (6月), 七月 (7月), 八月 (8月), 九月 (9月), 十月 (10月),
##         十一月 (11月), 十二月 (12月)
## AM/PM:  上午/下午
```

5. What’s the difference between read_csv() and read_csv2()?
      
      The delimiter. The function read_csv uses a comma, while read_csv2 uses a semi-colon (;). Using a semi-colon is useful when commas are used as the decimal point (as in Europe).

6. What are the most common encodings used in Europe? What are the most common encodings used in Asia? Do some googling to find out.
      
      [https://jrnold.github.io/e4qf/data-import.html]

7. Generate the correct format string to parse each of the following dates and times:


```r
?parse_date
d1 <- "January 1, 2010"
d2 <- "2015-Mar-07"
d3 <- "06-Jun-2017"
d4 <- c("August 19 (2015)", "July 1 (2015)")
d5 <- "12/30/14" # Dec 30, 2014
t1 <- "1705"
t2 <- "11:15:10.12 PM"
```


```r
parse_date(d1, format = "%B %d, %Y")
```

```
## [1] "2010-01-01"
```

```r
parse_date(d2, format = "%Y-%b-%d")
```

```
## [1] "2015-03-07"
```

```r
parse_date(d3, format = "%d-%b-%Y")
```

```
## [1] "2017-06-06"
```

```r
parse_date(d4, format = "%B %d (%Y)")
```

```
## [1] "2015-08-19" "2015-07-01"
```

```r
parse_date(d5, format = "%m/%d/%y")
```

```
## [1] "2014-12-30"
```

```r
parse_time(t1, format = "%H%M") 
```

```
## 17:05:00
```

```r
parse_time(t2, format = "%I:%M:%OS %p") 
```

```
## 23:15:10.12
```






