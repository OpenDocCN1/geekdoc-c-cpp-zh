# Two-Dimensional Arrays

![](bbox=[0.086, 0.082, 0.348, 0.207])

![](bbox=[0.53, 0.082, 0.916, 0.267])

> **Notice:** Please note that the elements of the main diagonal have their row index equal to their column index.

You can calculate the sum of the elements of the main diagonal using two different approaches. Let’s study them both.

# First Approach – Iterating through all elements

In this approach, the script iterates through rows, or even through columns, and checks if the row index is equal to the column index. For square arrays, represented as N × N, the number of rows and columns is equal, so you can define just one constant, N. The solution is as follows.

```
```php
<?php

define("N", 10);

$a = array(array());
for ($i = 0; $i <= N - 1; $i++) {
    for ($j = 0; $j <= N - 1; $j++) {
        $a[$i][$j] = trim(fgets(STDIN));
    }
}

//Calculate Sum
$sum = 0;
for ($i = 0; $i <= N - 1; $i++) {
    for ($j = 0; $j <= N - 1; $j++) {
        if ($i == $j) {
            $sum = $sum + $a[$i][$j];
        }
    }
}
```
```