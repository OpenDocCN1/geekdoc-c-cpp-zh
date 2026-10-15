In fact, the increment portion of the for loop can perform any calculation, not just a simple increment or decrement. Consider the program shown in Listing 6.3, which prints multiples of a particular value up to a particular limit.

The increment portion of the for loop in the Multiples program adds the value entered by the user after each iteration. The number of values printed per line is controlled by counting the values printed and then moving to the next line whenever count is evenly divisible by the PER_LINE constant.

# LISTING 6.3

```
//****************************************************************
// Multiples.java      Author: Lewis/Loftus
//
// Demonstrates the use of a for loop.
//****************************************************************

import java.util.Scanner;

public class Multiples
{
    //-------------------------------------------------------------
    // Prints multiples of a user-specified number up to a user-
    // specified limit.
    //-------------------------------------------------------------
    public static void main (String[] args)
    {
        final int PER_LINE = 5;
        int value, limit, mult, count = 0;

        Scanner scan = new Scanner (System.in);

        System.out.print ("Enter a positive value: ");
        value = scan.nextInt();

        System.out.print ("Enter an upper limit: ");
        limit = scan.nextInt();

        System.out.println ();
        System.out.println ("The multiples of " + value + " between " +
                            value + " and " + limit + " (inclusive) are:");

        for (mult = value; mult <= limit; mult += value)
        {
            System.out.print (mult + "\t");
```