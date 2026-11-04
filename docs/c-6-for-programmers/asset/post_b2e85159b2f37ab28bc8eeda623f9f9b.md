
exception of namespace System. When you create code that throws exceptions, they should be well documented, so that other developers who use your code will know how to handle them.

> **Good Programming Practice 13.1**
> Associating each type of malfunction with an appropriately named exception class improves program clarity.

> **Software Engineering Observation 13.4**
> Before creating a user-defined exception class, investigate the existing exceptions in the .NET Framework Class Library to determine whether an appropriate exception type already exists.

## Class NegativeNumberException

Figures 13.6–13.7 demonstrate a user-defined exception class. NegativeNumberException (Fig. 13.6) represents exceptions that occur when a program performs an illegal operation on a negative number, such as attempting to calculate a square root. According to Microsoft's “Best Practices for Handling Exceptions” (bit.ly/Exceptions-BestPractices), user-defined exceptions should typically extend class Exception, have a class name that ends with Exception and define three constructors:

- a parameterless constructor,
- a constructor that receives a string argument (the error message), and
- a constructor that receives a string argument and an Exception argument (the error message and the inner-exception object).

Defining these three constructors makes your exception class more flexible, allowing other programmers to easily use and extend it.

```csharp
// Fig. 13.6: NegativeNumberException.cs
// NegativeNumberException represents exceptions caused by
// illegal operations performed on negative numbers.
using System;

public class NegativeNumberException : Exception
{
    // default constructor
    public NegativeNumberException()
        : base("Illegal operation for a negative number")
    {   // empty body
    }

    // constructor for customizing error message
    public NegativeNumberException(string messageValue)
        : base(messageValue)
    {
        // empty body
    }

    // constructor for customizing the exception's error
    // message and specifying the InnerException object
    public NegativeNumberException(String messageValue, Exception inner)
        : base(messageValue, inner)
    {
    } // empty body
}
```

**Fig. 13.6** | *NegativeNumberException* represents exceptions caused by illegal operations performed on negative numbers.

*NegativeNumberExceptions* most frequently occur during arithmetic operations, so it seems logical to derive class *NegativeNumberException* from class *ArithmeticException*. However, class *ArithmeticException* derives from class *SystemException*—the category of exceptions thrown by the CLR. Per Microsoft's best practices for exception handling, *user-defined exception classes should inherit from Exception rather than SystemException*. In this case, we could have used the built-in *ArgumentOutOfRangeException* class (introduced in Chapter 10), which is recommended in the best practices for invalid argument values. We create our own exception type here simply for demonstration purposes.

## *Using Class NegativeNumberException*

Class *SquareRootTest* (Fig. 13.7) demonstrates our user-defined exception class. The app enables the user to input a numeric value, then invokes method *SquareRoot* (lines 40–52) to calculate the square root of that value. To perform this calculation, *SquareRoot* invokes class *Math*'s *Sqrt* method, which receives a double value as its argument. Normally, if the argument is *negative*, method *Sqrt* returns *NaN*. In this program, we'd like to *prevent* the user from calculating the square root of a negative number. If the numeric value that the user enters is negative, method *SquareRoot* throws a *NegativeNumberException* (lines 45–46). Otherwise, *SquareRoot* invokes class *Math*'s method *Sqrt* to compute the square root (line 50).

```csharp
// Fig. 13.7: SquareRootTest.cs
// Demonstrating a user-defined exception class.
using System;

class SquareRootTest
{
    static void Main(String[] args)
    {
        var continueLoop = true;

        do
        {
        // catch any NegativeNumberException thrown
        try
        {
            Console.Write(
                "Enter a value to calculate the square root of: ");
            double inputValue = double.Parse(Console.ReadLine());
            double result = SquareRoot(inputValue);

            Console.WriteLine(
                $"The square root of {inputValue} is {result:F6}\n");
            continueLoop = false;
        }
        catch (FormatException formatException)
        {
            Console.WriteLine("\n" + formatException.Message);
            Console.WriteLine("Please enter a double value.\n");
        }
        catch (NegativeNumberException negativeNumberException)
        {
            Console.WriteLine("\n" + negativeNumberException.Message);
            Console.WriteLine("Please enter a non-negative value.\n");
        }
        } while (continueLoop);

    }

    // computes square root of parameter; throws
    // NegativeNumberException if parameter is negative
    public static double SquareRoot(double value)
    {
        // if negative operand, throw NegativeNumberException
        if (value < 0)
        {
            throw new NegativeNumberException(
                "Square root of negative number not permitted");
        }
        else
        {
            return Math.Sqrt(value); // compute square root
        }
    }
}
```

