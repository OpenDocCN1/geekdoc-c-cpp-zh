# Exercise 10.1-2 Calculating the Area of a Circle

Write a PHP script that calculates and displays the area of a circle.

# Solution

The area of a circle can be calculated using the following formula:

Area = π · Radius²

The value of π is a known quantity, which is 3.14159. Therefore, the only value the user has to enter is a value for Radius. The solution to this problem is shown here.

```
file_10.1-2a.php
<?php
echo "Enter the length of Radius: ";
$radius = trim(fgets(STDIN));

$area = 3.14159 * $radius * $radius;

echo "The area of the circle is ", $area;
?>
```

A much better approach would be with to use a constant, PI.

```
file_10.1-2b.php
<?php
define("PI", 3.14159);

echo "Enter the length of Radius: ";
$radius = trim(fgets(STDIN));
$area = PI * $radius * $radius;
echo "The area of the circle is ", $area;
?>
```

# Exercise 10.1-3 Calculating Fuel Economy

In the United States, a car's fuel economy is measured in miles per gallon, or MPG. A car's MPG can be calculated using the following formula:

MPG = miles driven / gallons of gas used

Write a PHP script that prompts the user to enter the total number of miles he or she has driven and the gallons of gas used. Then the script should calculate and display the car's MPG.

# Solution