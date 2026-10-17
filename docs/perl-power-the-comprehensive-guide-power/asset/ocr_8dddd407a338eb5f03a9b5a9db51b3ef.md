does not accurately name this number, but it provides an example of the number of digits likely to be involved.

```
```perl
#Listing05_05
$LargeNumber = 393939393933838;
print "\nLarge: " . int($LargeNumber);
$GargantuanNumber = 393939393933838339303839303383930303839;
print "\nGargantuan: " . int($GargantuanNumber);
```
```

Rather than reporting with the second number that you have exceeded the limits of the integer range available to you as you have counted your photons, the Perl interpreter simply transforms the integer into a rational number presented in scientific notation. The output is as follows:

```
```
Large: 393939393933838
Gargantuan: 3.939393939333838e+051
```
```

The Perl interpreter creates a rational number with a decimal precision of 14, lops off any digits you might have exceeding that limit, and generates the scientifically noted number you see.

# Rational Operations

When you combine numbers, the Perl interpreter follows the logic of *type promotion*. Type promotion stipulates that if you combine two numbers of different types, the resulting value is of (or cast to) the type that provides the greatest storage ability. For example, an integer requires relatively little storage space. A float requires more than an integer. If you combine an integer and a float, the result is a float. Perl does not work in this way on a visible level because it does not require strict type designation for the identifiers you create. Still, when you work with numbers, Perl tends to maintain a logic of type promotion as you combine different values. Listing05_06 provides examples of what happens with the declaration and combination differed identifiers.

```
```perl
#Listing05_06
#1 Use of decimals, scientific notation, and integers
#1 Initialize identifiers
$LightYear = 9.6 * (10 ** 12);       #kilometers
$DToProximaCentauri = 4.26;          #light years
$FarthestGalaxy = 15 * (1.0e9);      #light years
$MilkyWayDiameter = 1000000;         #light years
$MilkyWayThickness = 1000;           #light years
$StarsInMilkyWay = 1.0 * (10 ** 11);
$PI = 3.1415926;
```
```