```
Enter a value to calculate the square root of: 30
The square root of 30 is 5.477226
```

```
Enter a value to calculate the square root of: hello

Input string was not in a correct format.
Please enter a double value.

Enter a value to calculate the square root of: 25
The square root of 25 is 5.000000
```

```
Enter a value to calculate the square root of: -2
Square root of negative number not permitted
Please enter a non-negative value.

Enter a value to calculate the square root of: 2
The square root of 2 is 1.414214
```

**Fig. 13.7** | Demonstrating a user-defined exception class.

When the user inputs a value, the try statement (lines 14–34) attempts to invoke SquareRoot using the value input by the user. If the user input is not a number, a FormatException occurs, and the catch block in lines 25–29 processes the exception. If the user inputs a negative number, method SquareRoot throws a NegativeNumberException (lines 45–46); the catch block in lines 30–34 catches and handles this type of exception.

## 13.9 Checking for null References; Introducing C# 6's ?. Operator

In Section 13.6, we showed the following code snippet:

```
{
    var exampleObject = new ExampleClass();
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
}
```

The if statement in the preceding finally block ensures that if exampleObject is null, the call to Dispose is skipped, thus preventing a NullReferenceException.

> **Error-Prevention Tip 13.6**
> Always ensure that a reference is not null before using it to call a method or access a property of an object.

### 13.9.1 Null-Conditional Operator (?.)

C# 6's new null-conditional operator (?.) provides a more elegant way to check for null. The following statement replaces the four-line if statement above:

```
exampleObject?.Dispose();
```

In this statement, Dispose is called only if exampleObject is not null—exactly as in the preceding if statement.

### 13.9.2 Revisiting Operators is and as

In Section 12.5.6, we introduced downcasting with the is operator and mentioned that downcasting can cause InvalidCastExceptions. We then mentioned that you can avoid the InvalidCastException by using the as operator as follows:

```
var employee = currentEmployee as BasePlusCommissionEmployee;
```

If currentEmployee is a BasePlusCommissionEmployee, employee is assigned the BasePlusCommissionEmployee; otherwise, it's assigned null. Since employee could be null, you must ensure that it's not null before using it. For example, to give the BasePlusCommissionEmployee a 10% raise, we could use the statement

```
employee?.BaseSalary *= 1.10M;
```

which accesses and modifies the BaseSalary property only if employee is not null.

### 13.9.3 Nullable Types

Suppose you'd like to capture the value of the expression employee?.BaseSalary, as in

```
decimal salary = employee?.BaseSalary;
```

This statement actually results in a compilation error indicating that you cannot implicitly convert type decimal? to type decimal.

Normally a value-type variable cannot be assigned null. Because the employee reference might be null, the expression

```
employee?.BaseSalary
```

returns a nullable type—a value type that also can be null. You specify a nullable type by following a value type's name with a question mark (?)—so decimal? represents a nullable decimal. The statement

```
decimal? salary = employee?.BaseSalary;
```

indicates that salary either will be null or the employee's BaseSalary.

Nullable types have the following capabilities for accessing their underlying values:

- The GetValueOrDefault method checks whether a nullable-type variable contains a value. If so, the method returns that value; otherwise, it returns the value type's default value. An overload of this method receives one argument that enables you to specify a custom default value.
- The HasValue property returns true if a nullable-type variable contains a value; otherwise, it returns false.
- The Value property returns the nullable-type variable's underlying value or throws an InvalidOperationException if the underlying value is null.

Variables of nullable types also may be used as the left operand of the null-conditional operator (?.) or the null coalescing operator (??—discussed in the next section).

> **Error-Prevention Tip 13.7**
> Before using a nullable-type variable's Value property, use the HasValue property to check whether the variable has a value. If the nullable-type variable is null, accessing Value results in an InvalidOperationException.
