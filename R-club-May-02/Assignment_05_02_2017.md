# Assignment_05_02_2017
Ruijuan Li  
5/2/2017  

## 3.6.1 Exercises
# 1) 
What geom would you use to draw a line chart? A boxplot? A histogram? An area chart?

```r
# geom_line
# geom_boxplot
# geom_histogram
# geom_area
```

# 2) 
Run this code in your head and predict what the output will look like. Then, run the code in R and check your predictions

```r
library("ggplot2")
```

```
## Warning: package 'ggplot2' was built under R version 3.2.5
```

```r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy, color = drv)) + 
  geom_point() + 
  geom_smooth(se = FALSE) # no confidence interval 
```

```
## `geom_smooth()` using method = 'loess'
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-2-1.png)<!-- -->

```r
?geom_smooth
```

# 3) 
What does show.legend = FALSE do? What happens if you remove it?
Why do you think I used it earlier in the chapter?

```r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy, color = drv)) + 
  geom_point(show.legend = F) + 
  geom_smooth(se = FALSE, show.legend = F)
```

```
## `geom_smooth()` using method = 'loess'
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-3-1.png)<!-- -->

# 4)
What does the se argument to geom_smooth() do?

```r
# add confidence interval or not 
```

# 5) 
Will these two graphs look different? Why/why not?

```r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_point() + 
  geom_smooth()
```

```
## `geom_smooth()` using method = 'loess'
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-5-1.png)<!-- -->

```r
ggplot() + 
  geom_point(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_smooth(data = mpg, mapping = aes(x = displ, y = hwy))
```

```
## `geom_smooth()` using method = 'loess'
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-5-2.png)<!-- -->

```r
# exactly the same 
```

# 6) 
Recreate the R code necessary to generate the following graphs.

```r
# a) 
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_point(show.legend = F) + 
  geom_smooth(se = FALSE, show.legend = F)
```

```
## `geom_smooth()` using method = 'loess'
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-6-1.png)<!-- -->

```r
# b) 
ggplot(data = mpg, mapping = aes(x = displ, y = hwy, group = drv)) + 
  geom_point(show.legend = F) + 
  geom_smooth(se = FALSE, show.legend = F)
```

```
## `geom_smooth()` using method = 'loess'
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-6-2.png)<!-- -->

```r
# c) 
ggplot(data = mpg, mapping = aes(x = displ, y = hwy, color = drv)) + 
  geom_point() + 
  geom_smooth(se = FALSE)
```

```
## `geom_smooth()` using method = 'loess'
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-6-3.png)<!-- -->

```r
# d) 
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_point(mapping = aes(color = drv)) + 
  geom_smooth(se = FALSE)
```

```
## `geom_smooth()` using method = 'loess'
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-6-4.png)<!-- -->

```r
# e)
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_point(mapping = aes(color = drv)) + 
  geom_smooth(mapping = aes(linetype = drv), se = FALSE)
```

```
## `geom_smooth()` using method = 'loess'
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-6-5.png)<!-- -->

```r
# f) 
ggplot(mpg, aes(displ, hwy)) +
  geom_point(aes(fill = drv), shape = 21, stroke = 2, colour = "white", size = 3) 
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-6-6.png)<!-- -->

## 3.7.1 Exercises
# 1) 
What is the default geom associated with stat_summary()? How could you rewrite the previous plot to use that geom function instead of the stat function?

```r
ggplot(data = diamonds) + 
  geom_pointrange(
    mapping = aes(x = cut, y = depth),
    stat = "summary",
    fun.ymin = min,
    fun.ymax = max,
    fun.y = median
  ) 
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-7-1.png)<!-- -->

# 2) 
What does geom_col() do? How is it different to geom_bar()?

```r
ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut))
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-8-1.png)<!-- -->

```r
# ggplot(data = diamonds) + 
#   geom_col(mapping = aes(x = cut))

library(tibble)
```

```
## Warning: package 'tibble' was built under R version 3.2.5
```

```r
demo <- tribble(
  ~a,      ~b,
  "bar_1", 20,
  "bar_2", 30,
  "bar_3", 40
)
ggplot(data = demo) +
  geom_bar(mapping = aes(x = a, y = b), stat = "identity")
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-8-2.png)<!-- -->

```r
ggplot(data = demo) +
  geom_col(mapping = aes(x = a, y = b))
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-8-3.png)<!-- -->

```r
# geom_bar uses stat_count by default: it counts the number of cases at each x position. geom_col uses stat_identity: it leaves the data as is.
```

# 3) 
Most geoms and stats come in pairs that are almost always used in concert. Read through the documentation and make a list of all the pairs. What do they have in common?

```r
# geom_area & stat_identity
# geom_bar & stat_count by default 
# geom_boxplot & stat_boxplot
# geom_errorbar & stat_identity 
# geom_histogram & stat_bin  
```

# 4) 
What variables does stat_smooth() compute? What parameters control its behaviour?

```r
# stat_smooth VS geom_smooth
ggplot(data = mpg, mapping = aes(x = displ, y = hwy, color = drv)) + 
  geom_point() + 
  stat_smooth(se = FALSE) # no confidence interval  
```

