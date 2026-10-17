```
```php
$min[$j] = $a[$i][$j];
}
if ($a[$i][$j] > $max[$j]) {
    $max[$j] = $a[$i][$j];
}
}
```
```

> **Notice:** Please note that the initial value of variable `$i` is 1. It wouldn’t be wrong to start iterating from row index 0 instead of 1, though the script would perform one useless iteration.

To process the whole array `$a`, you can just nest this code fragment into a counted loop structure that iterates for all columns as follows.

```
```php
for ($j = 0; $j <= COLUMNS - 1; $j++) {
    $min[$j] = $a[0][$j];
    $max[$j] = $a[0][$j];
    for ($i = 1; $i <= ROWS - 1; $i++) {
        if ($a[$i][$j] < $min[$j]) {
            $min[$j] = $a[$i][$j];
        }
        if ($a[$i][$j] > $max[$j]) {
            $max[$j] = $a[$i][$j];
        }
    }
}
```
```

> **Notice:** Finding the minimum and maximum values of each column is as easy as finding the minimum and the maximum value of each row, as you learned in the previous exercise. Please note that the two counted loop structures of `$i` and `$j` have switched places.

The final PHP script is as follows.

```
```php
<?php
define("ROWS", 30);
define("COLUMNS", 20);

$a = array(array());
for ($i = 0; $i <= ROWS - 1; $i++) {
    for ($j = 0; $j <= COLUMNS - 1; $j++) {
        $a[$i][$j] = trim(fgets(STDIN));
    }
}
```
```