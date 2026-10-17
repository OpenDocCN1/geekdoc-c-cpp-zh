
# Exercise 37.1-4 Merging Two-Dimensional Arrays

Write a PHP script that lets the user enter numerical values into arrays $a and $b of 10 × 20 and 30 × 20 elements respectively. Then, the script should create a new array $new of 40 × 20 elements. In this new array, the first 10 rows should contain the elements of array $a and the next 30 rows should contain the elements of array $b.

# Solution

This exercise can be solved pretty much the same way as the previous one. Below you can find the proposed solution. The approach of iterating through rows has been chosen, but iterating through columns could have been used as well.

# file_37.1-4.php

```php
<?php
define("COLUMNS", 20);
define("ROWS_OF_A", 10);
define("ROWS_OF_B", 30);
define("ROWS_OF_NEW", ROWS_OF_A + ROWS_OF_B);

//Read array $a
$a = array(array());
for ($i = 0; $i <= ROWS_OF_A - 1; $i++) {
    for ($j = 0; $j <= COLUMNS - 1; $j++) {
        $a[$i][$j] = trim(fgets(STDIN));
    }
}

//Read array $b
$b = array(array());
for ($i = 0; $i <= ROWS_OF_B - 1; $i++) {
    for ($j = 0; $j <= COLUMNS - 1; $j++) {
        $b[$i][$j] = trim(fgets(STDIN));
    }
}
```

# Chapter 37
More Exercises with Arrays

In this exercise, there is no one-to-one match between the index positions of the elements of array `$a` and the arrays `$pos` and `$neg`. For example, the element from position 1 of array `$a` is not stored in position 1 of array `$neg`, the element from position 2 of array `$a` is not stored in position 2 of array `$pos`, and so on. Thus, you cannot do the following,

```php
for ($i = 0; $i <= ELEMENTS - 1; $i++) {
    if ($a[$i] > 0) {
        $pos[$i] = $a[$i];
    }
    elseif ($a[$i] < 0) {
        $neg[$i] = $a[$i];
    }
}
```

because it will result in the following two arrays.

What you need here are two independent index variables: `$pos_index` for the array `$pos`, and `$neg_index` for the array `$neg`. These index variables must be incremented independently, and only when an element is added to the corresponding array. The index variable `$pos_index` must be incremented only when an element is added to the array `$pos`, and the index variable `$neg_index` must be incremented only when an element is added to the array `$neg`.

```php
$pos_index = 0;
$neg_index = 0;
for ($i = 0; $i <= ELEMENTS - 1; $i++) {
    if ($a[$i] > 0) {
        $pos[$pos_index] = $a[$i];
        $pos_index++;
    }
    elseif ($a[$i] < 0) {
        $neg[$neg_index] = $a[$i];
        $neg_index++;
    }
}
```

When this loop finishes iterating, the two arrays become as follows.

| $pos | 5 | 10 | 9 | 12 | ... | 2 |
|---|---:|---:|---:|---:|---:|---:|
| $neg | -11 | -25 | -4 | ... | -22 |

> **Notice:** Please note that variables `$pos_index` and `$neg_index` have dual roles. When the loop iterates, each points to the next position in which a new element should be placed. When the loop finishes iterating, variables `$pos_index` and `$neg_index` actually contain the total number of elements in each corresponding array!

The complete solution is presented next.

```php
<?php
define("ELEMENTS", 100);

$a = array();
for ($i = 0; $i <= ELEMENTS - 1; $i++) {
    $a[$i] = trim(fgets(STDIN));
}

//Create arrays $pos and $neg
$pos = array();
$neg = array();
$pos_index = 0;
$neg_index = 0;
for ($i = 0; $i <= ELEMENTS - 1; $i++) {
    if ($a[$i] > 0) {
        $pos[$pos_index] = $a[$i];
        $pos_index++;
    }
    elseif ($a[$i] < 0) {
        $neg[$neg_index] = $a[$i];
        $neg_index++;
    }
}

for ($i = 0; $i <= $pos_index - 1; $i++) {
    echo $pos[$i], "\t";
}
echo "\n";
for ($i = 0; $i <= $neg_index - 1; $i++) {
    echo $neg[$i], "\t";
}
?>
```

