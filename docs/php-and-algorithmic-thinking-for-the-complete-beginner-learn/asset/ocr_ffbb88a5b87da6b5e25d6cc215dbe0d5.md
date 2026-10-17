# Chapter 23
More Exercises with Decision Control Structures

![](bbox=[0.058, 0.057, 0.969, 0.397])

In PHP, you can use the `is_numeric()` function to test whether or not a variable contains a numeric value. The PHP script is shown here.

```
```php
<?php

echo "Enter an integer: ";
$x = trim(fgets(STDIN));

if (is_numeric($x) == true) {
    if ($x % 5 == 0 && $x % 8 == 0) {
        echo $x, " is exactly divisible by 5 and by 8";
    }
    else {
        echo $x, " is not what you are looking for!";
    }
}
else {
    echo "Invalid Number";
}
?>
```
```

# Exercise 23.1-3   *Is it an Integer?*

Write a PHP script that prompts the user to enter a number and then displays a message indicating whether the data type of this number is integer or real. Moreover, if the user enters a non-numeric character, an error message should be displayed.

(This exercise gives you some more practice in working with data validation.)