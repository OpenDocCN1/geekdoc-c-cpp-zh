# 40.6 Review Exercises

Complete the following exercises.

+   1. Create a trace table to determine the values of the variables in each step of the following PHP script when the values 3, 7, 9, 2, and 4 are entered.

```
```php
<?php

function display($a) {
    if ($a % 2 == 0) {
        echo $a, " is even";
    }
    else {
        echo $a, " is odd";
    }
}

for ($i = 1; $i <= 5; $i++) {
    $x = trim(fgets(STDIN));
    display($x);
}
?>
```
```

+   2. Create a trace table to determine the values of the variables in each step of the following PHP script.

```
```php
<?php

function division($a, $b) {
    $b = intval($b / $a);
    echo $a * $b, "\n";
}

$x = 20;
$y = 30;
while ($x % $y < 30) {
    division($y, $x);
    $x = 4 * $y;
    $y++;
}
?>
```
```