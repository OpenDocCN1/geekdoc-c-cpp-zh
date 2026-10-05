
In this final chapter of Part I, you'll learn how C# uses exceptions to signal that an error has occurred and how to use the try, catch, and finally statements to catch and handle the errors that these exceptions represent. By the end of this chapter, you'll have a solid foundation in all the fundamental elements of C#; and you'll build on that foundation in Part II.

# Trying code and catching exceptions

It's very difficult to ensure that a piece of code always works as expected. Failures can occur for numerous reasons, many of which are beyond your control as a programmer. Any applications that you write must be capable of detecting failures and gracefully handling them, either by taking the appropriate corrective actions or, if that's not possible, by reporting the reasons for the failure in the clearest possible way to the.

Errors can happen at any time. Using traditional techniques to manually add error-detecting code around every statement is time-consuming, and itself-prone. You can also lose sight of the main flow of an application if each statement requires confronted error-handling logic to manage each possible error that can occur at every stage.

Fortunately, C# makes it easy to separate the error-handling code from the code that implements the primary logic of a program by using exceptions and exception handlers. To write exception-aware programs, you need to do two things:

- Write your code within a try block (try is a C# keyword). When the code runs, it attempts to catch all the statements in the try block, and if none of the statements generate an error, they all run, one after the other, to completion. If an error condition occurs, exception jumps out of the try block and into another piece of code designed to catch and handle the exception: a catch handler.

- Write one or more catch handlers (catch is another C# keyword) immediately after the try block to handle any possible error conditions. A catch handler is intended to capture and handle a specific type of exception. You can have multiple catch handlers after a try block, each one designed to trap and handle a specific exception. This enables you to provide different handlers for the different errors that could arise in the try block. If any one of the statements within the try block causes an error, the runtime throws an exception. The runtime then examines the catch handlers after the try block and transfers control directly to the first matching handler.

Here’s an example of a try block that contains code that attempts to convert strings that a user has typed in some boxes on a form to integer values. The code then calls a method to calculate a value and writes the result to another box. Converting a string to an integer requires that the string contain a valid set of digits and not some arbitrary sequence of characters. If the string contains invalid characters, the int.Parse method throws a FormatException and execution transfers to the corresponding catch handler. When the catch handler finishes, the program continues with the first statement that follows the handler. (If no handler corresponds to the exception, the exception is said unhandled; this situation will be described shortly.)

Click here to view code image

```csharp
try
{
    int leftHandSide = int.Parse(lhsOperand.Text);
    int rightHandSide = int.Parse(rhsOperand.Text);
    int answer = doCalculation(leftHandSide, rightHandSide);
    result.Text = answer.ToString();
}
catch (FormatException fEx)
{
    // Handle the exception
}
```

A catch handler employs syntax similar to that used by a method parameter to specify the exception to be caught. In the preceding example, when a FormatException is thrown, the fEx variable is populated with an object containing the details of the exception.

The FormatException type has several properties that you can examine to determine the exact cause of the exception. Many of these properties are common to all exceptions. For example, the Message property contains a text description of the error that caused the exception. You can use this information when handling the exception, perhaps recording the details in a log file or displaying a meaningful message to the user and asking the user to try again.

# Unhandled exceptions

What happens if a try block throws an exception and there’s no corresponding catch handler? In the previous example, it’s possible that the lhsOperand box could contain the string representation of a valid integer but the integer is outside the range of valid integers supported by C# (for example, "2147483648").

In this case, the int.Parse statement would throw an OverflowException, which will not be caught by the FormatException handler. If this occurs and the try block is part of a method, the method immediately exits and execution returns to the calling method. If the calling method uses a try block, the runtime attempts to locate and execute a catch handler for this try block. If the calling method does not use a try block or there is no matching catch handler, the calling method immediately exits, and execution returns to its caller, where the process is repeated. If a matching catch handler is eventually found, the handler runs and execution continues with the first statement that follows the catch handler in the catching method.

# Important

Notice that after catching an exception, execution continues in the method containing the catch block that caught the exception. If the exception occurred in a method other than the one containing the catch handler, control does not return to the method that caused the exception.

If, after cascading back through the list of calling methods, the runtime is unable to find a matching catch handler, the program will terminate with an unhandled exception.

You can easily examine exceptions generated by your application. If you're running the application in Microsoft Visual Studio 2022 in debug mode (that is, the Debug menu, you selected Start Debugging to run the application) and an exception occurs, a dialog similar to the one shown here appears, and the application pauses, helping you determine the cause of the exception.

[Note: The following text in the OCR appears to be corrupted/metadata from a UI element, which has been omitted or filtered based on the instruction to provide clean content.]

# Catch multiple exceptions

The exception-catching mechanism provided by C# and .NET is quite comprehensive. The .NET libraries define many types of exceptions, and any programs you write can catch most of them.

It's highly unlikely that you'll want to write catch handlers for every possible exception that your code can catch. Remember, your application must be able to handle exceptions that you never considered when you wrote it! So, how do you ensure that your programs catch and handle all possible exceptions?

The answer to this question lies in the different exceptions related to one another. Exceptions are organized into families called inheritance hierarchies. (You'll learn about inheritance in Chapter 12, "Working with inheritance.") FormatException and OverflowException both belong to a family called SystemException, as do a number of other exceptions. SystemException is itself a member of a wider family simply called Exception, and this is the great
