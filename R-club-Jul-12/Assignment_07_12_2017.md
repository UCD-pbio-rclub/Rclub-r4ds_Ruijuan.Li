# Assignment_07_12_2017
Ruijuan Li  
7/12/2017  

# 14.2.5 Exercises

1. In code that doesn’t use stringr, you’ll often see paste() and paste0(). What’s the difference between the two functions? What stringr function are they equivalent to? How do the functions differ in their handling of NA?

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

```r
?stringr
?paste # Concatenate vectors after converting to character. 

## When passing a single vector, paste0 and paste work like as.character.
paste0(1:12)
```

```
##  [1] "1"  "2"  "3"  "4"  "5"  "6"  "7"  "8"  "9"  "10" "11" "12"
```

```r
paste(1:12)        # same
```

```
##  [1] "1"  "2"  "3"  "4"  "5"  "6"  "7"  "8"  "9"  "10" "11" "12"
```

```r
as.character(1:12) # same
```

```
##  [1] "1"  "2"  "3"  "4"  "5"  "6"  "7"  "8"  "9"  "10" "11" "12"
```

```r
## If you pass several vectors to paste0, they are concatenated in a
## vectorized way.
(nth <- paste0(1:12, c("st", "nd", "rd", rep("th", 9))))
```

```
##  [1] "1st"  "2nd"  "3rd"  "4th"  "5th"  "6th"  "7th"  "8th"  "9th"  "10th"
## [11] "11th" "12th"
```

```r
(nth <- paste(1:12, c("st", "nd", "rd", rep("th", 9))))
```

```
##  [1] "1 st"  "2 nd"  "3 rd"  "4 th"  "5 th"  "6 th"  "7 th"  "8 th" 
##  [9] "9 th"  "10 th" "11 th" "12 th"
```

```r
## paste works the same, but separates each input with a space.

?str_join
str_c(1:12) 
```

```
##  [1] "1"  "2"  "3"  "4"  "5"  "6"  "7"  "8"  "9"  "10" "11" "12"
```

2. In your own words, describe the difference between the sep and collapse arguments to str_c().

```r
# sep is to specify the symbol used between different strings
# collapse is the symbol used in between words of a single string.  
```

3. Use str_length() and str_sub() to extract the middle character from a string. What will you do if the string has an even number of characters?

```r
?str_length
?str_sub

string_eg <- str_c(letters, collapse = "")
str_length(string_eg)/2
```

```
## [1] 13
```

```r
extract.middle <- function(string){
  if (length(string) %% 2 == 0){ 
  middle_vlaue <- str_sub(string, str_length(string)/2, str_length(string)/2+1)}
  else {
    middle_vlaue <- str_sub(string, str_length(string)/2+1, str_length(string)/2+1)
  return(middle_vlaue)
  }
  }  

extract.middle(string = string_eg)
```

```
## [1] "n"
```

4. What does str_wrap() do? When might you want to use it?

```r
# This is a wrapper around stri_wrap which implements the Knuth-Plass paragraph wrapping algorithm.
# would be useful when parse a paragraph
?str_wrap
thanks_path <- file.path(R.home("doc"), "THANKS")
thanks <- str_c(readLines(thanks_path), collapse = "\n")
thanks <- word(thanks, 1, 3, fixed("\n\n"))
cat(str_wrap(thanks), "\n")
```

```
## R would not be what it is today without the invaluable help of these people,
## who contributed by donating code, bug fixes and documentation: Valerio Aimale,
## Thomas Baier, Henrik Bengtsson, Roger Bivand, Ben Bolker, David Brahm, G"oran
## Brostr"om, Patrick Burns, Vince Carey, Saikat DebRoy, Brian D'Urso, Lyndon
## Drake, Dirk Eddelbuettel, Claus Ekstrom, Sebastian Fischmeister, John Fox,
## Paul Gilbert, Yu Gong, Gabor Grothendieck, Frank E Harrell Jr, Torsten Hothorn,
## Robert King, Kjetil Kjernsmo, Roger Koenker, Philippe Lambert, Jan de Leeuw,
## Jim Lindsey, Patrick Lindsey, Catherine Loader, Gordon Maclean, John Maindonald,
## David Meyer, Ei-ji Nakama, Jens Oehlschaegel, Steve Oncley, Richard O'Keefe,
## Hubert Palme, Roger D. Peng, Jose' C. Pinheiro, Tony Plate, Anthony Rossini,
## Jonathan Rougier, Petr Savicky, Guenther Sawitzki, Marc Schwartz, Detlef Steuer,
## Bill Simpson, Gordon Smyth, Adrian Trapletti, Terry Therneau, Rolf Turner,
## Bill Venables, Gregory R. Warnes, Andreas Weingessel, Morten Welinder, James
## Wettenhall, Simon Wood, and Achim Zeileis. Others have written code that has
## been adopted by R and is acknowledged in the code files, including
```

