+1, you can start counting from 1 and use an _offset_ of +2. This modification decreases the number of iterations by half. The modified PHP script follows.

```
<?php
    define("ELEMENTS", 100);
    $values = array();
    for ($i = 0; $i <= ELEMENTS - 1; $i++) {
        $values[$i] = trim(fgets(STDIN));
    }
    for ($i = 1; $i <= ELEMENTS - 1; $i += 2) {
        if ($values[$i] % 2 == 0) {
            echo $values[$i];
        }
    }
?>
```

# Exercise 33.4-4 Finding the Sum

Write a PHP script that lets the user enter 50 numbers into an array and then calculates and displays their sum.

# Solution

The solution is as follows:

```
<?php
    define("ELEMENTS", 50);
    $values = array();
    for ($i = 0; $i <= ELEMENTS - 1; $i++) {
        $values[$i] = trim(fgets(STDIN));
    }
    $sum = 0;
    for ($i = 0; $i <= ELEMENTS - 1; $i++) {
        $sum = $sum + $values[$i];
    }
echo $sum;
```