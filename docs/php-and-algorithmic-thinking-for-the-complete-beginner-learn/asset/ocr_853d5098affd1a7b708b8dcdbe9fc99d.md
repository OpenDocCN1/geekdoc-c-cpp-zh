```
```php
$x = 5;

$i = $start;
if ($i <= $end) {
    do {
        $x = pow($x, 1.5);
        $i++;
    } while ($i <= $end);
}
echo $x;
?>
```
```

# ## Exercise 29.11-2 Converting the PHP Script

Rewrite the following PHP script using the post-test loop structure.

```
```php
<?php
$x = 10;

for ($i = -4; $i <= 4; $i++) {
    $x = pow($x, 2);
}
echo $x;
?>
```
```

# ## Solution

The intermediate pre-test loop structure is as follows.

```
```php
<?php
$x = 10;

$i = -4;
while ($i <= 4) {
    $x = pow($x, 2);
    $i++;
}
echo $x;
?>
```
```