```r
cat(str_wrap(thanks, width = 40), "\n")
```

```
## R would not be what it is today without
## the invaluable help of these people,
## who contributed by donating code, bug
## fixes and documentation: Valerio Aimale,
## Thomas Baier, Henrik Bengtsson, Roger
## Bivand, Ben Bolker, David Brahm, G"oran
## Brostr"om, Patrick Burns, Vince Carey,
## Saikat DebRoy, Brian D'Urso, Lyndon
## Drake, Dirk Eddelbuettel, Claus Ekstrom,
## Sebastian Fischmeister, John Fox, Paul
## Gilbert, Yu Gong, Gabor Grothendieck,
## Frank E Harrell Jr, Torsten Hothorn,
## Robert King, Kjetil Kjernsmo, Roger
## Koenker, Philippe Lambert, Jan de
## Leeuw, Jim Lindsey, Patrick Lindsey,
## Catherine Loader, Gordon Maclean, John
## Maindonald, David Meyer, Ei-ji Nakama,
## Jens Oehlschaegel, Steve Oncley,
## Richard O'Keefe, Hubert Palme, Roger
## D. Peng, Jose' C. Pinheiro, Tony Plate,
## Anthony Rossini, Jonathan Rougier,
## Petr Savicky, Guenther Sawitzki, Marc
## Schwartz, Detlef Steuer, Bill Simpson,
## Gordon Smyth, Adrian Trapletti, Terry
## Therneau, Rolf Turner, Bill Venables,
## Gregory R. Warnes, Andreas Weingessel,
## Morten Welinder, James Wettenhall, Simon
## Wood, and Achim Zeileis. Others have
## written code that has been adopted by R
## and is acknowledged in the code files,
## including
```

```r
cat(str_wrap(thanks, width = 60, indent = 2), "\n")
```

```
##   R would not be what it is today without the invaluable help
## of these people, who contributed by donating code, bug fixes
## and documentation: Valerio Aimale, Thomas Baier, Henrik
## Bengtsson, Roger Bivand, Ben Bolker, David Brahm, G"oran
## Brostr"om, Patrick Burns, Vince Carey, Saikat DebRoy, Brian
## D'Urso, Lyndon Drake, Dirk Eddelbuettel, Claus Ekstrom,
## Sebastian Fischmeister, John Fox, Paul Gilbert, Yu Gong,
## Gabor Grothendieck, Frank E Harrell Jr, Torsten Hothorn,
## Robert King, Kjetil Kjernsmo, Roger Koenker, Philippe
## Lambert, Jan de Leeuw, Jim Lindsey, Patrick Lindsey,
## Catherine Loader, Gordon Maclean, John Maindonald, David
## Meyer, Ei-ji Nakama, Jens Oehlschaegel, Steve Oncley,
## Richard O'Keefe, Hubert Palme, Roger D. Peng, Jose' C.
## Pinheiro, Tony Plate, Anthony Rossini, Jonathan Rougier,
## Petr Savicky, Guenther Sawitzki, Marc Schwartz, Detlef
## Steuer, Bill Simpson, Gordon Smyth, Adrian Trapletti, Terry
## Therneau, Rolf Turner, Bill Venables, Gregory R. Warnes,
## Andreas Weingessel, Morten Welinder, James Wettenhall, Simon
## Wood, and Achim Zeileis. Others have written code that has
## been adopted by R and is acknowledged in the code files,
## including
```

```r
cat(str_wrap(thanks, width = 60, exdent = 2), "\n")
```

