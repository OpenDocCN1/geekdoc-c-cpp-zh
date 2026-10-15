
static int abs (int num)
    Returns the absolute value of num.

static double acos (double num)
static double asin (double num)
static double atan (double num)
    Returns the arc cosine, arc sine, or arc tangent of num.

static double cos (double angle)
static double sin (double angle)
static double tan (double angle)
    Returns the angle cosine, sine, or tangent of angle, which is measured in radians.

static double ceil (double num)
    Returns the ceiling of num, which is the smallest whole number greater than or equal to num.

static double exp (double power)
    Returns the value e raised to the specified power.

static double floor (double num)
    Returns the floor of num, which is the largest whole number less than or equal to num.

static double pow (double num, double power)
    Returns the value num raised to the specified power.

static double random ()
    Returns a random number between 0.0 (inclusive) and 1.0 (exclusive).

static double sqrt (double num)
    Returns the square root of num, which must be positive.

## FIGURE 3.5 Some methods of the Math class

Note that this program assumes that the discriminant (the value under the square root) is negative. If it’s not negative, the results will not be a valid number, which Java represents as NAN, which stands for Not A Number. In Chapter 5 we will see how we can handle this type of situation gracefully.

## LISTING 3.3

```
//************************************************************************
// Quadratic.java      Author: Lewis/Loftus
//
// Demonstrates the use of the Math class to perform a calculation
// based on user input.
//************************************************************************

import java.util.Scanner;

public class Quadratic
{
    //------------------------------------------------------------
    // Determines the roots of a quadratic equation.
    //------------------------------------------------------------
    public static void main (String[] args)
    {
        int a, b, c;  // ax^2 + bx + c
        double discriminant, root1, root2;

        Scanner scan = new Scanner (System.in);

        System.out.print ("Enter the coefficient of x squared: ");
        a = scan.nextInt();

        System.out.print ("Enter the coefficient of x: ");
        b = scan.nextInt();

        System.out.print ("Enter the constant: ");
        c = scan.nextInt();

        // Use the quadratic formula to compute the roots.
        // Assumes a positive discriminant.

        discriminant = Math.pow(b, 2) - (4 * a * c);
        root1 = ((-1 * b) + Math.sqrt(discriminant)) / (2 * a);
        root2 = ((-1 * b) - Math.sqrt(discriminant)) / (2 * a);

        System.out.println ("Root #1: " + root1);
        System.out.println ("Root #2: " + root2);
    }
}
```

## LISTING 3.3 continued

## OUTPUT

```
Enter the coefficient of x squared: 3
Enter the coefficient of x: 8
Enter the constant: 4
Root #1: -0.6666666666666666
Root #2: -2.0
```

## SELF-REVIEW QUESTIONS (see answers in Appendix N)

- SR 3.20 What is a class method (also called a static method)?
- SR 3.21 What is the value of each of the following expressions?
  - a. Math.abs(10) + Math.abs(-10)
  - b. Math.pow(2, 4)
  - c. Math.pow(4, 2)
  - d. Math.pow(3, 5)
  - e. Math.pow(5, 3)
  - f. Math.sqrt(16)
- SR 3.22 Write a statement that prints the sine of an angle measuring 1.23 radians.
- SR 3.23 Write a declaration for a double variable called result and initialize it to 5 raised to the power 2.5.
- SR 3.24 Using the online Java API documentation, list three methods of the Math class that are not included in Figure 3.5.

## 3.6 Formatting Output

The NumberFormat class and the DecimalFormat class are used to format information so that it looks appropriate when printed or displayed. They are both part of the Java standard class library and are defined in the java.text package.

### The NumberFormat Class

The NumberFormat class provides generic formatting capabilities for numbers. You don’t instantiate a NumberFormat object by using the new operator. Instead, you request an object from one of the static methods that you invoke through the class name itself. Figure 3.6 lists some of the methods of the NumberFormat class.

String format (double number)
Returns a string containing the specified number formatted according to this object's pattern.

