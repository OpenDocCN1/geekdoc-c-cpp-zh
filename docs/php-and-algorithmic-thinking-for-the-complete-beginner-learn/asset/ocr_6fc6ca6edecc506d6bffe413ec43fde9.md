+   - For N = 1, M = 2 the criteria equals to |1/2 − 0.333| = 0.1670
+   - For N = 1, M = 3 the criteria equals to |1/3 − 0.333| = 0.0003
+   - For N = 1, M = 4 the criteria equals to |1/4 − 0.333| = 0.0830
+   - ...
+   - For N = 100, M = 99 the criteria equals to |100/99 − 0.333| = 0.6771
+   - For N = 100, M = 100 the criteria equals to |100/100 − 0.333| = 0.6670

As you can see, the value 0.0003 is the minimum value among all possible results. Thus, the combination N = 1 and M = 3 (which corresponds to the fraction 1/3) is considered the best approximation for the value 0.333.

And now the PHP script:

```
```php
<?php
do {
    echo "Enter a real between 0 and 100: ";
    $x = trim(fgets(STDIN));
} while (is_numeric($x) != true || $x < 0 || $x > 100);

$best_n = 1;
$best_m = 1;
for ($n = 0; $n <= 100; $n++) {
    for ($m = 1; $m <= 100; $m++) {
        if (abs($n / $m - $x) < abs($best_n / $best_m - $x)) {
            $best_n = $n;
            $best_m = $m;
        }
    }
}

echo "The corresponding fraction is: ", $best_n, "/", $best_m;
?>
```
```

# 31.5 Finding Minimum and Maximum Values with Loop Control Structures

In Chapter 23 you learned how to find the minimum and maximum values among four values using single-alternative decision structures. Now, the following code fragment does pretty much the same but uses only one variable $w to hold all of the user’s given values.