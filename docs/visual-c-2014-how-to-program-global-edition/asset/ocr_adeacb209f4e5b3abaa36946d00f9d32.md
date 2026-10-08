# 13.8 User-Defined Exception Classes 573

```
// empty body
}
// constructor for customizing the exception's error
// message and specifying the InnerException object
public class NegativeNumberException(string messageValue, Exception inner)
    : base(messageValue, inner)
{
    // empty body
}
```

Fig. 13.6 | NegativeNumberException represents exceptions caused by illegal operations performed on negative numbers. (Part 2 of 2.)

NegativeNumberExceptions most frequently occur during arithmetic operations, so it seems logical to derive class NegativeNumberException from class ArithmeticException. However, class ArithmeticException derives from class Exception—the category of exceptions thrown by the CLR. Per Microsoft's best practices for exception handling, user-defined exception classes should inherit from Exception rather than SystemException. In this case, we could have used the built-in ArgumentOutOfRangeException (introduced in Chapter 10), which is recommended in the best practices for invalid argument values. We create our own exception type here for demonstration purposes.

Using Class NegativeException
SquareRootTest (Fig. 13.7) demonstrates our user-defined exception class. The app enables the user to input a numeric value, then invokes method SquareRoot (lines 40-52) to calculate the square root of that value. To perform this calculation, SquareRoot invokes class Math Sqrt method, which returns a double value as its argument. Normally, if the argument is negative, method Sqrt returns NaN. In this program, we'd like to prevent the user from calculating the square root of a negative number. If the numeric value that the user enters is, method SquareRoot throws a NegativeNumberException (lines 45–46). Otherwise, SquareRoot invokes class Math's Sqrt to compute the square root (line 50).

```
// Fig. 13.7: SquareRootTest.cs
// Demonstrating a user-defined exception class.
```

```
class SquareRootTest
{
    static void Main(string[] args)
    {
        var continueLoop = true;
        do
        
```

Fig. 13.7 | Demonstrating a user-defined exception class. (Part I of 3.)