```
Enter a value to calculate the square root of: -2
Square root of negative number not permitted
Please enter a non-negative value.

Enter a value to calculate the square root of: 2
The square root of 2 is 1.414214
```

Fig. 13.7 | Demonstrating a user-defined exception class. (Part 3 of 3.)

When the user inputs a value, the try statement (lines 14–34) attempts to invoke SquareRoot using the value input by the user. If the user input is not a number, a FormatException occurs, and the catch block in lines 25–29 processes the exception. If the user inputs a negative number, method SquareRoot throws a NegativeNumberException (lines 45–46); the catch block in lines 30–34 catches and handles this type of exception.

# 13.9 Checking for null References; Introducing C# 6's ?. Operator

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

Error-Prevention Tip 13.6
Always ensure that a reference is not null before using it to call a method or access a property of an object.

# 13.9.1 Null-Conditional Operator (?. )

C# 6's new null-conditional operator (?.) provides a more elegant way to check for null. The following statement replaces the four-line if statement above:

```
exampleObject?.Dispose();
```

In this statement, Dispose is called only if exampleObject is not null—exactly as in the preceding if statement.