# Assignment_07_19_2017
Ruijuan Li  
7/18/2017  

# 14.3.1.1 Exercises

1. Explain why each of these strings don’t match a \: "\", "\\", "\\\".
* "\": This will escape the next character in the R string.
* "\\": This will resolve to \ in the regular expression, which will escape the next character in the regular expression.
* "\\\": The first two backslashes will resolve to a literal backslash in the regular expression, the third will escape the next character. So in the regular expresion, this will escape some escaped character.

2. How would you match the sequence "'\?

3. What patterns will the regular expression \..\..\.. match? How would you represent it as a string?