```
## R would not be what it is today without the invaluable help
##   of these people, who contributed by donating code, bug fixes
##   and documentation: Valerio Aimale, Thomas Baier, Henrik
##   Bengtsson, Roger Bivand, Ben Bolker, David Brahm, G"oran
##   Brostr"om, Patrick Burns, Vince Carey, Saikat DebRoy, Brian
##   D'Urso, Lyndon Drake, Dirk Eddelbuettel, Claus Ekstrom,
##   Sebastian Fischmeister, John Fox, Paul Gilbert, Yu Gong,
##   Gabor Grothendieck, Frank E Harrell Jr, Torsten Hothorn,
##   Robert King, Kjetil Kjernsmo, Roger Koenker, Philippe
##   Lambert, Jan de Leeuw, Jim Lindsey, Patrick Lindsey,
##   Catherine Loader, Gordon Maclean, John Maindonald, David
##   Meyer, Ei-ji Nakama, Jens Oehlschaegel, Steve Oncley,
##   Richard O'Keefe, Hubert Palme, Roger D. Peng, Jose' C.
##   Pinheiro, Tony Plate, Anthony Rossini, Jonathan Rougier,
##   Petr Savicky, Guenther Sawitzki, Marc Schwartz, Detlef
##   Steuer, Bill Simpson, Gordon Smyth, Adrian Trapletti, Terry
##   Therneau, Rolf Turner, Bill Venables, Gregory R. Warnes,
##   Andreas Weingessel, Morten Welinder, James Wettenhall, Simon
##   Wood, and Achim Zeileis. Others have written code that has
##   been adopted by R and is acknowledged in the code files,
##   including
```

```r
cat(str_wrap(thanks, width = 0, exdent = 2), "\n") 
```

```
## R
##   would
##   not
##   be
##   what
##   it
##   is
##   today
##   without
##   the
##   invaluable
##   help
##   of
##   these
##   people,
##   who
##   contributed
##   by
##   donating
##   code,
##   bug
##   fixes
##   and
##   documentation:
##   Valerio
##   Aimale,
##   Thomas
##   Baier,
##   Henrik
##   Bengtsson,
##   Roger
##   Bivand,
##   Ben
##   Bolker,
##   David
##   Brahm,
##   G"oran
##   Brostr"om,
##   Patrick
##   Burns,
##   Vince
##   Carey,
##   Saikat
##   DebRoy,
##   Brian
##   D'Urso,
##   Lyndon
##   Drake,
##   Dirk
##   Eddelbuettel,
##   Claus
##   Ekstrom,
##   Sebastian
##   Fischmeister,
##   John
##   Fox,
##   Paul
##   Gilbert,
##   Yu
##   Gong,
##   Gabor
##   Grothendieck,
##   Frank
##   E
##   Harrell
##   Jr,
##   Torsten
##   Hothorn,
##   Robert
##   King,
##   Kjetil
##   Kjernsmo,
##   Roger
##   Koenker,
##   Philippe
##   Lambert,
##   Jan
##   de
##   Leeuw,
##   Jim
##   Lindsey,
##   Patrick
##   Lindsey,
##   Catherine
##   Loader,
##   Gordon
##   Maclean,
##   John
##   Maindonald,
##   David
##   Meyer,
##   Ei-
##   ji
##   Nakama,
##   Jens
##   Oehlschaegel,
##   Steve
##   Oncley,
##   Richard
##   O'Keefe,
##   Hubert
##   Palme,
##   Roger
##   D.
##   Peng,
##   Jose'
##   C.
##   Pinheiro,
##   Tony
##   Plate,
##   Anthony
##   Rossini,
##   Jonathan
##   Rougier,
##   Petr
##   Savicky,
##   Guenther
##   Sawitzki,
##   Marc
##   Schwartz,
##   Detlef
##   Steuer,
##   Bill
##   Simpson,
##   Gordon
##   Smyth,
##   Adrian
##   Trapletti,
##   Terry
##   Therneau,
##   Rolf
##   Turner,
##   Bill
##   Venables,
##   Gregory
##   R.
##   Warnes,
##   Andreas
##   Weingessel,
##   Morten
##   Welinder,
##   James
##   Wettenhall,
##   Simon
##   Wood,
##   and
##   Achim
##   Zeileis.
##   Others
##   have
##   written
##   code
##   that
##   has
##   been
##   adopted
##   by
##   R
##   and
##   is
##   acknowledged
##   in
##   the
##   code
##   files,
##   including
```

5. What does str_trim() do? What’s the opposite of str_trim()?

```r
?str_trim # Trim whitespace from start and end of string. 
str_trim("  String with trailing and leading white space\t")
```