static NumberFormat getCurrencyInstance()
Returns a NumberFormat object that represents a currency format for the current locale.

static NumberFormat getPercentInstance()
Returns a NumberFormat object that represents a percentage format for the current locale.

## FIGURE 3.6 Some methods of the NumberFormat class

Two of the methods in the NumberFormat class, getCurrencyInstance and getPercentInstance, return an object that is used to format numbers. The getCurrencyInstance method returns a formatter for monetary values, and the getPercentInstance method returns an object that formats a percentage. The format method is invoked through a formatter object and returns a String that contains the number formatted in the appropriate manner.

The Purchase program shown in Listing 3.4 uses both types of formatters. It reads in a sales transaction and computes the final price, including tax.

## LISTING 3.4

```
//****************************************************************
// Purchase.java Author: Lewis/Loftus
//
// Demonstrates the use of the NumberFormat class to format output.
//****************************************************************

import java.util.Scanner;
import java.text.NumberFormat;

public class Purchase
{
//---------------------------------------------------------------
// Calculates the final price of a purchased item using values
// entered by the user.
//---------------------------------------------------------------
public static void main (String[] args)
{
    final double TAX_RATE = 0.06;  // 6% sales tax

    int quantity;
    double subtotal, tax, totalCost, unitPrice;

    Scanner scan = new Scanner (System.in);

    NumberFormat fmt1 = NumberFormat.getCurrencyInstance();
    NumberFormat fmt2 = NumberFormat.getPercentInstance();

    System.out.print ("Enter the quantity: ");
    quantity = scan.nextInt();

    System.out.print ("Enter the unit price: ");
    unitPrice = scan.nextDouble();

    subtotal = quantity * unitPrice;
    tax = subtotal * TAX_RATE;
    totalCost = subtotal + tax;

    // Print output with appropriate formatting
    System.out.println ("Subtotal: " + fmt1.format(subtotal));
    System.out.println ("Tax: " + fmt1.format(tax) + " at "
        + fmt2.format(TAX_RATE));
    System.out.println ("Total: " + fmt1.format(totalCost));
}
```

## LISTING 3.4 continued

## OUTPUT

```
Enter the quantity: 5
Enter the unit price: 3.87
Subtotal: $19.35
Tax: $1.16 at 6%
Total: $20.51
```

### The DecimalFormat Class

Unlike the NumberFormat class, the DecimalFormat class is instantiated in the traditional way using the new operator. Its constructor takes a string that represents the pattern that will guide the formatting process. We can then use the

DecimalFormat (String pattern)
    Constructor: creates a new DecimalFormat object with the specified pattern.

void applyPattern (String pattern)
    Applies the specified pattern to this DecimalFormat object.

String format (double number)
    Returns a string containing the specified number formatted according to the current pattern.

## FIGURE 3.7 Some methods of the DecimalFormat class

format method to format a particular value. At a later point, if we want to change the pattern that the formatter object uses, we can invoke the applyPattern method. Figure 3.7 describes these methods.

The pattern defined by the string that is passed to the DecimalFormat constructor can get fairly elaborate. Various symbols are used to represent particular formatting guidelines. The pattern defined by the string "0.###", for example, indicates that at least one digit should be printed to the left of the decimal point and should be a zero if the integer portion of the value is zero. It also indicates that the fractional portion of the value should be rounded to three digits.

This pattern is used in the CircleStats program, shown in Listing 3.5, which reads the radius of a circle from the user and computes its area and circumference. Trailing zeros, such as in the circle’s area of 78.540, are not printed.

### The printf Method

In addition to print and println, the System class has another output method called printf, which allows the user to print a formatted string containing data values. The first parameter to the method represents the format string, and the remaining parameters specify the values that are inserted into the format string.

For example, the following line of code prints an ID number and a name:

```
System.out.printf ("ID: %5d\tName: %s", id, name);
```

The first parameter specifies the format of the output and includes literal characters that label the output values as well as escape characters such as \t. The pattern %5d indicates that the corresponding numeric value (id) should be printed in a field of five characters. The pattern %s matches the string parameter
