The System.out object also provides another service we can use: the print method. The difference between print and println is small but important. The println method prints the information sent to it, then moves to the beginning of the next line. The print method is similar to println, but does not advance to the next line when completed.

The program shown in Listing 2.1 is called Countdown, and it invokes both the print and println methods.

Carefully compare the output of the Countdown program, shown at the bottom of the program listing, to the program code. Note that the word Liftoff is printed on the same line as the first few words, even though it is printed using the println method. Remember that the println method moves to the beginning of the next line after the information passed to it has been printed.

# KEY CONCEPT

The print and println methods represent two services provided by the System.out object.

# LISTING 2.1

```
//************************************************************************
//  Countdown.java      Author: Lewis/Loftus
//
//  Demonstrates the difference between print and println.
//************************************************************************
public class Countdown
{
    //-------------------------------------------------------------
    //  Prints two lines of output representing a rocket countdown.
    //-------------------------------------------------------------
    public static void main (String[] args)
    {
        System.out.print ("Three... ");
        System.out.print ("Two... ");
        System.out.print ("One... ");
        System.out.print ("Zero... ");
        System.out.println ("Liftoff!"); // appears on first output line
        System.out.println ("Houston, we have a problem.");
    }
}
```

# OUTPUT

Three... Two... One... Zero... Liftoff!
Houston, we have a problem.