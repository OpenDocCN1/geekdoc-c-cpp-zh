# Chapter 23
More Exercises with Decision Control Structures

![](bbox=[0.018, 0.064, 0.344, 0.849])

```
```php
<?php
echo "Enter the weight of four men:";

$w1 = trim(fgets(STDIN));
$w2 = trim(fgets(STDIN));
$w3 = trim(fgets(STDIN));
$w4 = trim(fgets(STDIN));

//memorize the weight of the first person
$min = $w1;

//if second one is lighter, forget
everything and memorize this weight
if ($w2 < $min) {
    $min = $w2;
}

//if third one is lighter, forget
everything and memorize this weight
if ($w3 < $min) {
    $min = $w3;
}

//if fourth one is lighter, forget
everything and memorize this weight
if ($w4 < $min) {
    $min = $w4;
}

echo $min;

?>
```
```

> **Notice:** You can find the maximum instead of the minimum value by simply replacing the “less than” with a “greater than” operator in all Boolean expressions.