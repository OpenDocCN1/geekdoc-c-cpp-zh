
## 13.8 User-Defined Exception Classes

```csharp
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
SquareRootTest (Fig. 13.7) demonstrates our user-defined exception class. The app enables the user to input a numeric value, then invokes method SquareRoot (lines 40-52) to calculate the square root of that value. To perform this calculation, SquareRoot invokes class Math Sqrt method, which returns a double value as its argument. Normally, if the argument is negative, method Sqrt returns NaN. In this program, we'd like to prevent the user from calculating the square root of a negative number. If the numeric value that the user enters is negative, method SquareRoot throws a NegativeNumberException (lines 45–46). Otherwise, SquareRoot invokes class Math's Sqrt to compute the square root (line 50).

```csharp
// Fig. 13.7: SquareRootTest.cs
// Demonstrating a user-defined exception class.
```

```csharp
class SquareRootTest
{
    static void Main(string[] args)
    {
        var continueLoop = true;
        do
```

Fig. 13.7 | Demonstrating a user-defined exception class. (Part I of 3.)

# Chapter 13 Exception Handling: A Deeper Look

```csharp
// catch any NegativeNumberException
{
    Console.Write("Enter a value to calculate the square root of: \n");
    double inputValue = double.Parse(Console.ReadLine());
    double result = SquareRoot(inputValue);
    Console.WriteLine("The square root of {inputValue} is {result:F6}\n");
    continueLoop = false;
} catch (FormatException formatException) {
    Console.WriteLine("\n" + formatException.Message);
    Console.WriteLine("Please enter a double value.\n");
} catch (NegativeNumberException negativeNumberException) {
    Console.WriteLine("\n" + negativeNumberException.Message);
    Console.WriteLine("Please enter a non-negative value.\n");
} while (continueLoop);

// compute square root of parameter; throws
// NegativeNumberException if parameter is negative
public static double SquareRoot(double value)
{
    if (value < 0)
    {
        throw new NegativeNumberException("Square root of negative number not permitted");
    }
    else {
        return Math.Sqrt(value); // compute square root
    }
}
```

Enter a value to calculate the square root of: **30**
The square root of 30 is 5.477226

Enter a value to calculate the square root of: **hello**
Input string was not in a correct format.
Please enter a double value.

Enter a value to calculate the square root of: **25**
The square root of 25 is 5.000000

**Fig. 13.7** | Demonstrating a user-defined exception class. (Part 2 of 3.)

## 13.9 Checking for null References; Introducing C# 6's ?. Operator

| Input | Output |
| :--- | :--- |
| Enter a value to calculate the square root of: -2 | Square root of negative number not permitted. Please enter a non-negative value. |
| Enter a value to calculate the square root of: 2 | The square root of 2 is 1.414214 |

**Fig. 13.7** | Demonstrating a user-defined exception. (Part 3 of 3 )

When the user inputs a value, the try statement (lines 14–34) attempts to invoke SquareRoot using the value input by the user. If the user is not a number, a Format-Exception, and the catch block in lines 25–29 processes the exception. If the user inputs a negative number, method SquareRoot throws a NegativeNumberException (lines 45–46); the catch block in lines 30–34 catches and handles this type of exception.

## 13.9 Checking for null References; Introducing C# 6's ?. Operator

In Section 13.6, we showed the following code snippet:

```csharp
exampleObject = new ExampleClass();
try
{
    exampleObject.SomeMethod();
}
finally
{
    if (exampleObject != null)
    {
        exampleObject.Dispose();
    }
}
```

The statement in the preceding finally block ensures that if exampleObject is null, the call to Dispose is skipped, preventing a NullReferenceException.

> **Error-Prevention Tip 13.6** Always ensure that a reference is not null before using it.

### 13.9.1 Null-Conditional Operator (?)

The statement in the preceding finally block ensures that if exampleObject is null, the call to Dispose is skipped, preventing a NullReferenceException.

> **Error-Prevention Tip 13.6** Always ensure that a reference is not null before using it.

### 13.9.2 Revisiting Operators as

The statement in the preceding finally block ensures that if exampleObject is null, the call to Dispose is skipped, preventing a NullReferenceException.

> **Error-Prevention Tip 13.6** Always ensure that a reference is not null before using it.

### 13.9.3 Nullable Types

The statement in the preceding finally block ensures that if exampleObject is null, the call to Dispose is skipped, preventing a NullReferenceException.

> **Error-Prevention Tip 13.6** Always ensure that a reference is not null before using it.

### 13.9.4 Null Coalescing Operator (??)

The statement in the preceding finally block ensures that if exampleObject is null, the call to Dispose is skipped, preventing a NullReferenceException.

> **Error-Prevention Tip 13.6** Always ensure that a reference is not null before using it.

### 13.10 Exception Filters and the C# 6 when Clause
