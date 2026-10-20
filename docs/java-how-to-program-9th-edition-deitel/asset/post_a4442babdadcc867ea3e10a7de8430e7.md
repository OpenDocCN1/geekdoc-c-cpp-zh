
```
12      System.out.printf( "Math.ceil( -9.8 ) = %f\n", Math.ceil( -9.8 ) );
13      System.out.printf( "Math.cos( 0.0 ) = %f\n", Math.cos( 0.0 ) );
14      System.out.printf( "Math.exp( 1.0 ) = %f\n", Math.exp( 1.0 ) );
15      System.out.printf( "Math.exp( 2.0 ) = %f\n", Math.exp( 2.0 ) );
16      System.out.printf( "Math.floor( 9.2 ) = %f\n", Math.floor( 9.2 ) );
17      System.out.printf( "Math.floor( -9.8 ) = %f\n",
18          Math.floor( -9.8 ) );
19      System.out.printf( "Math.log( Math.E ) = %f\n",
20          Math.log( Math.E ) );
21      System.out.printf( "Math.log( Math.E * Math.E ) = %f\n",
22          Math.log( Math.E * Math.E ) );
23      System.out.printf( "Math.max( 2.3, 12.7 ) = %f\n",
24          Math.max( 2.3, 12.7 ) );
25      System.out.printf( "Math.max( -2.3, -12.7 ) = %f\n",
26          Math.max( -2.3, -12.7 ) );
27      System.out.printf( "Math.min( 2.3, 12.7 ) = %f\n",
28          Math.min( 2.3, 12.7 ) );
29      System.out.printf( "Math.min( -2.3, -12.7 ) = %f\n",
30          Math.min( -2.3, -12.7 ) );
31      System.out.printf( "Math.pow( 2.0, 7.0 ) = %f\n",
32          Math.pow( 2.0, 7.0 ) );
33      System.out.printf( "Math.pow( 9.0, 0.5 ) = %f\n",
34          Math.pow( 9.0, 0.5 ) );
35      System.out.printf( "Math.sin( 0.0 ) = %f\n", Math.sin( 0.0 ) );
36      System.out.printf( "Math.sqrt( 900.0 ) = %f\n",
37          Math.sqrt( 900.0 ) );
38      System.out.printf( "Math.tan( 0.0 ) = %f\n", Math.tan( 0.0 ) );
39      } // end main
40      } // end class MathTest
```

Math.abs( 23.7 ) = 23.700000
Math.abs( 0.0 ) = 0.000000
Math.abs( -23.7 ) = 23.700000
Math.ceil( 9.2 ) = 10.000000
Math.ceil( -9.8 ) = -9.000000
Math.cos( 0.0 ) = 1.000000
Math.exp( 1.0 ) = 2.718282
Math.exp( 2.0 ) = 7.389056
Math.floor( 9.2 ) = 9.000000
Math.floor( -9.8 ) = -10.000000
Math.log( Math.E ) = 1.000000
Math.log( Math.E * Math.E ) = 2.000000
Math.max( 2.3, 12.7 ) = 12.700000
Math.max( -2.3, -12.7 ) = -2.300000
Math.min( 2.3, 12.7 ) = 2.300000
Math.min( -2.3, -12.7 ) = -12.700000
Math.pow( 2.0, 7.0 ) = 128.000000
Math.pow( 9.0, 0.5 ) = 3.000000
Math.sin( 0.0 ) = 0.000000
Math.sqrt( 900.0 ) = 30.000000
Math.tan( 0.0 ) = 0.000000

6.4    a) double hypotenuse( double side1, double side2 )
       b) int smallest( int x, int y, int z )
       c) void instructions()
       d) float intToFloat( int number )

6.5    a) Error: Method h is declared within method g.
       Correction: Move the declaration of h outside the declaration of g.
       b) Error: The method is supposed to return an integer, but does not.
       Correction: Delete the variable result, and place the statement

return x + y;

in the method, or add the following statement at the end of the method body:

return result;

+   c) Error: The semicolon after the right parenthesis of the parameter list is incorrect, and the parameter a should not be redeclared in the method.
+   Correction: Delete the semicolon after the right parenthesis of the parameter list, and delete the declaration float a;

+   d) Error: The method returns a value when it’s not supposed to.
+   Correction: Change the return type from void to int.

6.6 The following solution calculates the volume of a sphere, using the radius entered by the user:

```
// Exercise 6.6: Sphere.java
// Calculate the volume of a sphere.
import java.util.Scanner;

public class Sphere
{
    // obtain radius from user and display volume of sphere
    public static void main( String[] args )
    {
        Scanner input = new Scanner( System.in );

        System.out.print( "Enter radius of sphere: " );
        double radius = input.nextDouble();

        System.out.printf( "Volume is %f\n", sphereVolume( radius ) );
    } // end method determineSphereVolume

    // calculate and return sphere volume
    public static double sphereVolume( double radius )
    {
        double volume = ( 4.0 / 3.0 ) * Math.PI * Math.pow( radius, 3 );
        return volume;
    } // end method sphereVolume
} // end class Sphere
```

Enter radius of sphere: 4
Volume is 268.082573

# Exercises

6.7 What is the value of x after each of the following statements is executed?

+   a) x = Math.abs( 7.5 );
+   b) x = Math.floor( 7.5 );
+   c) x = Math.abs( 0.0 );
+   d) x = Math.ceil( 0.0 );
+   e) x = Math.abs( -6.4 );
+   f) x = Math.ceil( -6.4 );
+   g) x = Math.ceil( -Math.abs( -8 + Math.floor( -5.5 ) ) );

