# # Post-Test Loop Structure

```
```php
if (Boolean_Expression) {
    do {
        A statement or block of statements
    } while (Boolean_Expression);
}
```
```

# ## Exercise 29.10-1 Converting the PHP Script

Rewrite the following PHP script using the post-test loop structure.

```
```php
<?php
$a = trim(fgets(STDIN));
$b = trim(fgets(STDIN));

while ($b <= $a) {
    $a *= 2;
    $b = $b * 3;
}

echo $a, $b;
?>
```
```

# ## Solution

Following the conversion rule, the PHP script using the post-test loop structure becomes

```
```php
<?php
$a = trim(fgets(STDIN));
$b = trim(fgets(STDIN));

if ($b <= $a) {
    do {
        $a *= 2;
        $b = $b * 3;
    } while ($b <= $a);
}

echo $a, $b;
?>
```
```