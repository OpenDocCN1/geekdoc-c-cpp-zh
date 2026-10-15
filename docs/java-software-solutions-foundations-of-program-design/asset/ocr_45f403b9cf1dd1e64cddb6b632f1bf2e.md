Because the right-hand expression is evaluated first, the original value of count is obtained and the value 1 is added to it, producing the result 16. That result is then stored in the variable count, overwriting the original value of 15 with the new value of 16. Therefore, this assignment statement increments, or adds 1 to, the variable count.

Let’s look at another example of expression processing. The program in Listing 2.7, called TempConverter, converts a particular Celsius temperature value to its equivalent Fahrenheit value using an expression that computes the following formula:

Fahrenheit = 9/5 Celsius + 32

# LISTING 2.7

```
//************************************************************************
// TempConverter.java      Author: Lewis/Loftus
//
// Demonstrates the use of primitive data types and arithmetic
// expressions.
//************************************************************************

public class TempConverter
{
    //-------------------------------------------------------------
    // Computes the Fahrenheit equivalent of a specific Celsius
    // value using the formula F = (9/5)C + 32.
    //-------------------------------------------------------------
    public static void main (String[] args)
    {
        final int BASE = 32;
        final double CONVERSION_FACTOR = 9.0 / 5.0;

        double fahrenheitTemp;
        int celsiusTemp = 24;  // value to convert

        fahrenheitTemp = celsiusTemp * CONVERSION_FACTOR + BASE;

        System.out.println ("Celsius Temperature: " + celsiusTemp);
        System.out.println ("Fahrenheit Equivalent: " + fahrenheitTemp);
    }
}
```

# OUTPUT

Celsius Temperature: 24
Fahrenheit Equivalent: 75.2