6.8 (Parking Charges) A parking garage charges a $2.00 minimum fee to park for up to three hours. The garage charges an additional $0.50 per hour for each hour or part thereof in excess of three hours. The maximum charge for any given 24-hour period is $10.00. Assume that no car parks for longer than 24 hours at a time. Write an application that calculates and displays the parking charges for each customer who parked in the garage yesterday. You should enter the hours parked for each customer. The program should display the charge for the current customer and should calculate and display the running total of yesterday’s receipts. It should use the method calculateCharges to determine the charge for each customer.

# 6.9 (Rounding Numbers) Math.floor can be used to round values to the nearest integer—e.g.,

```
y = Math.floor( x + 0.5 );
```

will round the number x to the nearest integer and assign the result to y. Write an application that reads double values and uses the preceding statement to round each of the numbers to the nearest integer. For each number processed, display both the original number and the rounded number.

# 6.10 (Rounding Numbers) To round numbers to specific decimal places, use a statement like

```
y = Math.floor( x * 10 + 0.5 ) / 10;
```

which rounds x to the tenths position (i.e., the first position to the right of the decimal point), or

```
y = Math.floor( x * 100 + 0.5 ) / 100;
```

which rounds x to the hundredths position (i.e., the second position to the right of the decimal point). Write an application that defines four methods for rounding a number x in various ways:

+   a) roundToInteger( number )
+   b) roundToTenths( number )
+   c) roundToHundredths( number )
+   d) roundToThousandths( number )

For each value read, your program should display the original value, the number rounded to the nearest integer, the number rounded to the nearest tenth, the number rounded to the nearest hundredth and the number rounded to the nearest thousandth.

# 6.11 Answer each of the following questions:

+   a) What does it mean to choose numbers “at random”?
+   b) Why is the nextInt method of class Random useful for simulating games of chance?
+   c) Why is it often necessary to scale or shift the values produced by a Random object?
+   d) Why is computerized simulation of real-world situations a useful technique?

# 6.12 Write statements that assign random integers to the variable n in the following ranges:

+   a) 1 ≤ n ≤ 2.
+   b) 1 ≤ n ≤ 100.
+   c) 0 ≤ n ≤ 9.
+   d) 1000 ≤ n ≤ 1112.
+   e) −1 ≤ n ≤ 1.
+   f) −3 ≤ n ≤ 11.

# 6.13 Write statements that will display a random number from each of the following sets:

+   a) 2, 4, 6, 8, 10.
+   b) 3, 5, 7, 9, 11.
+   c) 6, 10, 14, 18, 22.

# 6.14 (Exponentiation) Write a method integerPower(base, exponent) that returns the value of base exponent

For example, integerPower(3, 4) calculates 3⁴ (or 3 * 3 * 3 * 3). Assume that exponent is a positive, nonzero integer and that base is an integer. Use a for or while statement to control the calculation. Do not use any Math class methods. Incorporate this method into an application that reads integer values for base and exponent and performs the calculation with the integerPower method.

# 6.15 (Hypotenuse Calculations) Define a method hypotenuse that calculates the hypotenuse of a right triangle when the lengths of the other two sides are given. The method should take two arguments of type double and return the hypotenuse as a double. Incorporate this method into an application that reads values for side1 and side2 and performs the calculation with the hypotenuse method. Use Math methods pow and sqrt to determine the length of the hypotenuse for each of the triangles in Fig. 6.15. [Note: Class Math also provides method hypot to perform this calculation.]

| Triangle | Side 1 | Side 2 |
|---|---|---|
| 1 | 3.0 | 4.0 |
| 2 | 5.0 | 12.0 |
| 3 | 8.0 | 15.0 |

Fig. 6.15 | Values for the sides of triangles in Exercise 6.15.

6.16 (Multiples) Write a method isMultiple that determines, for a pair of integers, whether the second integer is a multiple of the first. The method should take two integer arguments and return true if the second is a multiple of the first and false otherwise. [Hint: Use the remainder operator.] Incorporate this method into an application that inputs a series of pairs of integers (one pair at a time) and determines whether the second value in each pair is a multiple of the first.

6.17 (Even or Odd) Write a method isEven that uses the remainder operator (%) to determine whether an integer is even. The method should take an integer argument and return true if the integer is even and false otherwise. Incorporate this method into an application that inputs a sequence of integers (one at a time) and determines whether each is even or odd.

6.18 (Displaying a Square of Asterisks) Write a method squareOfAsterisks that displays a solid square (the same number of rows and columns) of asterisks whose side is specified in integer parameter side. For example, if side is 4, the method should display
****
****
****
****

Incorporate this method into an application that reads an integer value for side from the user and outputs the asterisks with the squareOfAsterisks method.

6.19 (Displaying a Square of Any Character) Modify the method created in Exercise 6.18 to receive a second parameter of type char called fillCharacter. Form the square using the char provided as an argument. Thus, if side is 5 and fillCharacter is #, the method should display
#####
#####
#####
#####
#####

Use the following statement (in which input is a Scanner object) to read a character from the user at the keyboard:

```
char fill = input.next().charAt(0);
```

6.20 (Circle Area) Write an application that prompts the user for the radius of a circle and uses a method called circleArea to calculate the area of the circle.

6.21 (Separating Digits) Write methods that accomplish each of the following tasks:
a) Calculate the integer part of the quotient when integer a is divided by integer b.
b) Calculate the integer remainder when integer a is divided by integer b.
