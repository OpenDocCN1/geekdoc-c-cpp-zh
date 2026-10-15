The Wages program shown in Listing 5.2 uses an if-else statement to compute the proper payment amount for an employee.

In the Wages program, if an employee works over 40 hours in a week, the payment amount takes into account the overtime hours. An if-else statement is used to determine whether the number of hours entered by the user is greater than 40. If it is, the extra hours are paid at a rate one and a half times the normal rate. If there are no overtime hours, the total payment is based simply on the number of hours worked and the standard rate.

Let’s look at another example of an if-else statement:

```
if (roster.getSize() == FULL)
    roster.expand();
else
    roster.addName (name);
```

# LISTING 5.2

```
//****************************************************************
// Wages.java        Author: Lewis/Lofitus
//
// Demonstrates the use of an if-else statement.
//****************************************************************

import java.text.NumberFormat;
import java.util.Scanner;

public class Wages
{
    //-------------------------------------------------------------
    // Reads the number of hours worked and calculates wages.
    //-------------------------------------------------------------
    public static void main (String[] args)
    {
        final double RATE = 8.25;  // regular pay rate
        final int STANDARD = 40;   // standard hours in a work week

        Scanner scan = new Scanner (System.in);

        double pay = 0.0;

        System.out.print ("Enter the number of hours worked: ");
        int hours = scan.nextInt();
```