
## CHAPTER 5 Scalars and Formatting

```perl
$PlRadiusOfEarth = 6357;
$EqRadiusOfEarth = 6378;
# rational number - floating decimal values
$EarthToSun = 149597870.7;
# Scientific notation
$EarthToMoon = 3.84401e6;
$AgeOfSolarSystem = 4.6e9;
# Raising 10 to the ninth power
$AgeOfKnownUniverse = 16.5 * (10 ** 9);
# Large integers
$SpeedOfLight = 299792458; # meters per second

#2 Print the values
print "\nPolar radius of earth: " .
 " $PlRadiusOfEarth kilometers.";
print "\nEquatorial radius of earth: " .
 " $EqRadiusOfEarth kilometers.";
print "\nThe distance to the sun from earth: " .
 " $EarthToSun kilometers.";
print "\nThe distance from the earth to the moon: " .
 " $EarthToMoon kilometers.";
print "\nThe age of the solar system: " .
 " $AgeOfSolarSystem years.";
print "\nThe age of the known universe: " .
 " $AgeOfKnownUniverse years.";
print "\nThe known universe: " .
 " $RatioOfSsToKU times older than the solar system.";
print "\nThe speed of light: " .
 " $SpeedOfLight meters per second.";
```

In Listing05_03, you create a scalar, $PlRadiusOfEarth, to represent the polar radius of Earth in kilometers as an integer (6357). An integer ($EqRadiusOfEarth) also accommodates the equatorial radius of Earth (6378). Figure 5.4 illustrates the output of Listing05_03.

Next, you create a scalar identifier ($EarthToSun) to accommodate a rational (floating decimal) number that represents the distance to the sun in kilometers (149597870.7). You need no type identifiers. Assignment creates the number as named.

### Standard Presentation Using the print() Function

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_125_0.png)

**Figure 5.4**  
Different types of numbers result from your definition and operations.

In the next two declarations, you define variables using scientific notation. The e raises the base to a given power of 10. For distance to the moon ($EarthToMoon), you create a rational number with a precision of 5 places and then raise the power of 10 to 6 (3.84401e6). To jump into the dimension of time ($AgeOfSolarSystem), given an estimation that the solar system is 4.6 billion years old, you create a rational number with a precision of just one place but raise the power of 10 to 9 (4.6e9).

Perl provides different ways to deal with powers. To simply raise a number to any power, you employ double asterisks (**). To define an identifier for the age of the known universe ($AgeOfKnownUniverse), you can vary from the use of scientific notation employing e and use a more literal approach. Rather than coding the definition as 16.5e9, in this example, you employ the expression 16.5 * (10 ** 9).

In the final declaration, you experiment with a relatively large integer ($SpeedOfLight), which represents the meters per second that light travels (299792458). If you type a particularly large integer value (one that exceeds 14 digits), Perl automatically begins to present your output in scientific notation with a large rational component.

### Random Numbers and Integers

In Table 5.1, the integer is important enough that a numeric function addresses the need of programmers to create integers. To exercise the int() function in a slightly complicated context, consider the use of the int() function in relation to the rand() function. The int() function removes the decimal portion of a number. The rand() function generates a random number:

```perl
# Listing05_04
# int() used to make a random number an integer
# A random number less than 6 and equal to or greater than 0
$RandomNumber = 1 + rand(6);
print "\nRandom number without integer status:\n" . $RandomNumber;
print "\nRandom number converted to an integer:\n" . int($RandomNumber);
```

In Listing05_04, to use the `int()` function, you insert the rational number you want to convert to an integer. In this instance, the number (`$RandomNumber`) possesses a decimal precision of 14. If you are working with a dice game, such precision is not likely to be very useful. The `int()` function truncates the number for you. The output is as follows:

```text
Random number without integer status:

4.77630615234375

Random number converted to an integer:

4

Press a key to continue...
```

### Range Problems and the rand() Function

To generate the random number shown in Listing05_04, you use the `rand()` function. By default, the return value of this function is a rational number in a range that is zero or greater and less than a whole number value of the digit you use as an argument. As Figure 5.5 illustrates, a problem results when you consider that a die has 6 dots. If you use an argument of 6 for the `rand()` function, the largest value the `rand()` function can generate is 5.99999999999999. This is not quite 6. Likewise, a die has 1 to 6 dots; no face is blank. Such inconsistencies constitute a range problem.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_126_0.png)

