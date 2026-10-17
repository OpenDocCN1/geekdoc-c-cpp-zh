
## Chapter 16
### The Single-Alternative Decision Structure

3. Fill in the following table with the words “True” or “False” according to the values of the Boolean expressions BE1 and BE2.

| Boolean Expression1 (BE1) | Boolean Expression2 (BE2) | BE1 || BE2 | BE1 && BE2 | !(BE2) |
|---|---|---|---|---|---|
| False | False |  |  |  | |
| False | True |  |  |  | |
| True | False |  |  |  | |
| True | True |  |  |  | |

4. Fill in the following table with the words “True” or “False” according to the values of variables $a, $b, and $c.

| $a | $b | $c | $a > 3 || $c > $b && $c > 1 | $a > 3 && $c > $b || $c > 1 |
|---|---|---|---|---|---|
| 4 | -6 | 2 |  |  |
| -3 | 2 | -4 |  |  |
| 2 | 5 | 5 |  |  |

5. For $x = 4, $y = -2 and $flag = true, fill in the following table with the corresponding values.

| Expression | Value |
|---|---|
| pow($x + $y, 3) |  |
| ($x + $y) / (pow($x, 2) - 14) |  |
| ($x - 1) == $y + 5 |  |
| $x > 2 && $y == 1 |  |
| $x == 1 || $y == -2 && !($flag == false) |  |
| !($x >= 3) && ($x % 2 > 1) |  |

6. Calculate the result of each the following complex Boolean expressions when variables $a, $b, $c, and $d contain the values 6, -3, 4, and 7 respectively.

+   i. (3 * $a + $b / 5 - $c * $b / $a > 4) && ($b != -3)
+   ii. ($a * $b - $c / 2 + 21 * $c / 3 != 8) || ($a >= 5)

7. A head teacher asks the students to raise their hands according to their age. He wants to find the students who are:

+   i. under the age of 12, but not those who are 8 years old.
+   ii. between the ages of 6 and 9, and also those who are 11 years old.
+   iii. over the age of 7, but not those who are 10 or 12 years old.
+   iv. 6, 9, and 11 years old.

# Chapter 16
### The Single-Alternative Decision Structure

> **Notice:** A very common mistake that novice programmers make when writing PHP scripts is to confuse the assignment operator with the equal operator. They frequently make the mistake of writing `if ($x = $y)` when they actually want to say `if ($x == $y)`.

# Exercise 16.1-1  *Trace Tables and Single-Alternative Decision Structures*

Design the corresponding flowchart and create a trace table to determine the values of the variables in each step of the next PHP script for two different executions. The input values for the two executions are (i) 10, and (ii) 51.

```php
<?php

$a = trim(fgets(STDIN));

$y = 5;
if ($a * 2 > 100) {
    $a = $a * 3;
    $y = $a * 4;
}

echo $a, $y;

?>
```

# Solution

The flowchart is shown here.

![](img/4d9a992abc5da7946ac44f9e6bf1d032_196_0.png)

+   3. It is possible that none of the statements enclosed in a single-alternative decision structure will be executed.
+   
+   4. In a flowchart, the Decision symbol represents the beginning and the end of an algorithm.
+   
+   5. The code fragment
+   
+   ```php
+   define("if", 5);
+   $x = if + 5;
+   ```
+   
+   is syntactically correct.
+   
+   6. The single-alternative decision structure uses the reserved keyword `else`.
+   
+   7. The following code fragment satisfies the property of definiteness.
+   
+   ```php
+   if ($b != 3) {
+       $x = $a / ($b - 3);
+   }
+   ```
+   
+   8. The following PHP script satisfies the property of definiteness.
+   
+   ```php
+   <?php
+   $a = trim(fgets(STDIN));
+   $b = trim(fgets(STDIN));
+   
+   if ($b != 3) {
+       $x = $a / ($b - 3);
+   }
+   echo $x;
+   ?>
+   ```

# 16.3  Review Questions: Multiple Choice

Select the correct answer for each of the following statements.

