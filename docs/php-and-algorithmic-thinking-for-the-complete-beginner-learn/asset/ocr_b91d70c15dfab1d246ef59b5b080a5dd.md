# # Exercise 31.4-5 Is the Number a Prime?

```
```php
<?php
echo "Enter an integer greater than 1: ";
$x = trim(fgets(STDIN));

$number_of_divisors = 2;
for ($i = 2; $i <= intval($x / 2); $i++) {
    if ($x % $i == 0) {
        $number_of_divisors++;
```
```