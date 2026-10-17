```
}
else {
    echo $x, " is real";
}
}
else {
    echo "Invalid Number";
}
?>
```

# Exercise 23.1-4    Converting Gallons to Liters, and Vice Versa

Write a PHP script that displays the following menu:

+   1. Convert gallons to liters
+   2. Convert liters to gallons

The script prompts the user to enter a choice (1 or 2) and a quantity. Then, it calculates and displays the required value. It is given that

1 gallon = 3.785 liters

# Solution

The PHP script is shown here.

```
file_23.1-4.php
<?php
define("COEFFICIENT", 3.785);

echo "1: Gallons to liters\n";
echo "2: Liters to gallons\n";
echo "Enter choice: ";
$choice = trim(fgets(STDIN));

echo "Enter quantity: ";
$quantity = trim(fgets(STDIN));

if ($choice == 1) {
    $result = $quantity * COEFFICIENT;
    echo $quantity, " gallons equal to ", $result, " liters";
}
else {
    $result = $quantity / COEFFICIENT;
    echo $quantity, " liters equal to ", $result, " gallons";
```