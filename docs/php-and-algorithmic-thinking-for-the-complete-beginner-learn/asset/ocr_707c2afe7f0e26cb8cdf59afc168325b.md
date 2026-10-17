```
```php
echo "Invalid value";
}
else {
    if ($x <= -5 || $x > 20) {
        $y = abs($x);
    }
    elseif ($x <= 0) {
        $y = $x / ($x - 3) + (8 + $x) / ($x + 1);
    }
    elseif ($x <= 6) {
        $y = 40 * $x / ($x - 8);
    }
    else {
        $y = 3 * $x / ($x - 9);
    }
    echo $y;
}
?>
```
```

> **Notice:** It is obvious that one problem can have many solutions. It is up to you to find the optimal one!

# Exercise 23.4-5    *Progressive Rates and Electricity Consumption*

The LAV Electricity Company charges subscribers for their electricity consumption according to the following table (monthly rates for domestic accounts). Assume that all extra charges such as transmission service charges and distribution charges are all included. Please note that the rates are progressive.

| Kilowatt-hours (kWh) | USD per kWh |
|---|---|
| kWh ≤ 500 | $0.10 |
| 501 ≤ kWh ≤ 2000 | $0.25 |
| 2001 ≤ kWh ≤ 4000 | $0.40 |
| 4001 < kWh | $0.60 |

Write a PHP script that prompts the user to enter the total number of kWh consumed and then calculates and displays the total amount to pay.

# Solution

The term “progressive rates” means that when a customer consumes, for example, 2200 kWh, not all of the kilowatt-hours are charged at $0.40. The first 500 kWh are