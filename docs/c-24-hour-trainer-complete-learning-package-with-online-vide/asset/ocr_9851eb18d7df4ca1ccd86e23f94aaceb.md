One way to make an assertion is to evaluate the statement and, if it is false, throw an exception.

That guarantees that the program cannot continue running if the assertion is false.

The following code shows a Factorial method with assertions. If the method's parameter is less than 0 or greater than 20, the code throws an exception:

```
```csharp
// Recursively calculate n!
private long Factorial(long n)
{
    // Validate the input.
    if ((n < 0) || (n > 20))
        throw new ArgumentOutOfRangeException(
            "n", "Factorial parameter must be between 0 and 20.");

    if (n == 1) return 1;
    return n * Factorial(n - 1);
}
```
```

To make this kind of assertion easier, the .NET Framework provides a Debug class. The Debug class's static Assert method takes as a parameter a boolean value. If the value is false, Assert displays an error message showing the program's stack dump at the time so you can figure out where the error occurred

The following code shows a new version of the factorial method that uses Debug.Assert. The optional second parameter to Debug.Assert gives a message that should be displayed if the assertion fails:

```
```csharp
// Recursively calculate n!
private long Factorial(long n)
{
    // Validate the input.
    Debug.Assert((n >= 0) && (n <= 20),
        "Factorial parameter must be between 0 and 20.");

    if (n == 1) return 1;
    return n * Factorial(n - 1);
}
```
```

> **NOTE** The Debug class is in the System.Diagnostics namespace. If you want to use it without including the namespace, as in the preceding code, you should include the following using directive at the top of the file:
> 
> ```csharp
> using System.Diagnostics;
> ```

Normally when you develop a program you make debug builds. These include extra debugging symbols so you can step through the code in the debugger. If you switch to a release build, those symbols are omitted, making the compiled program a bit smaller. The Debug.Assert method also has no effect in release builds.