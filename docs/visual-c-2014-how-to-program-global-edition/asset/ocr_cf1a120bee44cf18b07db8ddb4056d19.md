# 334 Chapter 7 Methods: A Deeper Look

return true if the second is a multiple of the first and false otherwise. Incorporate this method into an app that inputs a series of integers (one pair at a time) and determines whether the second value in each pair is a multiple of the first.

+   **7.17 (Positive, Negative or Zero)** Write expression-bodied method FindIntType that uses the Math.Abs method to determine the sign of an integer. The method should take an integer argument and return 1 if it is positive, -1 if negative, and 0 otherwise. Incorporate this method into an app that inputs a sequence of integers one at a time, and determines whether each is positive, negative or zero.

+   **7.18 (Displaying a Triangle of Asterisks)** Write method TriangleAsterisks that displays a right-isosceles triangle (a triangle with base and perpendicular equal) of asterisks whose side length is specified in integer parameter len. For example, if len is 5, the method should display

```
*
 *
*****
```

Incorporate this method into an app that reads an integer value for len from the user and outputs the asterisks with the TriangleAsterisks method.

+   **7.19 (Displaying a Triangle of Any Character)** Modify the method created in Exercise 7.18 to form the triangle of whatever character is contained in parameter f11Character and provide '*' as the default. If len is 5 and f11Character is '$', the method should display

```
$$
$$$
$\$
$\$
$$$$
```

> [Hint: Use the expression char.Parse(Console.ReadLine()) to read a character from the user. A variable of char can store a single character.]

+   **7.20 (Cylinder Volume)** Write an app that prompts the user for the height and radius of a cylinder and uses expression-bodied method CylinderVolume to calculate the volume of the cylinder.

+   **7.21 (Separating Digits)** Write code segments that completes each of the following tasks:
a) Calculate the first of the quotient when an integer is divided by b.
b) Calculate the remainder when integer is divided by b.
c) Use the app pieces developed in parts (a) and (b) to write a method Display0101gt that receives an integer between 1 and 99999 and displays it as a sequence of digits, separating each pair of digits by two spaces. For example, the integer 4562 should appear as:
d Incorporate the method developed in part (c) into an app that inputs integers and calls Display0101gt by passing the method entered. Display the results.

+   **7.22 (Temperature Conversions)** Implement the following methods:
a) Expression-bodied method Celsius returns the Celsius equivalent of a Fahrenheit temperature, using the calculation

```
5.0 / 9.0 * (f - 32);
```

+   b) Expression-bodied method Fahrenheit returns the Fahrenheit equivalent of a Celsius temperature, using the calculation

```
9.0 / 5.0 * c + 32;
```

+   c) Use the methods from parts (a) and (b) to write an app that enables the user either to enter a Fahrenheit temperature and display the Celsius equivalent or enter a Celsius temperature and display the Fahrenheit equivalent.