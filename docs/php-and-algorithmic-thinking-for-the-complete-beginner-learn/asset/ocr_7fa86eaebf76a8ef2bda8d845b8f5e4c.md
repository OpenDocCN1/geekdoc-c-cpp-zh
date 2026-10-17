Two properties are not satisfied by this algorithm. The first one is obvious: there is no data input. The second one is the property of definiteness. You should never refer to a non-existing element of an array and, in this exercise, there is no element at index position 100.

# 33.3 How to Add Values Entered by the User to a One-Dimensional Array

There is nothing new here. Instead of reading a value from the keyboard and assigning that value to a variable, you can directly assign that value to a specific position of an array. The next code fragment lets the user enter three values, and then adds these values to positions 0, 1, and 2 of the array `$test`.

```
```php
$test = array();
$test[0] = trim(fgets(STDIN));
$test[1] = trim(fgets(STDIN));
$test[2] = trim(fgets(STDIN));
```
```

# 33.4 How to Iterate Through a One-Dimensional Array

Now comes the interesting part. A script can iterate through the elements of an array using a loop control structure (usually a counted loop structure) in which the counter variable is used as the index to the array. Following is a code fragment, written in general form

```
```php
for ($i = 0; $i <= size_of_the_array - 1; $i++) {
    process array_name[$i];
}
```
```

in which *size_of_the_array* is the number of elements the array contains, and *process* is any PHP statement or block of statements that processes one element of the array at each iteration.

> **Notice:** The name of the variable `$i` is not binding. You can use any variable name you wish, such as `$index`, `$ind`, `$j`, and many more.

The following PHP script,

```
```php
<?php
$grades = array("B+", "A+", "A", "C-");
for ($i = 0; $i <= 3; $i++) {
    process $grades[$i];
}
?>
```
```

“processes” all elements of the array `$grades`, one at each iteration.