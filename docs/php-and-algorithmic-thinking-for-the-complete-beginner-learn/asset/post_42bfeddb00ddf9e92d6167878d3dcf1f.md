

# 7. Try, without using a trace table, to determine the values that the array will contain when the following code fragment is executed.

$a = array(array(11, 10),
array(15, 19),
array(22, 15));
for ($j = 0; $j <= 1; $j++) {
for ($i = 0; $i <= 2; $i++) {
if ($i == 2)
$a[$i][$j] += $a[$i - 1][$j];
else
$a[$i][$j] += $a[$i + 1][$j];
}
}

# 8. Assume that array $a contains the following values.

|    | 0   | 1   | 2   | 3   |
|---|---|---|---|---|
| 0  | -1  | 15  | 22  | 3   |
| 1  | 25  | 12  | 16  | 14  |
| 2  | 7   | 9   | 1   | 45  |
| 3  | 40  | 17  | 11  | 13  |

# What displays on the screen after executing each of the following code fragments?

i) for ($i = 0; $i <= 2; $i++) {
for ($j = 0; $j <= 2; $j++) {
echo $a[$i][$j], " ";
}
}

ii) for ($i = 2; $i >= 0; $i--) {
for ($j = 0; $j <= 2; $j++) {
echo $a[$i][$j], " ";
}
}

iii)
```php
for ($i = 0; $i <= 2; $i++) {
    for ($j = 2; $j >= 0; $j--)
        echo $a[$i][$j], " ";
}
```

iv)
```php
for ($i = 2; $i >= 0; $i--)
    for ($j = 2; $j >= 0; $j--)
        echo $a[$i][$j], " ";
```

v)
```php
for ($j = 0; $j <= 2; $j++) {
    for ($i = 0; $i <= 2; $i++)
        echo $a[$i][$j], " ";
}
```

vi)
```php
for ($j = 0; $j <= 2; $j++) {
    for ($i = 2; $i >= 0; $i--)
        echo $a[$i][$j], " ";
}
```

vii)
```php
for ($j = 2; $j >= 0; $j--) {
    for ($i = 0; $i <= 2; $i++)
        echo $a[$i][$j], " ";
}
```

viii)
```php
for ($j = 2; $j >= 0; $j--)
    for ($i = 2; $i >= 0; $i--)
        echo $a[$i][$j], " ";
```

9. Write a PHP script that lets the user enter integer values in a 10 × 15 array and then displays the indexes of the positions that contain odd numbers.

10. Write a PHP script that lets the user enter numeric values in a 10 × 6 array and then displays the elements of the columns with even-numbered indexes (that is, column indexes 0, 2, and 4).

11. Write a PHP script that lets the user enter numeric values in a 12 × 8 array and then calculates and displays the sum of the elements that have even column indexes and odd row indexes.

12. Write a PHP script that lets the user enter numeric values in an 8 × 8 square array and then calculates the average value of the elements of its main diagonal and the average value of the elements of its antidiagonal. Try to calculate both average values within the same loop control structure.

13. Write a PHP script that creates and displays the following array.

$a =

|   | 0 | 1 | 2 | 3 | 4 |
|---|---|---|---|---|---|
| 0 | 11 | 11 | 11 | 11 | 5 |
| 1 | 11 | 11 | 11 | 5 | 88 |
| 2 | 11 | 11 | 5 | 88 | 88 |
| 3 | 11 | 5 | 88 | 88 | 88 |
| 4 | 5 | 88 | 88 | 88 | 88 |

# Two-Dimensional Arrays

14. Write a PHP script that creates and displays the following array.

$a =

|   | 0 | 1 | 2 | 3 | 4 |
|---|---|---|---|---|---|
| 0 | 0 | 11 | 11 | 11 | 5 |
| 1 | 11 | 0 | 11 | 5 | 88 |
| 2 | 11 | 11 | 0 | 88 | 88 |
| 3 | 11 | 5 | 88 | 0 | 88 |
| 4 | 5 | 88 | 88 | 88 | 0 |

15. Write a PHP script that lets the user enter numeric values in a 5 × 4 array and then displays the row and column indexes of the positions that contain integers.

16. Write a PHP script that lets the user enter numeric values in a 10 × 4 array and then counts and displays the total number of negative elements.

17. Write a PHP script that lets the user enter words in a 3 × 4 array and then displays them with a space character between them.