```
## `geom_smooth()` using method = 'loess'
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-10-1.png)<!-- -->

# 5) 
In our proportion bar chart, we need to set group = 1. Why? In other words what is the problem with these two graphs?

```r
ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut, y = ..prop.., group = 1)) 
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-11-1.png)<!-- -->

```r
ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut, y = ..prop..))
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-11-2.png)<!-- -->

```r
ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut, fill = color, y = ..prop..))
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-11-3.png)<!-- -->

```r
# If group is not set to 1, then all the bars have prop == 1. The function geom_bar assumes that the groups are equal to the x values, since the stat computes the counts within the group. 
```

## 3.8.1 Exercises
# 1) 
What is the problem with this plot? How could you improve it? 

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_point()
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-12-1.png)<!-- -->

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_point(position = "jitter")
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-12-2.png)<!-- -->

# 2) 
What parameters to geom_jitter() control the amount of jittering?

```r
?geom_jitter 
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_point()
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-13-1.png)<!-- -->

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_point(position = "jitter")
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-13-2.png)<!-- -->

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_jitter(width = 10, height = 10)
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-13-3.png)<!-- -->

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_jitter(width = 10, height = 1)
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-13-4.png)<!-- -->

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_jitter(width = 1, height = 1) 
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-13-5.png)<!-- -->

# 3) 
Compare and contrast geom_jitter() with geom_count() 

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_jitter()
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-14-1.png)<!-- -->

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_count()
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-14-2.png)<!-- -->

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_count() + 
  geom_jitter()
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-14-3.png)<!-- -->

```r
?geom_count # counts the number of observations at each location, then maps the count to point area. 
```

# 4) 
What’s the default position adjustment for geom_boxplot()? Create a visualisation of the mpg dataset that demonstrates it. 

```r
?geom_boxplot # identity OR dodge OR fill OR jitter OR stack

ggplot(data = mpg, mapping = aes(x = drv, y = hwy, color = class)) + 
  geom_boxplot() 
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-15-1.png)<!-- -->

```r
ggplot(data = mpg, mapping = aes(x = drv, y = hwy, color = class)) + 
  geom_boxplot(position = "dodge") 
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-15-2.png)<!-- -->

```r
ggplot(data = mpg, mapping = aes(x = drv, y = hwy, color = class)) + 
  geom_boxplot(position = "identity") 
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-15-3.png)<!-- -->

```r
ggplot(data = mpg, mapping = aes(x = drv, y = hwy, color = class)) + 
  geom_boxplot(position = "fill") 
```

```
## Warning: Stacking not well defined when not anchored on the axis
```

```
## Warning: Removed 11 rows containing missing values (position_stack).
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-15-4.png)<!-- -->

```r
ggplot(data = mpg, mapping = aes(x = drv, y = hwy, color = class)) + 
  geom_boxplot(position = "jitter") 
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-15-5.png)<!-- -->

```r
ggplot(data = mpg, mapping = aes(x = drv, y = hwy, color = class)) + 
  geom_boxplot(position = "stack") 
```

```
## Warning: Stacking not well defined when not anchored on the axis

## Warning: Removed 11 rows containing missing values (position_stack).
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-15-6.png)<!-- -->
 
## 3.9.1 Exercises
# 1) 
Turn a stacked bar chart into a pie chart using coord_polar().

```r
p <- ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut, y = ..prop.., fill = color)) 
p + coord_polar()
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-16-1.png)<!-- -->

# 2) 
What does labs() do? Read the documentation.

```r
?labs # modify axis, legend and plot labels 
```

# 3) 
What’s the difference between coord_quickmap() and coord_map()

```r
# install.packages("mapproj")
library("mapproj")
```

```
## Loading required package: maps
```

```
## Warning: package 'maps' was built under R version 3.2.5
```

```r
library("maps")
nz <- map_data("nz")

ggplot(nz, aes(long, lat, group = group)) +
  geom_polygon(fill = "white", colour = "black")
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-18-1.png)<!-- -->

```r
ggplot(nz, aes(long, lat, group = group)) +
  geom_polygon(fill = "white", colour = "black") +
  coord_quickmap() 
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-18-2.png)<!-- -->

```r
ggplot(nz, aes(long, lat, group = group)) +
  geom_polygon(fill = "white", colour = "black") +
  coord_map()
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-18-3.png)<!-- -->

```r
?coord_map
?coord_quickmap
```

# 4) 
What does the plot below tell you about the relationship between city and highway mpg? Why is coord_fixed() important? What does geom_abline() do?

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) +
  geom_point() + 
  geom_abline() +
  coord_fixed()
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-19-1.png)<!-- -->

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) +
  geom_point() + 
  geom_abline() 
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-19-2.png)<!-- -->

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) +
  geom_point() 
```

![](Assignment_05_02_2017_files/figure-html/unnamed-chunk-19-3.png)<!-- -->

```r
# almost linear relationship. 
?geom_abline
?coord_fixed 
```





