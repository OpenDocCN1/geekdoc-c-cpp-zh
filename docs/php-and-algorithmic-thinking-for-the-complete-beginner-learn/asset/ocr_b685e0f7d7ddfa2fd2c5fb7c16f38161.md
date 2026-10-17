# Exercise 31.3-1 *Finding the Square Root - Validation Without Error Messages*

Write a PHP script that prompts the user to enter a numeric value and then calculates its square root. Moreover, the script should validate data input, allowing the user to enter only *non-negative*¹ numeric values. There is no need to display any error messages.

# Solution

First, let’s write the script without data validation.

```
```php
<?php
echo "Enter a number: ";
$x = trim(fgets(STDIN));

$y = sqrt($x);
echo $y;
?>
```
```

![](bbox=[0.405, 0.626, 0.938, 0.675])

To validate data input without displaying any error messages you can use the first approach. All you need to do is replace the statements marked with a dashed rectangle with the following code fragment.

```
```php
do {
    echo "Enter a non-negative number: ";
    $x = trim(fgets(STDIN));
} while (is_numeric($x) != true || $x < 0);
```
```

> ¹ A quantity that is either zero or positive.