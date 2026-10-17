The corresponding PHP script is as follows.

```
```php
<?php
define("ELEMENTS", 100);

$a = array();
for ($i = 0; $i <= ELEMENTS - 1; $i++) {
    $a[$i] = trim(fgets(STDIN));
}

$b = array();
$k = 0;
for ($i = 0; $i <= ELEMENTS - 1; $i++) {
    $last_digit = $a[$i] % 10;
    $first_digit = intval($a[$i] / 10);

    if ($last_digit == 5 || $first_digit == 5) {
        $b[$k] = $a[$i];
        $k++;
    }
}

for ($i = 0; $i <= $k - 1; $i++) {
    echo $b[$i], "\t";
}
?>
```
```

> **Remember!** When you need to create a new array using values from an old array and there is no one-to-one match between their index positions, you need an extra variable that becomes the index for the new array. Of course, this variable should increase by 1 only when a new element is added into the new array. Moreover, when the loop that creates the new array finishes iterating, the value of this variable matches the total number of elements in the new array!

# 37.2  Data Validation with Arrays

As you already know, data validation is the process of restricting data input, which forces the user to enter only valid values. As you have already been taught in Chapter 31, there are three approaches that you can use depending on whether or not you wish to display an error message and whether you wish to display individual error messages for each error or just a single error message for any kind of error. Let’s see how those three approaches can be adapted and used with arrays.