To solve the range problem, you shift the returned value of the `rand()` function by one. Given the truncation that the `int()` function performs, if you add one to the value the `rand()` function generates and set the argument of `rand()` to 6, you then acquire numbers in the range of 1 to 6.

### Gargantuan Integers

Consider again the use of the `int()` function. In this case, the problem is that you want to do something like name the number of photons bombarding a rooftop on a sunny day. Listing05_05 does not accurately name this number, but it provides an example of the number of digits likely to be involved.

```perl
# Listing05_05
$LargeNumber = 393939393933838;
print "\nLarge: " . int($LargeNumber);
$GargantuanNumber = 393939393933838339303839303383930303839;
print "\nGargantuan: " . int($GargantuanNumber);
```

Rather than reporting with the second number that you have exceeded the limits of the integer range available to you as you have counted your photons, the Perl interpreter simply transforms the integer into a rational number presented in scientific notation. The output is as follows:

```text
Large: 393939393933838
Gargantuan: 3.939393939333838e+038
```

The Perl interpreter creates a rational number with a decimal precision of 14, lops off any digits you might have exceeding that limit, and generates the scientifically notated number you see.

### Rational Operations

When you combine numbers, the Perl interpreter follows the logic of *type promotion*. Type promotion stipulates that if you combine two numbers of different types, the resulting value is of (or cast to) the type that provides the greatest storage ability. For example, an integer requires relatively little storage space. A float requires more than an integer. If you combine an integer and a float, the result is a float. Perl does not work in this way on a visible level because it does not require strict type designation for the identifiers you create. Still, when you work with numbers, Perl tends to maintain a logic of type promotion as you combine different values. Listing05_06 provides examples of what happens with the declaration and combination of different identifiers.

```perl
# Listing05_06
#1 Use of decimals, scientific notation, and integers
# Initialize identifiers
$LightYear = 9.6 * (10 ** 12);       # kilometers
$DToProximaCentauri = 4.26;          # light years
$FarthestGalaxy = 15 * (1.0e9);      # light years
$MilkyWayDiameter = 1000000;         # light years
$MilkyWayThickness = 1000;           # light years
$StarsInMilkyWay = 1.0 * (10 ** 11);
$PI = 3.1415926;
```

```text
#2 Display value
# Interpolated string
print "\nA light year is $LightYear kilometers.";
# Resolved variable
print "\nDistance to Proxima Centauri:" . $DToProximaCentauri . " lys.";
print "\nThe distance to the farthest Galaxy: $FarthestGalaxy lys.";
print "\nThe diameter of the Milky Way: $MilkyWayDiameter lys.";
print "\nThe thickness of the Milky Way: $MilkyWayThickness lys.";
print "\nThe number of stars in the Milky Way: $StarsInMilkyWay.\n\n";
print "Value of PI: $PI";

#3 Perform a calculation
# V = (4 Pi/3)r^3
# Calculate the volume of the universe if it were a sphere
# extending to Proxima Centauri

print "\n \nPerform a calculation: V = (4 Pi/3)r^3.\n";
print '((4 * $PI) / 3) * (($DToProximaCentauri/2) ** 3)' . "\n ";
$VolumeToProxima = ((4 * $PI) / 3) * (($DToProximaCentauri/2) ** 3);

#4 Print using default
print "\nVolume of sphere " .
"(in cubic light years)\n" .
"extending to Proxima Centauri:" . $VolumeToProxima . ".\n\n";

#5 Preliminary view: Print using the sprintf() function
print "\nVolume of sphere " .
"(in cubic light years)\n" .
"extending to Proxima Centauri:" . sprintf("%e", $VolumeToProxima) . ".\n\n";
```

The lines trailing comment #1 in Listing05_06 provide you with a number of different data definitions. All of the definitions involve scalars, but the expressions that initialize the identifiers involve a variety of number types. You define the identifier $LightYear using a combination of a rational number (9.6), a multiplication operator, and an exponential operator (**) that creates 10 to the power of 12. As Figure 5.6 illustrates, the result is an integer. The same procedure characterizes your definition of the identifier $DToProximaCentauri, but this time you assign a simple rational number (4.26).
