# **LISTING 10.2** Catching Multiple Exceptions

```
```csharp
try
{
    int divisor = Convert.ToInt32(Console.ReadLine());
    int result = 3/divisor;
}
catch (DivideByZeroException)
{
    Console.WriteLine("Attempted to divide by zero");
}
catch (FormatException)
{
    Console.WriteLine("Input was not in the correct format");
}
catch (Exception)
{
    Console.WriteLine("General catch handler");
}
```
```

If the try block in Listing 10.2 resulted in a DivideByZeroException, the output would be "Attempted to divide by zero". If the try block resulted in a FormatException, the output would be "Input was not in the correct format". Any other exceptions would generate "General catch handler" as the output. However, if the catch blocks were rearranged so the general catch block came first, the program would fail to compile.

# Swallowing Exceptions

It is common to write catch blocks that do nothing more than log the error. Although this is sometimes important, it can usually be done by the top-level caller and does not need to occur for every function.

This leads to a problem known as "swallowing exceptions," and occurs when you catch an exception and either do nothing with it or don't allow it to pass up the chain. This can also lead to problems because you are effectively hiding the exception and not doing anything with it, which can lead to intermittent problems that will be hard to track.

The best way to look at this situation is that you should catch an exception only if you have meaningful cleanup work that needs to be done as a result of the exception (such as closing files or database connections).

Remember, a catch handler executes only if an exception has occurred, so it should not be used for cleanup activities. If you do need to perform any type of cleanup activities, they should be done in a finally handler. This means that unless you can legitimately take some action because of an exception, you should use the try-finally pattern instead of the try-catch or try-catch-finally patterns.