```
```php
$k = 0;
for ($i = 100; $i >= -100; $i -= 5) {
    $k = $k + $i;
}
echo $i;
```
```

the value displayed is

+   a. -95.
+   
+   b. -100.
+   
+   c. -105.
+   
+   d. none of the above

# 27.5 Review Exercises

Complete the following exercises.

+   1. Create a trace table to determine the values of the variables in each step of the next PHP script. How many iterations does this PHP script perform?

```
```php
<?php
$a = 0;
$b = 0;
for ($j = 0; $j <= 8; $j += 2) {
    if ($j < 5) {
        $b++;
    }
    else {
        $a += $j - 1;
    }
}
echo $a, $b;
?>
```
```

+   2. Create a trace table to determine the values of the variables in each step of the next PHP script for two different executions.

The input values for the two executions are: (i) 10, and (ii) 21.

```
```php
<?php
$a = trim(fgets(STDIN));
$b = $a;
for ($j = $a - 5; $j <= $a; $j += 2) {
    if ($j % 2 != 0) {
        $b = $a + $j + 5;
    }
    else {
        $b = $a - $j;
    }
```
```