18. Write a PHP script that lets the user enter words in a 20 × 14 array and then displays those who have less than five characters.

Hint: Use the `strlen()` function.

19. Write a PHP script that lets the user enter words in a 20 × 14 array and displays those that have less than five characters, then those that have less than 10 characters, and finally those that have less than 20 characters. Assume that the user enters only words with less than 20 characters.

Hint: Try to display the words using three counted loop structures nested one within the other.

# 35.1 Introduction

Since arrays are handled with the same sequence, decision, and loop control structures that you learned about in previous chapters, there is no need to repeat all of that information here. However, what you will discover in this chapter is how to process each row or column of a two-dimensional array individually, how to solve problems that require the use of more than one array, and how to create a two-dimensional array from a one-dimensional array and vice versa.

# 35.2 Processing Each Row Individually

Processing each row individually means that every row is processed separately and the result of each row (which can be the sum, the average value, and so on) can be used individually for further processing. Suppose you have the following 4 × 5 array.

![](img/4d9a992abc5da7946ac44f9e6bf1d032_632_0.png)

Let’s try to find the sum of each row individually. There are actually two approaches that you can use. Both of these approaches iterate through rows.

# First Approach – Creating an auxiliary array

In this approach, the script processes each row individually and creates an auxiliary array in which each position stores the sum of one row. This approach gives you much flexibility since you can use this new array later in your script for further processing. The auxiliary array is shown on the right.

![](img/4d9a992abc5da7946ac44f9e6bf1d032_632_1.png)

Now, let’s write the corresponding code fragment. To more easily understand the process, the “from inner to outer” method is used. The following code fragment calculates the sum of the first row (row index 0) and stores the result in position 0 of the auxiliary array. Assume variable `$i` contains the value 0.

```php
$s = 0;
for ($j = 0; $j <= COLUMNS - 1; $j++) {
    $s += $a[$i][$j];
}
$sum[$i] = $s;
```

This script can equivalently be written as

```php
$sum[$i] = 0;
for ($j = 0; $j <= COLUMNS - 1; $j++) {
    $sum[$i] += $a[$i][$j];
}
```

Now, nesting this code fragment in a counted loop structure that iterates for all rows results in the following.

```php
$sum = array();
for ($i = 0; $i <= ROWS - 1; $i++) {
    $sum[$i] = 0;
    for ($j = 0; $j <= COLUMNS - 1; $j++) {
        $sum[$i] += $a[$i][$j];
    }
}
```

# Second Approach – Just find it and process it!

This approach uses no auxiliary array; it just calculates and directly processes the sum. The code fragment is as follows.

```php
for ($i = 0; $i <= ROWS - 1; $i++) {
    $sum = 0;
    for ($j = 0; $j <= COLUMNS - 1; $j++) {
        $sum += $a[$i][$j];
    }
    process $sum;
}
```

What does process $sum mean? It depends on the given problem. It may just display the sum, it may calculate the average value of each individual row and display it, or it may use the sum for calculating even more complex mathematical expressions.

For instance, the following example calculates and displays the average value of each row.

```php
for ($i = 0; $i <= ROWS - 1; $i++) {
    $sum = 0;
    for ($j = 0; $j <= COLUMNS - 1; $j++) {
        $sum += $a[$i][$j];
    }
```

# # Exercise 35.2-1 Finding the Average Value

There are 20 students and each one of them has received his or her grades for 10 lessons. Write a PHP script that prompts the user to enter the grades of each student for all lessons and then calculates and displays, for each student, all average values that are greater than 89.

# # Solution

Since you’ve learned two approaches for processing each row individually, let’s use them both.

# # First Approach – Creating an auxiliary array

In this approach, the script processes each row individually and creates an auxiliary array in which each position stores the average value of one row. The two required arrays are shown next.

After the array $average is created, the script can find and display all average values that are greater than 89. The PHP script is as follows.

# # file_35.2-1a.php

```php
<?php
define("STUDENTS", 20);
define("LESSONS", 10);

$grades = array(array());
for ($i = 0; $i <= STUDENTS - 1; $i++) {
echo "For student No. ", $i + 1, "...\n";
```

![](img/4d9a992abc5da7946ac44f9e6bf1d032_634_0.png)

```php
$average = $sum / COLUMNS;
echo $average;
}
```
