![](bbox=[0.173, 0.095, 0.237, 0.146])

Also, had the last `catch` clause (`catch (System.Exception)`) been listed first, C# would issue a syntax error for the second `catch` clause indicating “A previous `catch` clause already catches all exceptions of this or a super type.”

Remember that writing the `catch` clause without an argument list is the same as writing `catch (System.Exception)`, which is the base of all exceptions. The last `catch` clause catches all other exceptions. If any exceptions other than `FloatingPtDivisionException` are encountered, `System.Exception` is thrown.

# Throwing an Exception

In the `GetResults()` method that tested the programmer-defined custom exception, an exception object is instantiated when “an exceptional condition occurs.” This exceptional condition is (`value2 < .0000001`). It could be any condition, but it should be one that happens very infrequently. After an object (`excepObj`) of the `FloatingPtDivisionException` class is instantiated with a string value of “Exception type: Floating-point division by zero”, the `excepObj` object is thrown. The `GetResults()` method is presented again in Example 12-8 for your review.

# Example 12-8

```
```csharp
static double GetResults(double value1, double value2)
{
    if (value2 < .0000001) // Be careful comparing floating-
                           // point values for equality.
    {
        FloatingPtDivisionException excepObj = new
            FloatingPtDivisionException
                ("Exception type: " +
                 "Floating-point division by zero");
        throw excepObj;
    }
    return value1 / value2;
}
```
```

The CLR is not throwing the exception here. Instead, the exception is thrown by the program using the `throw` keyword. When the `object` excepObj is thrown in the `GetResults()` method, the exception object propagates back up the call chain, first stopping at the method that called it to see if a `catch` is available to handle it. As you examine Example 12-7, notice that the `GetResults()` method was called from within the `try` block in the `Main()` method. When the `object` excepObj is thrown in `GetResults()`, it is thrown back to the `Main()` method’s `catch` clause because that is the position from which it was called.