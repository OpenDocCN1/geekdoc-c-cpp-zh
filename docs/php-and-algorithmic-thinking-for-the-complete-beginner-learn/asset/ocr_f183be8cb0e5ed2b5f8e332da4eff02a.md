# Chapter 26
The Post-Test Loop Structure

# ## 26.4 Review Exercises

Complete the following exercises.

+   1. Identify the syntax error(s) in the following PHP script.

```
```php
<?php
    $i = 3;
do
    $i--;
} while ($i > 0)
echo "The end";
?>
```
```

+   2. Create a trace table to determine the values of the variables in each step of the next PHP script. How many iterations does this PHP script perform?

```
```php
<?php
    $y = 5;
    $x = 38;

do {
    $y *= 2;
    $x++;
    echo $y;
} while ($y < $x);
?>
```
```

+   3. Create a trace table to determine the values of the variables in each step of the next PHP script. How many iterations does this PHP script perform?

```
```php
<?php
    $x = 1;

do {
    if ($x % 2 == 0) {
        $x++;
    }
    else {
        $x += 3;
    }
    echo $x;
} while ($x < 12);
?>
```
```

+   4. Create a trace table to determine the values of the variables in each step of the next PHP script. How many iterations does this PHP script perform?

```
```php
<?php
    $y = 2;
```
```