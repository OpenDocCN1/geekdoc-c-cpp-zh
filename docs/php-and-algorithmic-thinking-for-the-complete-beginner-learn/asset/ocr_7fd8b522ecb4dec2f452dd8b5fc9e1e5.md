goals each player scored. The script should then display the name of each team along with its five best scorers. Use the modified bubble sort algorithm.

# Solution

In this exercise you need the following three arrays.

![](bbox=[0.018, 0.18, 0.974, 0.413])

> **Notice:** To save paper short array names are used, but it is more or less obvious that array `$t` holds the names of the 32 national teams, array `$p` holds the names of the 24 players of each team, and array `$g` holds the total number of goals each player scored.

Since you need to find the five best scorers for each team, the PHP script must sort each row of array `$g` in descending order but it should also take care to preserve the relationship with the elements of arrays `$p`. This means that, every time the bubble sort algorithm swaps the contents of two elements of array `$g`, the corresponding elements of array `$p` should be swapped as well. When sorting is completed, the five best scorers should appear in the first five columns.

The “from inner to outer” method is used again. The following code fragment sorts the first row (row index 0) of array `$g` in descending order and, at the same time, takes care to preserve the relationship with elements of array `$p`. Assume variable `$i` contains the value 0.

```
```php
$m = 1;
$swaps = true;
while (($m <= PLAYERS - 1) && ($swaps == true)) {
    $swaps = false;
    for ($n = PLAYERS - 1; $n >= $m; $n--) {
        if ($g[$i][$n] < $g[$i][$n - 1]) {
            $temp = $g[$i][$n];
            $g[$i][$n] = $g[$i][$n - 1];
            $g[$i][$n - 1] = $temp;
        }
    }
}
```
```