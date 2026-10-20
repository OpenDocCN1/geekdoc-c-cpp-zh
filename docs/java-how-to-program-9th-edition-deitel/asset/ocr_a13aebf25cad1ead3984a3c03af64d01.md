example, you’ll see that exceptions are thrown (i.e., the exception occurs) when a method detects a problem and is unable to handle it.

```
// Fig. 11.1: DivideByZeroNoExceptionHandling.java
// Integer division without exception handling.
import java.util.Scanner;
public class DivideByZeroNoExceptionHandling
{
    // demonstrates throwing an exception when a divide-by-zero occurs
    public static int quotient(int numerator, int denominator)
    {
        return numerator / denominator; // possible division by zero
    } // end method quotient
    public static void main(String[] args)
    {
        Scanner scanner = new Scanner(System.in); // scanner for input
        System.out.print("Please enter an integer numerator: ");
        int numerator = scanner.nextInt();
        System.out.print("Please enter an integer denominator: ");
        int denominator = scanner.nextInt();
        int result = quotient(numerator, denominator);
        System.out.printf(
            "%nResult: %d / %d = %d%n", numerator, denominator, result);
    } // end main
}
```

```
Please enter an integer numerator: 100
Please enter an integer denominator: 7
Result: 100 / 7 = 14
```

```
Please enter an integer numerator: 100
Please enter an integer denominator: 0
Exception in thread "main" java.lang.ArithmeticException: / by zero
at DivideByZeroNoExceptionHandling.quotient(DivideByZeroNoExceptionHandling.java:10)
at DivideByZeroNoExceptionHandling.main(DivideByZeroNoExceptionHandling.java:22)
```

```
Please enter an integer numerator: 100
Please enter an integer denominator: hello
Exception in thread "main" java.util.InputMismatchException
at java.util.Scanner.throwFor(Unknown Source)
at java.util.Scanner.next(Unknown Source)
at java.util.Scanner.nextInt(Unknown Source)
at DivideByZeroNoExceptionHandling.main(DivideByZeroNoExceptionHandling.java:20)
```

> Fig. 11.1 | Integer division without exception handling.