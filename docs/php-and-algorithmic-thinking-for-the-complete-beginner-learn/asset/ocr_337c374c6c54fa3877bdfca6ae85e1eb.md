# 23.2 Decision Control Structures in Solving Mathematical Problems

# Exercise 23.2-1  *Finding the Value of y*

Design a flowchart and write the corresponding PHP script that finds and displays the value of y (if possible) in the following formula.

\[Y = \frac{5+x}{x} + \frac{x+9}{x-4}\]

# Solution

In this exercise the user should not be allowed to enter values 0 or 4 because they make the denominator equal to zero. Therefore, the script needs to take these restrictions into consideration. The flowchart is shown here.

![](bbox=[0.139, 0.355, 0.89, 0.692])

and the PHP script is shown here.

```
```php
<?php

$x = trim(fgets(STDIN));

if ($x == 0 || $x == 4) {
    echo "Error: Division by zero";
}
else {
    $y = (5 + $x) / $x + ($x + 9) / ($x - 4);
    echo $y;
}
```
```