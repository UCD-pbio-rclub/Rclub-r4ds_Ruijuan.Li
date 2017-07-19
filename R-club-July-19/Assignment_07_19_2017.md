# Assignment_07_19_2017
Ruijuan Li  
7/18/2017  


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
library(stringr)
```

```
## Warning: package 'stringr' was built under R version 3.2.5
```

# 14.3.1.1 Exercises

1. Explain why each of these strings don’t match a \: "\", "\\", "\\\".
* "\": This will escape the next character in the R string.
* "\\": This will resolve to \ in the regular expression, which will escape the next character in the regular expression.
* "\\\": The first two backslashes will resolve to a literal backslash in the regular expression, the third will escape the next character. So in the regular expresion, this will escape some escaped character. 

```r
x1 <- "a\\b"
writeLines(x1)
```

```
## a\b
```

```r
x <- "a\b"
writeLines(x)
```

```
## a
```

```r
x <- "a\\\b"
writeLines(x)
```

```
## a\
```

```r
x <- "a\\\\b"
writeLines(x)
```

```
## a\\b
```

```r
#> a\b 
str_view(x1, "\\\\") 
```

<!--html_preserve--><div id="htmlwidget-4024f1f629ba5cc0abe8" style="width:960px;height:auto;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-4024f1f629ba5cc0abe8">{"x":{"html":"<ul>\n  <li>a<span class='match'>\\<\/span>b<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

2. How would you match the sequence "'\?

```r
x <- "\"\'\\"
writeLines(x)
```

```
## "'\
```

```r
str_view(x, "\"\'\\\\") 
```

<!--html_preserve--><div id="htmlwidget-89bd31f6a3b78363650f" style="width:960px;height:auto;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-89bd31f6a3b78363650f">{"x":{"html":"<ul>\n  <li><span class='match'>\"'\\<\/span><\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

3. What patterns will the regular expression \..\..\.. match? How would you represent it as a string?

      It will match any patterns that are a dot followed by any character, repeated three times. (???)

# 14.3.2.1 Exercises

1. How would you match the literal string "$^$"?

```r
x <- "$^$"
writeLines(x)
```

```
## $^$
```

```r
str_view(x, "^\\$\\^\\$$")
```

<!--html_preserve--><div id="htmlwidget-2928d3f331bcbb97623f" style="width:960px;height:auto;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-2928d3f331bcbb97623f">{"x":{"html":"<ul>\n  <li><span class='match'>$^$<\/span><\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

2. Given the corpus of common words in stringr::words, create regular expressions that find all words that:

      1. Start with “y”.
      2. End with “x”
      3. Are exactly three letters long. (Don’t cheat by using str_length()!)
      4. Have seven letters or more.


```r
str_view(c("yes", "happy"), "^y")
```

<!--html_preserve--><div id="htmlwidget-cf66f8aff5c646ef8cec" style="width:960px;height:auto;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-cf66f8aff5c646ef8cec">{"x":{"html":"<ul>\n  <li><span class='match'>y<\/span>es<\/li>\n  <li>happy<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

```r
str_view(c("tax", "xmas"), "x$")
```

<!--html_preserve--><div id="htmlwidget-6246369c3d05f2845b79" style="width:960px;height:auto;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-6246369c3d05f2845b79">{"x":{"html":"<ul>\n  <li>ta<span class='match'>x<\/span><\/li>\n  <li>xmas<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

```r
str_view(c("tax", "xmas"), "^[a-zA-Z]{3}$")
```

<!--html_preserve--><div id="htmlwidget-bc409ee9a200abec5dde" style="width:960px;height:auto;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-bc409ee9a200abec5dde">{"x":{"html":"<ul>\n  <li><span class='match'>tax<\/span><\/li>\n  <li>xmas<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

```r
str_view(c("birthday", "today", "Christmas"), "^[a-zA-Z]{7,}$")
```

<!--html_preserve--><div id="htmlwidget-65db7b0a18edbb640d84" style="width:960px;height:auto;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-65db7b0a18edbb640d84">{"x":{"html":"<ul>\n  <li><span class='match'>birthday<\/span><\/li>\n  <li>today<\/li>\n  <li><span class='match'>Christmas<\/span><\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

Since this list is long, you might want to use the match argument to str_view() to show only the matching or non-matching words.

# 14.3.3.1 Exercises

1. Create regular expressions to find all words that:

      1. Start with a vowel.

      2. That only contain consonants. (Hint: thinking about matching “not”-vowels.)

      3. End with ed, but not with eed.

      4. End with ing or ise.
      

```r
str_view(c("birthday", "Auburn", "earth", "iMac", "ohh", "Urea"), "^[aeiouAEIOU]")
```

<!--html_preserve--><div id="htmlwidget-b5efdb3abf716b0adbef" style="width:960px;height:auto;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-b5efdb3abf716b0adbef">{"x":{"html":"<ul>\n  <li>birthday<\/li>\n  <li><span class='match'>A<\/span>uburn<\/li>\n  <li><span class='match'>e<\/span>arth<\/li>\n  <li><span class='match'>i<\/span>Mac<\/li>\n  <li><span class='match'>o<\/span>hh<\/li>\n  <li><span class='match'>U<\/span>rea<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

```r
str_view(c("birthday", "Auburn", "earth", "iMac", "ohh", "Urea"), "^[a|e|i|o|u|A|E|I|O|U]")
```

<!--html_preserve--><div id="htmlwidget-e020498cc6c46bff336e" style="width:960px;height:auto;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-e020498cc6c46bff336e">{"x":{"html":"<ul>\n  <li>birthday<\/li>\n  <li><span class='match'>A<\/span>uburn<\/li>\n  <li><span class='match'>e<\/span>arth<\/li>\n  <li><span class='match'>i<\/span>Mac<\/li>\n  <li><span class='match'>o<\/span>hh<\/li>\n  <li><span class='match'>U<\/span>rea<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

```r
str_view(c("birthday", "Auburn", "earth", "iMac", "ohh", "Urea"), "^[^a|e|i|o|u|A|E|I|O|U]")
```

<!--html_preserve--><div id="htmlwidget-37ac00ea34447c9b805c" style="width:960px;height:auto;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-37ac00ea34447c9b805c">{"x":{"html":"<ul>\n  <li><span class='match'>b<\/span>irthday<\/li>\n  <li>Auburn<\/li>\n  <li>earth<\/li>\n  <li>iMac<\/li>\n  <li>ohh<\/li>\n  <li>Urea<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

```r
str_view(c("led", "let", "seed"), "[^e]ed$")
```

<!--html_preserve--><div id="htmlwidget-cc11495f03756fb427a9" style="width:960px;height:auto;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-cc11495f03756fb427a9">{"x":{"html":"<ul>\n  <li><span class='match'>led<\/span><\/li>\n  <li>let<\/li>\n  <li>seed<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

```r
str_view(c("ending", "rise", "seed"), "ise$|ing$") 
```

<!--html_preserve--><div id="htmlwidget-70b1a9d8b3f7461a8fdd" style="width:960px;height:auto;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-70b1a9d8b3f7461a8fdd">{"x":{"html":"<ul>\n  <li>end<span class='match'>ing<\/span><\/li>\n  <li>r<span class='match'>ise<\/span><\/li>\n  <li>seed<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

2. Empirically verify the rule “i before e except after c”.

3. Is “q” always followed by a “u”?

```r
str_view(stringr::words, "qu", match = T)
```

<!--html_preserve--><div id="htmlwidget-97e19b1dced7a93881b3" style="width:960px;height:auto;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-97e19b1dced7a93881b3">{"x":{"html":"<ul>\n  <li>e<span class='match'>qu<\/span>al<\/li>\n  <li><span class='match'>qu<\/span>ality<\/li>\n  <li><span class='match'>qu<\/span>arter<\/li>\n  <li><span class='match'>qu<\/span>estion<\/li>\n  <li><span class='match'>qu<\/span>ick<\/li>\n  <li><span class='match'>qu<\/span>id<\/li>\n  <li><span class='match'>qu<\/span>iet<\/li>\n  <li><span class='match'>qu<\/span>ite<\/li>\n  <li>re<span class='match'>qu<\/span>ire<\/li>\n  <li>s<span class='match'>qu<\/span>are<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

4. Write a regular expression that matches a word if it’s probably written in British English, not American English.
https://jrnold.github.io/e4qf/strings.html

5. Create a regular expression that will match telephone numbers as commonly written in your country.

```r
x <- c("123-456-7890", "1235-2351")
str_view(x, "\\d\\d\\d-\\d\\d\\d-\\d\\d\\d\\d")
```

<!--html_preserve--><div id="htmlwidget-7c9bc4bdbea350bf69ca" style="width:960px;height:auto;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-7c9bc4bdbea350bf69ca">{"x":{"html":"<ul>\n  <li><span class='match'>123-456-7890<\/span><\/li>\n  <li>1235-2351<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

# 14.3.4.1 Exercises

1. Describe the equivalents of ?, +, * in {m,n} form.

```r
str_view(c("birthday", "today", "Christmas", "happy", "happpy"), "(p)?")
```

<!--html_preserve--><div id="htmlwidget-be9ff1af5d878b68e088" style="width:960px;height:auto;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-be9ff1af5d878b68e088">{"x":{"html":"<ul>\n  <li><span class='match'><\/span>birthday<\/li>\n  <li><span class='match'><\/span>today<\/li>\n  <li><span class='match'><\/span>Christmas<\/li>\n  <li><span class='match'><\/span>happy<\/li>\n  <li><span class='match'><\/span>happpy<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

```r
str_view(c("birthday", "today", "Christmas", "happy", "happpy"), "p?") 
```

<!--html_preserve--><div id="htmlwidget-c3e4a808ff60e6532e84" style="width:960px;height:auto;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-c3e4a808ff60e6532e84">{"x":{"html":"<ul>\n  <li><span class='match'><\/span>birthday<\/li>\n  <li><span class='match'><\/span>today<\/li>\n  <li><span class='match'><\/span>Christmas<\/li>\n  <li><span class='match'><\/span>happy<\/li>\n  <li><span class='match'><\/span>happpy<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

2. Describe in words what these regular expressions match: (read carefully to see if I’m using a regular expression or a string that defines a regular expression.)

      ^.*$
      "\\{.+\\}"
      \d{4}-\d{2}-\d{2}
      "\\\\{4}"
      
3. Create regular expressions to find all words that:

      Start with three consonants.
      Have three or more vowels in a row.
      Have two or more vowel-consonant pairs in a row.

4. Solve the beginner regexp crosswords at https://regexcrossword.com/challenges/beginner.

###################################################### 


