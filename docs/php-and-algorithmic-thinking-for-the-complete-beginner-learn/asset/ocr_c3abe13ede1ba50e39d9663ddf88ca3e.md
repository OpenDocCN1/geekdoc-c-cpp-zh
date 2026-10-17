# Exercise 17.1-4 *Finding Odd and Even Numbers*

Design a flowchart and write the corresponding PHP script that prompts the user to enter an integer, and then displays a message indicating whether this number is odd or even.

# Solution

In this exercise, you need to find a way to determine whether a number is odd or even. You need to find a common attribute between all even numbers, or between all odd numbers. And actually there is one! All even numbers are exactly divisible by 2. So, when the result of the operation x ÷ 2 equals 0, x is even; otherwise, x is odd.

Next you can find various odd and even numbers:

+   - Odd numbers: 1, 3, 5, 7, 9, 11...
+   - Even numbers: 0, 2, 4, 6, 8, 10, 12, ....

> **Notice:** Please note that zero is considered an even number.

The flowchart is shown here.

![](bbox=[0.287, 0.437, 0.735, 0.744])

and the PHP script is shown here.

```
```php
<?php
echo "Enter an integer ";
$x = trim(fgets(STDIN));

if ($x % 2 == 0) {
    echo "Even";
}
else {
```
```