
## 11.2 Uncaught Exceptions

If a program does not handle the exception at all, it will terminate abnormally and produce a message that describes what exception occurred and where it was produced. The information associated with an exception is often helpful in tracking down the cause of a problem.

Let's look at the output of an exception. The program shown in Listing 11.1 throws an ArithmeticException when an invalid arithmetic operation is attempted. In this case, the program attempts to divide by zero.

Because there is no code in this program to handle the exception explicitly, it terminates when the exception occurs, printing specific information about the exception. Note that the last println statement in the program never executes, because the exception occurs first.

### LISTING 11.1

```
//****************************************************************
// Zero.java      Author: Lewis/Loftus
//
// Demonstrates an uncaught exception.
//****************************************************************

public class Zero
{
    //-------------------------------------------------------------
    // Deliberately divides by zero to produce an exception.
    //-------------------------------------------------------------
    public static void main (String[] args)
    {
        int numerator = 10;
        int denominator = 0;

        System.out.println (numerator / denominator);

        System.out.println ("This text will not be printed.");
    }
}
```

### OUTPUT

```
Exception in thread "main" java.lang.ArithmeticException: / by zero
    at Zero.main(Zero.java:17)
```

## KEY CONCEPT

The messages printed when an exception is thrown provide a method call stack trace.

The first line of the exception output indicates which exception was thrown and provides some information about why it was thrown. The remaining lines are the call stack trace; they indicate where the exception occurred. In this case, there is only one line in the call stack trace, but there may be several depending on where the exception originated. The first trace line indicates the method, file, and line number where the exception occurred. The other trace lines, if present, indicate the methods that were called to get to the method that produced the exception. In this program, there is only one method, and it produced the exception; therefore there is only one line in the trace.

The call stack trace information is also available by calling methods of the exception class that is being thrown. The method getMessage returns a string explaining the reason the exception was thrown. The method printStackTrace prints the call stack trace.

### SELF-REVIEW QUESTION (see answer in Appendix N)

SR 11.3 True or False. Explain.

- a. An exception and an error are the same thing.
- b. An attempt to divide by zero will cause an exception to be thrown.
- c. If a program does not handle a raised exception, the exception is ignored and nothing happens.
- d. If a program does not handle an exception, a message related to the exception will be produced.
- e. A call stack trace shows the sequence of method calls that led to the code where an exception occurred.

## 11.3 The try-catch Statement

Let’s now examine how we catch and handle an exception when it is thrown. The try-catch statement identifies a block of statements that may throw an exception. A catch clause, which follows a try block, defines how a particular kind of exception is handled. A try block can have several catch clauses associated with it. Each catch clause is called an exception handler.

When a try statement is executed, the statements in the try block are executed. If no exception is thrown during the execution of the try block, processing continues with the statement following the try statement (after all of the catch clauses). This situation is the normal execution flow and should occur most of the time.

If an exception is thrown at any point during the execution of the try block, control is immediately transferred to the appropriate catch handler if it is present. That is, control transfers to the first catch clause whose exception class corresponds to the exception that was thrown. After executing the statements in the catch clause, control transfers to the statement after the entire try-catch statement.

Let’s look at an example. Suppose a hypothetical company uses codes to represent its various products. A product code includes, among other information, a character in the tenth position that represents the zone from which that product was made, and a four-digit integer in positions 4 through 7 that represents the district in which it will be sold. Due to some reorganization, products from zone R are banned from being sold in districts with a designation of 2000 or higher. The program shown in Listing 11.2 reads product codes from the user and counts the number of banned codes entered.

### KEY CONCEPT
Each catch clause handles a particular kind of exception that may be thrown within the try block.

### Try Statement

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_568_0.png)

A try statement contains a block of code followed by one or more catch clauses. If an exception occurs in the try block, the code of the corresponding catch clause is executed. The finally clause, if present, is executed no matter how the try block is exited.

Example:

```
try
{
    System.out.println (Integer.parseInt(numString));
}
catch (NumberFormatException exception)
{
    System.out.println ("Caught an exception.");
}
finally
{
    System.out.println ("Done.");
}
```

```java
/**************************************************************
//  ProductCodes.java        Author: Lewis/Loftus
//
//  Demonstrates the use of a try-catch block.
/**************************************************************

import java.util.Scanner;

public class ProductCodes
{
    //-----------------------------------------------------------
    //  Counts the number of product codes that are entered with a
    //  zone of R and a district greater than 2000.
    //-----------------------------------------------------------
    public static void main (String[] args)
    {
        String code;
        char zone;
        int district, valid = 0, banned = 0;

        Scanner scan = new Scanner (System.in);

        System.out.print ("Enter product code (XXX to quit): ");
        code = scan.nextLine();

        while (!code.equals ("XXX"))
        {
            try
            {
                zone = code.charAt(0);
                district = Integer.parseInt(code.substring(3, 7));
                valid++;
                if (zone == 'R' && district > 2000)
                    banned++;
            }
            catch (StringIndexOutOfBoundsException exception)
            {
                System.out.println ("Improper code length: " + code);
            }
            catch (NumberFormatException exception)
            {
                System.out.println ("District is not numeric: " + code);
            }
        }
    }
}
```

### LISTING 11.2 continued

```
System.out.print ("Enter product code (XXX to quit): ");
code = scan.nextLine();
}

System.out.println ("# of valid codes entered: " + valid);
System.out.println ("# of banned codes entered: " + banned);
}
```

### OUTPUT

```
Enter product code (XXX to quit): TRV2475A5R-14
Enter product code (XXX to quit): TRD1704A7R-12
Enter product code (XXX to quit): TRL2k74A5R-11
District is not numeric: TRL2k74A5R-11
Enter product code (XXX to quit): TRQ2949A6M-04
Enter product code (XXX to quit): TRV2105A2
Improper code length: TRV2105A2
Enter product code (XXX to quit): TRQ2778A7R-19
Enter product code (XXX to quit): XXX
# of valid codes entered: 4
# of banned codes entered: 2
```

The programming statements in the try block attempt to pull out the zone and district information, and then determine whether it represents a banned product code. If there is any problem extracting the zone and district information, the product code is considered to be invalid and is not processed further. For example, a StringIndexOutOfBoundsException could be thrown by either the charAt or substring methods. Furthermore, a NumberFormatException could be thrown by the parseInt method if the substring does not contain a valid integer. A particular message is printed depending on which exception is thrown. In either case, since the exception is caught and handled, processing continues normally.

Note that, for each code examined, the integer valid is incremented only if no exception is thrown. If an exception is thrown, control transfers immediately to the appropriate catch clause. Likewise, the zone and district are tested by the if statement only if no exception is thrown.
