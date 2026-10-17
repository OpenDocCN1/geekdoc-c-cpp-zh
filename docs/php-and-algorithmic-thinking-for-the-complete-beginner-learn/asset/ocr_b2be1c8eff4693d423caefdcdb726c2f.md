# # Exercise 35.2-1 Finding the Average Value

There are 20 students and each one of them has received his or her grades for 10 lessons. Write a PHP script that prompts the user to enter the grades of each student for all lessons and then calculates and displays, for each student, all average values that are greater than 89.

# # Solution

Since you’ve learned two approaches for processing each row individually, let’s use them both.

# # First Approach – Creating an auxiliary array

In this approach, the script processes each row individually and creates an auxiliary array in which each position stores the average value of one row. The two required arrays are shown next.

After the array $average is created, the script can find and display all average values that are greater than 89. The PHP script is as follows.

# # file_35.2-1a.php

```
```php
<?php
define("STUDENTS", 20);
define("LESSONS", 10);

$grades = array(array());
for ($i = 0; $i <= STUDENTS - 1; $i++) {
echo "For student No. ", $i + 1, "...\n";
```
```

![](bbox=[0.183, 0.458, 0.842, 0.752])

```
```php
$average = $sum / COLUMNS;
echo $average;
}
```
```