
error. Alternatively, you might choose to derive your own custom Exception object that describes the error condition in the context of your application.

Suppose that the user next types a number that is not between 0 and 5. The number is picked up by the if statement and an IndexOutOfRangeException object is instantiated and thrown. At this point, the application immediately exits the try block and hunts for a catch block that handles IndexOutOfRangeException. The first catch block it encounters is this:

```csharp
catch (IndexOutOfRangeException ex)
{
    WriteLine($"Exception: Number should be between 0 and 5. {ex.Message}");
}
```

Because this catch block takes a parameter of the appropriate class, the catch block receives the exception instance and is executed. In this case, you display an error message and the Exception.Message property (which corresponds to the string passed to the IndexOutOfRangeException’s constructor). After executing this catch block, control then switches to the finally block, just as if no exception had occurred.

Notice that in the example you have also provided another catch block:

```csharp
catch (Exception ex)
{
    WriteLine($"An exception was thrown. Message was: {ex.Message}");
}
```

This catch block would also be capable of handling an IndexOutOfRangeException if it weren’t for the fact that such exceptions will already have been caught by the previous catch block. A reference to a base class can also refer to any instances of classes derived from it, and all exceptions are derived from Exception. This catch block isn’t executed when an exception of type IndexOutOfRangeException is thrown because the application executes only the first suitable catch block it finds from the list of available catch blocks. This second catch block catches other exceptions derived from the Exception base class. Be aware that the three separate calls to methods within the try block (Console.ReadLine, Console.Write, and Convert.ToInt32) might throw other exceptions.

If the user types something that is not a number—say a or hello—the Convert.ToInt32 method throws an exception of the class System.FormatException to indicate that the string passed into ToInt32 is not in a format that can be converted to an int. When this happens, the application traces back through the method calls, looking for a handler that can handle this exception. Your first catch block (the one that takes an `IndexOutOfRangeException`) will not do. The application then looks at the second `catch` block. This one will do because `FormatException` is derived from `Exception`, so a `FormatException` instance can be passed in as a parameter here.

The structure of the example is actually fairly typical of a situation with multiple `catch` blocks. You start with `catch` blocks that are designed to trap specific error conditions. Then, you finish with more general blocks that cover any errors for which you have not written specific error handlers. Indeed, the order of the `catch` blocks is important. Had you written the previous two blocks in the opposite order, the code would not have compiled, because the second `catch` block is unreachable (the `Exception catch` block would catch all exceptions). Therefore, the uppermost `catch` blocks should be the most granular options available, ending with the most general options.

Now that you have analyzed the code for the example, you can run it. The following output illustrates what happens with different inputs and demonstrates both the `IndexOutOfRangeException` and the `FormatException` being thrown:

```text
SimpleExceptions
Input a number between 0 and 5 (or just hit return to exit)> 4
Your number was 4
Thank you

Input a number between 0 and 5 (or just hit return to exit)> 0
Your number was 0
Thank you

Input a number between 0 and 5 (or just hit return to exit)> 10
Exception: Number should be between 0 and 5. You typed in 10
Thank you

Input a number between 0 and 5 (or just hit return to exit)>
hello
An exception was thrown. Message was: Input string was not in a correct format.
Thank you

Input a number between 0 and 5 (or just hit return to exit)>
Thank you
```

## Catching Exceptions from Other Code

The previous example demonstrates the handling of two exceptions. One of them, `IndexOutOfRangeException`, was thrown by your own code. The other, `FormatException`, was thrown from inside one of the base classes. It is very common for code in a library to throw an exception if it detects that a problem has occurred, or if one of the methods has been called inappropriately by being passed the wrong parameters. However, library code rarely attempts to catch exceptions; this is regarded as the responsibility of the client code.

Often, exceptions are thrown from the base class libraries while you are debugging. The process of debugging to some extent involves determining why exceptions have been thrown and removing the causes. Your aim should be to ensure that by the time the code is actually shipped, exceptions occur only in very exceptional circumstances and, if possible, are handled appropriately in your code.

## System.Exception Properties

The example illustrated the use of only the `Message` property of the exception object. However, a number of other properties are available in `System.Exception`, as shown in the following table.

| Property | Description |
|---|---|
| `Data` | Enables you to add key/value statements to the exception that can be used to supply extra information about it. |
| `HelpLink` | A link to a help file that provides more information about the exception. |
| `InnerException` | If this exception was thrown inside a `catch` block, then `InnerException` contains the exception object that sent the code into that `catch` block. |
| `Message` | Text that describes the error condition. |
| `Source` | The name of the application or object that caused the exception. |
| `StackTrace` | Provides details about the method calls on the stack (to help track down the method that threw the exception). |

The property value for `StackTrace` is supplied automatically by the .NET runtime if a stack trace is available. `Source` will always be filled in by the .NET runtime as the name of the assembly in which the exception was raised (though you might want to modify the property in your code to give more specific information), whereas `Data`, `Message`, `HelpLink`, and `InnerException` must be filled in by the code that threw the exception, by setting these properties immediately before throwing the exception. For example, the code to throw an exception might look something like this:

```csharp
if (ErrorCondition == true)
{
    var myException = new ClassMyException("Help!!!!");
    myException.Source = "My Application Name";
    myException.HelpLink = "MyHelpFile.txt";
    myException.Data["ErrorDate"] = DateTime.Now;
    myException.Data.Add("AdditionalInfo", "Contact Bill from the Blue Team");
    throw myException;
}
```

Here, `ClassMyException` is the name of the particular exception class you are throwing. Note that it is common practice for the names of all exception classes to end with `Exception`. In addition, note that the `Data` property is assigned in two possible ways.

## Exception Filters

A new feature of C# 6 is exception filters. You can have different catch blocks that act differently when catching different exception types. In some scenarios, it’s useful to have the catch blocks act differently based on the content of an exception. For example, when using the Windows runtime you often get COM exceptions for all different kinds of exceptions, or when doing network calls you get a network exception for many different scenarios—for example, if the server is not available, or the data supplied do not match the expectations. It’s good to react to these errors differently. Some exceptions can be recovered in different ways, while with others the user might need some information.

The following code sample throws the exception of type MyCustomException and sets the ErrorCode property of this exception (code file ExceptionFilters/Program.cs):

```csharp
public static void ThrowWithErrorCode(int code)
{
    throw new MyCustomException("Error in Foo") { ErrorCode = code };
}
```

In the Main method, the try block safeguards the method invocation with two catch blocks. The first catch block uses the when keyword to filter only exceptions if the ErrorCode property equals 405. The expression for the when clause needs to return a Boolean value. If the result is true, this catch block handles the exception. If it is false, other catches are looked for. Passing 405 to the method ThrowWithErrorCode, the filter returns true, and the first catch handles the exception. Passing another value, the filter returns false and the second catch handles the exception. With filters, you can have multiple handlers to handle the same exception type.

Of course you can also remove the second catch block and not handle the exception in that circumstance.

```csharp
try
{
    ThrowWithErrorCode(405);
}
catch (MyCustomException ex) when (ex.ErrorCode == 405)
{
    WriteLine($"Exception caught with filter {ex.Message} and {ex.ErrorCode}");
}
catch (MyCustomException ex)
{
    WriteLine($"Exception caught {ex.Message} and {ex.ErrorCode}");
}
```

## Re-throwing Exceptions
