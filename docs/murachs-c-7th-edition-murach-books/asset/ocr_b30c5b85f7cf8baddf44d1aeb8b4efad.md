# Five static methods of the Math class

# The syntax of the Round() method

```
Math.Round(decimalNumber[, precision[, mode]])
```

# The syntax of the Pow() method

```
Math.Pow(number, power)
```

# The syntax of the Sqrt() method

```
Math.Sqrt(number)
```

# The syntax of the Min() and Max() methods

```
Math.{Min|Max}(number1, number2)
```

# Statements that use static methods of the Math class

```
int shipWeight = Math.Round(shipWeightDouble); // round to a whole number
double orderTotal = Math.Round(orderTotal, 2); // round to 2 decimal places
double area = Math.Pow(radius, 2) * Math.PI; // area of circle
double sqrtX = Math.Sqrt(x);
double maxSales = Math.Max(lastYearSales, thisYearSales);
int minQty = Math.Min(lastYearQty, thisYearQty);
```

# Results from static methods of the Math class

| Statement | Result | Statement | Result |
|---|---|---|---|
| Math.Round(23.75, 1) | 23.8 | Math.Pow(5, 2) | 25 |
| Math.Round(23.85, 1) | 23.8 | Math.Sqrt(20.25) | 4.5 |
| Math.Round(23.744, 2) | 23.74 | Math.Max(23.75, 20.25) | 23.75 |
| Math.Round(23.745, 2) | 23.74 | Math.Min(23.75, 20.25) | 20.25 |
| Math.Round(23.745, 2, MidpointRounding.AwayFromZero) | 23.75 | | |

# Description

+   - To use one of the static methods of the Math class, code the class name, a dot, the method name, and one or more arguments in parentheses. The arguments provide the values that are used by the method.
+   - The Round() method rounds a decimal argument to the specified precision, which is the number of significant decimal digits. If the precision is omitted, the number is rounded to the nearest whole number.
+   - By default, if you round a decimal value that ends in 5, the number is rounded to the nearest even decimal value. This is referred to as banker’s rounding. You can also code the mode argument with a value of MidpointRounding.AwayFromZero to round positive values up and negative values down.
+   - The Pow() method raises the first argument to the power of the second argument. Both arguments must have the double data type.
+   - The Sqrt() method returns the square root of the specified argument, which can have any numeric data type.
+   - The Min() and Max() methods return the minimum and maximum of two numeric arguments. The two arguments must have the same data type.