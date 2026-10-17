beginning, gives you the opportunity to remove the statement (echo $y) outside of all paths and move it at the end of them. The modified PHP script is shown here.

```
```php
<?php
echo "Enter a value for x: ";
$x = trim(fgets(STDIN));

if ($x == -1 || $x == 9) {
    echo "Invalid value";
}
else {
    if ($x > -5 && $x <= 0) {
        $y = $x / ($x - 3) + (8 + $x) / ($x + 1);
    }
    elseif ($x > 0 && $x <= 6) {
        $y = 40 * $x / ($x - 8);
    }
    elseif ($x > 6 && $x <= 20) {
        $y = 3 * $x / ($x - 9);
    }
    else {
        $y = abs($x);
    }
    echo $y;
}
?>
```
```

Now, if you are speculating about whether the Boolean expressions in bold are redundant, the answer is “no” again. Suppose you do remove them and the user enters a value of −20 for x. The flow of execution then reaches the Boolean expression $x \leq 0$, which evaluates to true. Then the fraction $\frac{x}{x-3}+\frac{8+x}{x+1}$, instead of the absolute value of x, is calculated.

Yet still there is hope! Next, you can find a proposed solution in which unnecessary Boolean expressions are actually removed. The trick here is that the case of the absolute value of x is examined first.

```
```php
<?php
echo "Enter a value for x: ";
$x = trim(fgets(STDIN));

if ($x == -1 || $x == 9) {
```
```