```
## [1] "String with trailing and leading white space"
```

```r
str_trim("  String with trailing and leading white space    ")
```

```
## [1] "String with trailing and leading white space"
```

```r
str_pad("hadley", 3)
```

```
## [1] "hadley"
```

```r
str_pad("a", c(5, 10, 20)) # adding space 
```

```
## [1] "    a"                "         a"           "                   a"
```

6. Write a function that turns (e.g.) a vector c("a", "b", "c") into the string a, b, and c. Think carefully about what it should do if given a vector of length 0, 1, or 2.

```r
vec_to_str <- function(vector){
  str_c(vector, collapse = "")
}

vec_to_str(letters) # don't really see 
```

```
## [1] "abcdefghijklmnopqrstuvwxyz"
```

https://regexone.com/ regular expression 

# 14.3.5.1 Exercises

1. Describe, in words, what these expressions will match:

      1. (.)\1\1
      2. "(.)(.)\\2\\1"
      3. (..)\1
      4. "(.).\\1.\\1"
      5. "(.)(.)(.).*\\3\\2\\1"

```r
# from Julin 
str_view("appple","(.)\\1\\1") # a tripple repeated single letter 
```

<!--html_preserve--><div id="htmlwidget-6485ad886c19dc7e6a58" style="width:960px;height:auto;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-6485ad886c19dc7e6a58">{"x":{"html":"<ul>\n  <li>a<span class='match'>ppp<\/span>le<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

```r
str_view("abba is my favorite band", "(.)(.)\\2\\1") # two different letters repeat for 1:2:2 
```

<!--html_preserve--><div id="htmlwidget-8c01addb486e6d796f30" style="width:960px;height:auto;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-8c01addb486e6d796f30">{"x":{"html":"<ul>\n  <li><span class='match'>abba<\/span> is my favorite band<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

```r
str_view("abab is my favorite band", "(..)\\1") # A two character string repeated , ie "abab"
```

<!--html_preserve--><div id="htmlwidget-0c64434e00532f6bb797" style="width:960px;height:auto;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-0c64434e00532f6bb797">{"x":{"html":"<ul>\n  <li><span class='match'>abab<\/span> is my favorite band<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

```r
str_view("bananas are good", "(.).\\1.\\1") # A character repeated twice, but with any other characters inbetween 
```

<!--html_preserve--><div id="htmlwidget-8301db458ea7f6a8eb73" style="width:960px;height:auto;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-8301db458ea7f6a8eb73">{"x":{"html":"<ul>\n  <li>b<span class='match'>anana<\/span>s are good<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

```r
str_view("geese from canda see many sights","(.)(.)(.).*\\3\\2\\1") # A three character palindrome separated by any number of characters in the middle 
```

<!--html_preserve--><div id="htmlwidget-a8fd223749098518433e" style="width:960px;height:auto;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-a8fd223749098518433e">{"x":{"html":"<ul>\n  <li>g<span class='match'>eese from canda see<\/span> many sights<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

2. Construct regular expressions to match words that:

      1. Start and end with the same character.

      2. Contain a repeated pair of letters (e.g. “church” contains “ch” repeated twice.) 

```r
pattern <- "[A-Za-z]*([A-Za-z]{2})[a-z]*\\1[a-z]*"
str_view_all("what silly sentence am I going to write for this exercise?",pattern)
```

<!--html_preserve--><div id="htmlwidget-10fbbdf59700b34e27a1" style="width:960px;height:auto;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-10fbbdf59700b34e27a1">{"x":{"html":"<ul>\n  <li>what silly <span class='match'>sentence<\/span> am I going to write for this exercise?<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

      3. Contain one letter repeated in at least three places (e.g. “eleven” contains three “e”s.)

```r
pattern <- "[A-Za-z]*([A-Za-z])[a-z]*\\1[a-z]*\\1[a-z]*"
str_view_all("what silly sentence am I going to write for this exercise?  Aiyeee",pattern) 
```

<!--html_preserve--><div id="htmlwidget-dc501030d39503cbcb70" style="width:960px;height:auto;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-dc501030d39503cbcb70">{"x":{"html":"<ul>\n  <li>what silly <span class='match'>sentence<\/span> am I going to write for this <span class='match'>exercise<\/span>?  <span class='match'>Aiyeee<\/span><\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

