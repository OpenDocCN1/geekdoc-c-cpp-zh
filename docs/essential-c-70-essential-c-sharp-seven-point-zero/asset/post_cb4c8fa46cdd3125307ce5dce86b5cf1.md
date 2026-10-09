
# 11 Exception Handling

Chapter 5 discussed using the try/catch/finally blocks for standard exception handling. In that chapter, the catch block always caught exceptions of type `System.Exception`. This chapter defines some additional details of exception handling—specifically, details surrounding additional exception types, defining custom exceptions, and multiple catch blocks for handling each type. This chapter also details exceptions because of their reliance on inheritance.

![](img/ef6a8a417630b222bfb3f3b949facff0_501_0.png)

### Multiple Exception Types

Listing 11.1 throws a `System.ArgumentException`, not the `System.Exception` type demonstrated in Chapter 5. C# allows code to throw any type that derives (perhaps indirectly) from `System.Exception`.

To throw an exception, you simply prefix the exception instance with the keyword `throw`. The type of exception used is obviously the type that best describes the circumstances surrounding the error that caused the exception.

For example, consider the `TextNumberParser.Parse()` method in Listing 11.1.

**LISTING 11.1: Throwing an Exception**

```csharp
public sealed class TextNumberParser
{
    public static int Parse(string textDigit)
    {
        string[] digitTexts =
            { "zero", "one", "two", "three", "four",
              "five", "six", "seven", "eight", "nine" };

        int result = Array.IndexOf(
            digitTexts,
            // Leveraging C# 2.0's null coalesce operator
            textDigit ??
            // Leveraging C# 7.0's throw expression
            throw new ArgumentNullException(nameof(textDigit))
            ).ToLower());
        if (result < 0)
        {
            // Leveraging C# 6.0's nameof operator
            throw new ArgumentException(
                "The argument did not represent a digit",
                nameof(textDigit));
        }

        return result;
    }
}
```

In the call to `Array.IndexOf()`, we leverage a C# 7.0 throw expression when the `textDigit` argument is null. Prior to C# 7.0, throw expressions were not allowed; only throw statements were allowed. As a result, two separate statements were required: one checking for null and the other to throw the exception. You could not embed the throw within the same statement as a null coalescing operator, for example.

Instead of throwing `System.Exception`, it is more appropriate to throw `ArgumentException` because the type itself indicates what went wrong and includes special parameters for identifying which parameter was at fault.

Two similar exceptions are `ArgumentNullException` and `NullReferenceException`. `ArgumentNullException` should be thrown for the inappropriate passing of null arguments. This is a special case of an invalid parameter exception that would more generally (when it isn't null) be thrown as an `ArgumentException` or an `ArgumentOutOfRangeException`. `NullReferenceException` is generally an exception that the underlying runtime will throw only with an attempt to dereference a null value—that is, an attempt to call a member on an object whose value is null. Instead of triggering a `NullReferenceException` to be thrown, programmers should check parameters for null before accessing them and then throw an `ArgumentNullException`, which can provide more contextual information, such as the parameter name. If there is an innocuous way to proceed even if an argument is null, be sure to use the C# 6.0 null propagation operator to avoid the runtime throwing a `NullReferenceException`.

One important characteristic of the argument exception types (including `ArgumentNullException`, `ArgumentException`, and `ArgumentOutOfRangeException`) is that each has a constructor parameter that allows identification of the argument name as a string. Prior to C# 6.0, this meant hardcoding a magic string (e.g., `"textDigit"`) to identify the parameter name. The problem with this approach is that if the parameter name ever changed, developers had to remember to update the magic string. Fortunately, C# 6.0 and later provides a `nameof` operator, which takes the parameter name identifier and generates the parameter name at compile time (see `nameof(textDigit)` in Listing 11.1). The advantage of this approach is that now the IDE can use refactoring tools (such as automatic renaming) to change the identifier everywhere, including when it is used as an argument to the `nameof` operator. Additionally, if the parameter name changes (without the use of a refactoring tool), the compiler will generate an error if the identifier passed to the `nameof` operator no longer exists. Moving forward, with C# 6.0 (and later), the general guideline is to always use the `nameof` operator for the parameter name of an argument type exception. Chapter 18 provides a full explanation for the `nameof` operator. Until then, it is sufficient to understand that `nameof` simply returns the name of the argument identified.

Several other exceptions are intended only for the runtime and derive (sometimes indirectly) from `System.SystemException`. They include `System.StackOverflowException`, `System.OutOfMemoryException`, `System.Runtime.InteropServices.COMException`, `System.ExecutionEngineException`, and `System.Runtime.InteropServices.SEHException`. Do not throw exceptions of these types. Similarly, you should avoid throwing a `System.Exception` or `System.ApplicationException`, as these exceptions are so general that they provide little indication of the cause of or resolution to the problem. Instead, throw the most derived exception that fits the scenario. Obviously, developers should avoid creating APIs that could potentially result in a system failure. However, if the executing code reaches a certain state such that continuing to execute is unsafe or unrecoverable, it should call `System.Environment.FailFast()`. This will immediately terminate the process after writing a message to the Windows Application event log, and will even include the message as part of Windows Error Reporting if the user so chooses.

### Guidelines

- **DO** throw an `ArgumentException` or one of its subtypes if bad arguments are passed to a member. Prefer the most derived exception type (e.g., `ArgumentNullException`), if applicable.
- **DO** set the `ParamName` property when throwing an `ArgumentException` or one of the subclasses.
- **DO** throw the most specific (most derived) exception that makes sense.
- **DO NOT** throw a `NullReferenceException`. Instead, throw `ArgumentNullException` when a value is unexpectedly null.
- **DO NOT** throw a `System.SystemException` or an exception type that derives from it.
- **DO NOT** throw a `System.Exception` or `System.ApplicationException`.
- **CONSIDER** terminating the process by calling `System.Environment.FailFast()` if the program encounters a scenario where it is unsafe for further execution.
- **DO** use `nameof` for the `paramName` argument passed into argument exception types that take such a parameter. Examples of such exceptions include `ArgumentException`, `ArgumentOutOfRangeException`, and `ArgumentNullException`.

### Catching Exceptions

Throwing a particular exception type enables the catcher to use the exception's type itself to identify the problem. It is not necessary, in other words, to catch the exception and use a switch statement on the exception message to determine which action to take in light of the exception. Instead, C# allows for multiple catch blocks, each targeting a specific exception type, as Listing 11.2 shows.

**LISTING 11.2: Catching Different Exception Types**

```csharp
using System;

public sealed class Program
{
    public static void Main(string[] args)
    {
        try
        {
            // ...
            throw new InvalidOperationException(
                "Arbitrary exception");
            // ...
        }
        catch (Win32Exception exception)
            when (exception.NativeErrorCode == 42)
        {
            // Handle Win32Exception where
            // ErrorCode is 42
        }
        catch (NullReferenceException exception)
        {
            // Handle NullReferenceException
        }
        catch (ArgumentException exception)
        {
            // Handle ArgumentException
        }
        catch (InvalidOperationException exception)
        {
            bool exceptionHandled = false;
            // Handle InvalidOperationException
            // ...
            if (exceptionHandled)
            {
                throw;
            }
        }
    }
}
```
