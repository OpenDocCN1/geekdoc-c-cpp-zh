
The behavior starting in C# 2.0 varies slightly from the earlier C# behavior. In C# 2.0, if a language allows throwing non-System.Exceptions, the object of the thrown exception will be wrapped in a System.Runtime.CompilerServices.RuntimeWrappedException that does derive from System.Exception. Therefore, all exceptions, whether derived from System.Exception or not, will propagate into C# assemblies as if they were derived from System.Exception.

The result is that System.Exception catch blocks will catch all exceptions not caught by earlier blocks, and a general catch block, following a System.Exception catch block, will never be invoked. Consequently, following a System.Exception catch block with a general catch block in C# 2.0 or later will result in a compiler warning indicating that the general catch block will never execute.

## Guidelines

- AVOID general catch blocks and replace them with a catch of System.Exception.
- AVOID catching exceptions for which the appropriate action is unknown. It is better to let an exception go unhandled than to handle it incorrectly.
- AVOID catching and logging an exception before rethrowing it. Instead, allow the exception to escape until it can be handled appropriately.

## Reporting Errors Using a throw Statement

C# allows developers to throw exceptions from their code, as demonstrated in Listing 4.24 and Output 4.15.

### LISTING 4.24: Throwing an Exception

```
using System;
public class ThrowingExceptions
{
    public static void Main()
    {
        try
        {
            Console.WriteLine("Begin executing");
            Console.WriteLine("Throw exception");
            throw new Exception("Arbitrary exception");
            Console.WriteLine("End executing");
        }
        catch(FormatException exception)
        {
            Console.WriteLine(
            "A FormatException was thrown");
        }
        catch(Exception exception)
        {
            Console.WriteLine(
            $"Unexpected error: { exception.Message }");
        }
        catch
        {
            Console.WriteLine("Unexpected error!");
        }
        Console.WriteLine(
        "Shutting down...");
    }
}
```

### OUTPUT 4.15

```
Begin executing
Throw exception...
Unexpected error:  Arbitrary exception
Shutting down...
```

As the arrows in Listing 4.24 depict, throwing an exception causes execution to jump from where the exception is thrown into the first catch block within the stack that is compatible with the thrown exception type.⁵ In this case, the second catch block handles the exception and writes out an error message. In Listing 4.24, there is no finally block, so execution falls through to the System.Console.WriteLine() statement following the try/catch block.

To throw an exception, it is necessary to have an instance of an exception. Listing 4.24 creates an instance using the keyword new followed by the type of the exception. Most exception types allow a message to be generated as part of throwing the exception, so that when the exception occurs, the message can be retrieved.

5. Technically, it could be caught by a compatible catch filter as well.

Sometimes a catch block will trap an exception but be unable to handle it appropriately or fully. In these circumstances, a catch block can rethrow the exception using the throw statement without specifying any exception, as shown in Listing 4.25.

### LISTING 4.25: Rethrowing an Exception

```
catch(Exception exception)
{
    Console.WriteLine(
        $@"Rethrowing unexpected error: { exception.Message }");
    throw;
}
```

In Listing 4.25, the throw statement is “empty” rather than specifying that the exception referred to by the exception variable is to be thrown. This illustrates a subtle difference: throw; preserves the “call stack” information in the exception, whereas throw exception; replaces that information with the current call stack information. For debugging purposes, it is usually better to know the original call stack.

## Guidelines

- DO prefer using an empty throw when catching and rethrowing an exception so as to preserve the call stack.
- DO report execution failures by throwing exceptions rather than returning error codes.
- DO NOT have public members that return exceptions as return values or an out parameter. Throw exceptions to indicate errors; do not use them as return values to indicate errors.

## Avoid Using Exception Handling to Deal with Expected Situations

Developers should make an effort to avoid throwing exceptions for expected conditions or normal control flow. For example, developers should not expect users to enter valid text when specifying their age.⁶ Therefore,

> 6. In general, developers should expect their users to perform unexpected actions, and therefore they should code defensively to handle “stupid user tricks.”

instead of relying on an exception to validate data entered by the user, developers should provide a means of checking the data before attempting the conversion. (Better yet, they should prevent the user from entering invalid data in the first place.) Exceptions are designed specifically for tracking exceptional, unexpected, and potentially fatal situations. Using them for an unintended purpose such as expected situations will cause your code to be hard to read, understand, and maintain.

Additionally, like most languages, C# incurs a slight performance hit when throwing an exception—taking microseconds compared to the nanoseconds most operations take. This delay is generally not noticeable in human time—except when the exception goes unhandled. For example, when Listing 4.20 is executed and the user enters an invalid age, the exception is unhandled and there is a noticeable delay while the runtime searches the environment to see whether there is a debugger to load. Fortunately, slow performance when a program is shutting down isn’t generally a factor to be concerned with.

**Guidelines**

DO NOT use exceptions for handling normal, expected conditions; use them for exceptional, unexpected conditions.

## ADVANCED TOPIC

## Numeric Conversion with TryParse()

One of the problems with the Parse() method is that the only way to determine whether the conversion will be successful is to attempt the cast and then catch the exception if it doesn’t work. Because throwing an exception is a relatively expensive operation, it is better to attempt the conversion without exception handling. In the first release of C#, the only data type that enabled this behavior was a double method called double.TryParse(). However, the CLI added this method to all numeric primitive types in version 2.0. It requires the use of the out keyword because the return from the TryParse() function is a bool rather than the converted value. Listing 4.26 is a code snippet that demonstrates the conversion using int.TryParse().

### LISTING 4.26: Conversion Using int.TryParse()

```
if (int.TryParse(ageText, out age))
{
    Console.WriteLine(
        $"Hi { firstName }! "
        + $"You are { age*12 } months old.");
}
else
{
    Console.WriteLine(
        $"The age entered, { ageText }, is not valid.");
}
```

With the .NET Framework 4, a TryParse() method was also added to enum types.

With the TryParse() method, it is no longer necessary to include a try/catch block simply for the purpose of handling the string-to-numeric conversion.

## SUMMARY

This chapter discussed the details of declaring and calling methods, including the use of the keywords out and ref to pass variables rather than their values. In addition to method declaration, this chapter introduced exception handling.

Methods are a fundamental construct that is a key to writing readable code. Instead of writing large methods with lots of statements, you should use methods to create “paragraphs” within your code, whose lengths are roughly 10 or fewer statements. The process of breaking large functions into smaller pieces is one of the ways you can refactor your code to make it more readable and maintainable.

The next chapter considers the class construct and describes how it encapsulates methods (behavior) and fields (data) into a single unit.
