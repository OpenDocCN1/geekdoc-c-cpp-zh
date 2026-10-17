and the post-test loop structure is

```
```php
<?php

$x = 10;

$i = -4;
if ($i <= 4) {
    do {
        $x = pow($x, 2);
        $i++;
    } while ($i <= 4);
}

echo $x;

?>
```
```

In this case, since variable `$i` does not depend on user input (it is assigned the constant value -4), the decision structure is redundant and can be omitted.

```
```php
<?php

$x = 10;

$i = -4;
do {
    $x = pow($x, 2);
    $i++;
} while ($i <= 4);

echo $x;

?>
```
```

# 29.12  Converting from a Post-Test Loop Structure to a Counted Loop Structure

This conversion doesn’t have its own rules but you can use the rules you have already learned, that is, you can convert from a post-test loop structure to an intermediate pre-test loop structure, and finally to a counted loop structure, as shown in next diagram.

![](bbox=[0.077, 0.887, 0.944, 0.98])