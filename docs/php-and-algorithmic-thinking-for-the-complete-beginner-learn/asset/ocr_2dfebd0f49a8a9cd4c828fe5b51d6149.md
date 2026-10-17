```
function f2($number1, $number2) {
    return f1($number1) + f1($number2);
}

$a = 3;
$b = 4;

echo f2($a, $b);
?>
```

# 3. Without using a trace table, can you find out what the next PHP script displays?

```
<?php
function f1($number1) {
    $number1 *= 2;
}

function f2($number1, $number2) {
    f1($number1);
    f1($number2);
    return $number1 + $number2;
}

$a = 2;
$b = 5;

echo f2($a, $b);
?>
```

# 4. Create a trace table to determine the values of the variables in each step of the following PHP script when the value 12 is entered.

```
<?php
function swap(&$x, &$y) {
    $temp = $x;
    $x = $y;
    $y = $temp;
}

$k = trim(fgets(STDIN));
$m = 1;
$a = 1;
while ($a < 8) {
```