+   1. The single-alternative decision structure is used when
+      a. statements are executed one after another.
+      b. a decision must be made before executing some statements.
+      c. none of the above
+      d. all of the above
+   
+   2. The single-alternative decision structure includes a statement or block of statements on
+      a. the false path only.
+      b. both paths.
+      c. the true path only.

# 3. In the following code fragment,

```php
if ($x == 3)
    $x = 5;
    $y++;
```

the statement `$y++` is executed

+   a. only when variable `$x` contains a value of 3.  
+   b. only when variable `$x` contains a value of 5.  
+   c. only when variable `$x` contains a value other than 3.  
+   d. either way.

# 4. In the following code fragment,

```php
if ($x % 2 == 0) $y++;
```

the statement `$y++` is executed when

+   a. variable `$x` is exactly divisible by 2.  
+   b. variable `$x` contains an even number.  
+   c. variable `$x` does not contain an odd number.  
+   d. all of the above  
+   e. none of the above

# 5. In the following code fragment,

```php
$x = 3 * $y;
if ($x > $y) $y++;
```

the statement `$y++` is

+   a. always executed.  
+   b. never executed.  
+   c. executed either way.  
+   d. executed only when variable `$y` contains positive values.  
+   e. none of the above

# 16.4 Review Exercises

Complete the following exercises.

# 1. Identify the syntax errors in the following PHP script:

```php
<?php

$x = trim(fgets(STDIN));

$y <− 5;
if ($x * $y / 2 > 20)
    $y--
    $x == 4 * $x2;
}
```

```php
echo $x $y;
?>
```

+   2. Create a trace table to determine the values of the variables in each step of the following PHP script for two different executions. Then, design the corresponding flowchart.
+   
+   The input values for the two executions are (i) 10, and (ii) -10.

```php
<?php

$x = trim(fgets(STDIN));

$y = -5;
if ($x * $y / 2 > 20) {
    $y--;
    $x -= 4;
}

if ($x > 0) {
    $y += 30;
    $x = pow($x, 2);
}

echo $x, $y;
?>
```

+   3. Create a trace table to determine the values of the variables in each step of the following PHP script for two different executions. Then, design the corresponding flowchart.
+   
+   The input values for the two executions are (i) -11, and (ii) 11.

```php
<?php

$x = trim(fgets(STDIN));

$y = 0;
if (abs($x) > 10) {
    $y += $x;
    $x--;
}

if (abs($x) > 10) {
    $y *= 3;
}

echo $x, $y;
?>
```

# The Single-Alternative Decision Structure

4. Create a trace table to determine the values of the variables in each step of the following PHP script for two different executions. Then, design the corresponding flowchart.

The input values for the two executions are (i) 1, 2, 3; and (ii) 4, 2, 1.

```php
<?php

$x = trim(fgets(STDIN));
$y = trim(fgets(STDIN));
$z = trim(fgets(STDIN));

if ($x + $y > $z)
    $x = $y + $z;
if ($x > $y + $z)
    $y = $x + $z;
if ($x > $y - $z)
    $z = $x - $z % 2;

echo $x, $y, $z;
?>
```

+   5. Write a PHP script that prompts the user to enter a number, and then displays the message “Positive” when the given number is positive.
+   
+   6. Write a PHP script that prompts the user to enter two numbers, and then displays the message “Positive” when both given numbers are positives.
+   
+   7. Write a PHP script that prompts the user to enter a value and then displays the message “Numeric” when the given value is a numeric value.
+   
+   Hint: Use the `is_numeric()` function.
+   
+   8. Write a PHP script that prompts the user to enter a string, and then displays the message “Uppercase” when the given string contains only uppercase characters.
+   
+   Hint: Use the `strtoupper()` function
+   
+   9. Write a PHP script that prompts the user to enter a string, and then displays the message “Many characters” when the given string contains more than 20 characters.
+   
+   Hint: Use the `strlen()` function
+   
+   10. Write a PHP script that prompts the user to enter four numbers and, if one of them is negative, it displays the message “Among the given numbers, there is a negative one!”
+   
+   11. Write a PHP script that prompts the user to enter two numbers. If the first number given is greater than the second one, the script should swap their values. In the end, the script should display the numbers, always in ascending order.
