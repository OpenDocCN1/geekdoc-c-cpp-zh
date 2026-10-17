```
```php
echo "1: Gallons to liters\n";
echo "2: Liters to gallons\n";
echo "Enter choice: ";
$choice = trim(fgets(STDIN));

echo "Enter quantity: ";
$quantity = trim(fgets(STDIN));

if ($choice < 1 || $choice > 2) {
    echo "Wrong choice!";
}
elseif (is_numeric($quantity) != true) {
    echo "Invalid quantity!";
}
else {
    if ($choice == 1) {
        $result = $quantity * COEFFICIENT;
        echo $quantity, " gallons equal to ", $result, " liters";
    }
    else {
        $result = $quantity / COEFFICIENT;
        echo $quantity, " liters equal to ", $result, " gallons";
    }
}
?>
```
```

# Exercise 23.1-6  *Where is the Tollkeeper?*

In a toll gate, there is an automatic system that recognizes whether the passing vehicle is a motorcycle, a car, or a truck. Write a PHP script that lets the user enter the type of the vehicle (M for motorcycle, C for car, and T for truck) and then displays the corresponding amount of money the driver must pay according to the following table.

| Vehicle Type | Amount to Pay |
|---|---|
| Motorcycle | $1 |
| Car | $2 |
| Track | $4 |