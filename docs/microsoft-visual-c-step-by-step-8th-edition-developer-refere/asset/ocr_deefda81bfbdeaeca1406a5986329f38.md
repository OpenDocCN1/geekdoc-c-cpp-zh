Click here to view code image

```
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
    ...
}
```

A catch handler employs syntax similar to that used by a method parameter to specify the exception to be caught. In the preceding example, when a FormatException is thrown, the fEx variable is populated with an object containing the details of the exception.

The FormatException type has a number of properties that you can examine to determine the exact cause of the exception. Many of these properties are common to all exceptions. For example, the Message property contains a text description of the error that caused the exception. You can use this information when handling the exception, perhaps recording the details in a log file or displaying a meaningful message to the user and then asking the user to try again.

# Unhandled exceptions

What happens if a try block throws an exception and there is no corresponding catch handler? In the previous example, it is possible that the lhsOperand text box could contain the string representation of a valid integer but the integer it represents is outside the range of valid integers supported by C# (for example, “2147483648”). In this case, the int.Parse statement would throw an OverflowException, which will not be caught by the FormatException catch handler. If this occurs and the try block is part of a method, the method immediately exits and execution returns to the calling method. If the calling method uses a try block, the runtime attempts to locate a matching catch handler for this try block and execute it. If the calling method does not use a try block or there is no matching catch handler, the calling method immediately exits and execution returns to its caller, where the process is repeated. If a matching catch handler is eventually found, the handler runs and execution continues with the first statement that follows the catch handler in the catching method.