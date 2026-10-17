# Exercise 39.4-2 Calculating the Sum of Two Numbers Using Fewer Lines of Code!

Rewrite the PHP script of the previous exercise using fewer lines of code.

# Solution

The solution is shown here.

```
```php
<?php
function sum($a, $b) {
    return $a + $b;
}

$num1 = trim(fgets(STDIN));
$num2 = trim(fgets(STDIN));

echo "The sum of ", $num1, " + ", $num2, " is ", sum($num1, $num2);
?>
```
```

Contrary to the solution of the previous exercise, in this function sum() the sum is not assigned to variable $s but it is directly calculated and returned. Furthermore, this main code doesn't assign the returned value to a variable but directly displays it.

> > Notice: User-defined functions can be called just like the built-in functions of PHP.

# 39.5 Review Questions: True/False

Choose true or false for each of the following statements.

+   1. There are two categories of functions in PHP.
+   2. The variables that are used to pass values to a function are called arguments.
+   3. The function trim() is a user-defined function.
+   4. Every call to a user-defined function is made in the same way as a call to the built-in functions of PHP.
+   5. There can be as many arguments as you wish in a function’s formal argument list.
+   6. In a function, the formal argument list must contain at least one argument.
+   7. In a function, the formal argument list is optional.