> **Notice:** Please note that the arrays `$pos` and `$neg` contain a total number of `$pos_index` and `$neg_index` elements respectively. This is why the two last loop control structures iterate until variable `$i` reaches values `$pos_index - 1` and `$neg_index - 1`, respectively, and not until `ELEMENTS - 1`, as you may mistakenly expect. Obviously the sum of `$pos_index + $neg_index` equals to `ELEMENTS`.

Now, let’s design the corresponding flowchart fragment only for that part of the script that creates the arrays `$pos` and `$neg`. As you may notice, there is a multiple-alternative decision structure nested within a counted loop structure. The flowchart fragment is as follows.

# Exercise 37.1-6 Creating an Array with Those who Contain Digit 5

Write a PHP script that lets the user enter 100 two-digit integers into an array and then creates a new array of only the integers that contain at least one of the digit 5.

# Solution

This exercise requires some knowledge from the past. In Chapter 13 you learned how to use the quotient and the remainder to split an integer into its individual digits. Here, the integer has two digits; therefore, you can use the following flowchart fragment to split any two-digit integer contained in variable *x*.

The final flowchart is as follows.

The corresponding PHP script is as follows.

```php
<?php
define("ELEMENTS", 100);

$a = array();
for ($i = 0; $i <= ELEMENTS - 1; $i++) {
    $a[$i] = trim(fgets(STDIN));
}

$b = array();
$k = 0;
for ($i = 0; $i <= ELEMENTS - 1; $i++) {
    $last_digit = $a[$i] % 10;
    $first_digit = intval($a[$i] / 10);

    if ($last_digit == 5 || $first_digit == 5) {
        $b[$k] = $a[$i];
        $k++;
    }
}

for ($i = 0; $i <= $k - 1; $i++) {
    echo $b[$i], "\t";
}
?>
```

> **Remember!** When you need to create a new array using values from an old array and there is no one-to-one match between their index positions, you need an extra variable that becomes the index for the new array. Of course, this variable should increase by 1 only when a new element is added into the new array. Moreover, when the loop that creates the new array finishes iterating, the value of this variable matches the total number of elements in the new array!

# 37.2 Data Validation with Arrays

As you already know, data validation is the process of restricting data input, which forces the user to enter only valid values. As you have already been taught in Chapter 31, there are three approaches that you can use depending on whether or not you wish to display an error message and whether you wish to display individual error messages for each error or just a single error message for any kind of error. Let’s see how those three approaches can be adapted and used with arrays.

```php
while($input_array[$i] test 1 fails || $input_array[$i] test 2 fails || …) {
    echo "Error message \n";
    echo "Prompt message";
    $input_array[$i] = trim(fgets(STDIN));
}
```

# Third Approach – Validating data input with individual error messages

Once again, the next code fragment is taken from Chapter 31 and adapted to operate with an array. It validates data input and displays an error message (that is, individual error messages, one for each type of input error).

```php
for ($i = 0; $i <= ELEMENTS - 1; $i++) {
    do {
        echo "Prompt message";
        $input_array[$i] = trim(fgets(STDIN));
        $failure = false;
        if ($input_array[$i] test 1 fails) {
            echo "Error message 1 \n";
            $failure = true;
        }
        elseif ($input_array[$i] test 2 fails) {
            echo "Error message 2 \n";
            $failure = true;
        }
        elseif (…
            …
        }
    } while ($failure == true);
}
```

# Exercise 37.2-1 Displaying Odds in Reverse Order – Validation Without Error Messages

Write a PHP script that prompts the user to enter 20 odd integers into an array and then displays them in reverse order. The script should also validate data input, allowing the user to enter only odd integers. There is no need to display any error messages.

# Solution

As the wording of the exercise implies, not all entered values should be added in the array—only the odd ones. The PHP script is as follows.
