# Chapter 23
More Exercises with Decision Control Structures

> **Notice:** The path on the right (a = 0) is the solution to the linear equation bx + c = 0, which was shown in the previous exercise.

Using this diagram you can design the following flowchart.

![](bbox=[0.009, 0.166, 0.987, 0.652])

The PHP script is shown here.

```
```php
<?php
    echo "Enter values for coefficients a, b and c: ";
    $a = trim(fgets(STDIN));
    $b = trim(fgets(STDIN));
    $c = trim(fgets(STDIN));

    if ($a != 0) {
        $D = $b * $b - 4 * $a * $c;
        if ($D >= 0) {
            if ($D > 0) {
                $x1 = (-$b + sqrt($D)) / (2 * $a);
```
```