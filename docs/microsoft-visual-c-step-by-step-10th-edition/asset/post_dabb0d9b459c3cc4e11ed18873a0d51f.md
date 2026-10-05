
granddaddy of all exceptions. If you catch Exception, the handler traps every possible exception that can occur.

> Note
> The family includes a wide variety of exceptions, many of which are intended for use by various parts of .NET. Some of these exceptions are somewhat esoteric, but it's still useful to understand how to catch them.

The next example shows how to catch all possible exceptions:

Click here to view code image

```
try
{
    int leftHandSide = int.Parse(lhsOperand.Text);
    int rightHandSide = int.Parse(rhsOperand.Text);
    int answer = doCalculation(leftHandSide, rightHandSide);
    result.Text = answer.ToString();
}
catch (Exception ex) // this is a general catch handler
{
    //...
}
```

> Note
> If you want to catch Exception, you can actually omit its name from the catch handler because it is the default exception:

```
catch
{
    // ...
}
```

However, this is not recommended. The exception object passed to the catch handler can contain useful information concerning the exception, which is not easily accessible when using this version of the catch construct.

There's one final question you should be asking at this point: What happens if the same exception matches multiple catch handlers at the end of a try block? For example, if you catch FormatException and Exception in two different handlers, which one will run? (Or will both execute)?

When an exception occurs, the runtime uses the first handler that matches the exception, and the others are ignored. So, if you place a handler for Exception before a handler for FormatException, the FormatException handler will never run. Therefore, you should place more specific catch handlers above a general catch handler after a try block. If one of the specific catch handlers matches the exception, the catch handler will win.

## Filtering exceptions

You can filter the exceptions that are matched against catch handlers to ensure that a catch handler is triggered only when additional conditions are met. These conditions take the form of a Boolean expression prefixed by the when keyword. This example illustrates the syntax:

Click here to view code image

```
bool catchErrors = ...;
try {
  ...
}
catch (Exception ex) when (catchErrors == true) {
  // Handle exceptions only if the catchErrors variable is true
}
```

This example catches all exceptions (the Exception type) depending on the value of the catchErrors Boolean variable. If this variable is false, then no exception occurs, and the default exception handling mechanism for the application is used. If catchErrors is true, then the code in the catch block runs to handle the exception.

In the following exercises, you will see what happens when an application throws an unhandled exception, and you'll write a try block to catch and handle an exception.

## To observe how the application reports unhandled exceptions

- 1. Start Visual Studio 2022, if it is not already running.
- 2. Open the MathOperators solution, which is located in the \Microsoft Press\VCSBS\Chapter 6\MathOperators folder in your Documents folder.

This is a version of the program from Chapter 2, “Working with variables, operators, and expressions,” that demonstrates the different arithmetic operators.
- 3. On the Debug menu, select Start Without Debugging.

> Note
> For this exercise, ensure that you actually run the application without debugging.

The form appears. You will now enter some text in the Left Operand box that will cause an exception. This operation will demonstrate the lack of robustness in this current version of the program.
- 4. In the Left Operand box, select John, and in the Right Operand box, type 2.
- 5. Select the - + Addition button, and then select Calculate.

This input triggers Windows default exception handling. The application simply terminates, and you are returned to the desktop without any explanation of what went wrong!

Now that you have seen how the application behaves when an unhandled exception occurs, the next step is to make the application more robust by handling invalid input and preventing unhandled exceptions from arising.

## To write a try/catch statement block

- 1. Return to Visual Studio 2022.
- 2. On the Debug menu, select Start Debugging.

> Note
> This time, make sure you run the application in debug mode.
- 3. When the form appears, in the Left Operand box, type John, and in the Right Operand box, type 2.
- 4. Select the + Addition button, and then select Calculate.

This input should cause the same exception that occurred in the previous exercise, except now you're running in debug mode, so Visual Studio traps the exception and reports it.

Visual Studio displays your code and highlights the statement that caused the exception. It also displays a dialog that describes the exception, which in this case is "Input string was not in a correct format"

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_267_0.png)

You can see that a FormatException was thrown by the call to int.Parse inside the addValues method. The problem is that this method is unable to parse the text John into a valid number.
- 5. In the Exception dialog, select View Details.

The QuickWatch dialog opens, in which you can view more details about the exception.

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_268_0.png)

> Tip
> Some exceptions are the result of other exceptions raised earlier. The exception reported by Visual Studio is just the final exception in this chain, but it's usually the earlier exceptions that highlight the real cause of the problem.
> You can drill into these earlier exceptions by expanding the InnerException property in the View Detail dialog. Inner exceptions might have further exceptions, so you should keep digging down until you find an exception with the InnerException property set to null (as shown in the previous image). At this point, you have reached the initial exception, and this exception typically highlights the problem you need to address.
- 6. Select Close in the QuickWatch dialog.
- 7. In Visual Studio, on the Debug menu, select Stop Debugging
- 8. Display the code for the file MainPage.xml.cs in the Code and Text Editor window, and locate the addValues method.
- 9. Add a try block (including braces) around the statements inside this method, together with a catch handler for the FormatException exception, as shown in the form:

Click here to view code image

```
try
{
  int lhs = int.Parse(lhsOperand.Text);
  int rhs = int.Parse(rhsOperand.Text);
  int outcome = 0;

  outcome = lhs + rhs;
  expression.Text = $"{lhs} + {rhs}";
  result.Text = outcome.ToString();
}
catch (FormatException fex)
{
  result.Text = fex.Message;
}
```

Now, if a FormatException exception occurs, the catch handler displays the text in the exception's Message property in the Result box at the bottom of the form.
- 10. On the Debug menu, select Start Debugging.
- 11. When the form appears, in the Left Operand box, type John, and in the Right Operand box type 2.
- 12. Select the + Addition button, and then select Calculate.

The catch handler successfully catches the FormatException, and the message “Input string was not in a correct format” is written to the Result box. The application is now a bit more robust.

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_270_0.png)
- 13. In the Left Operand box, replace John with the number 10. In the Right Operand box, type Sharp. Then select Calculate.
The try blocks the statements that parse both boxes, so the same exception handler handles user input errors in both boxes.
- 14. In the Right Operand box, replace Sharp with 20, select the + Addition button, and then select Calculate.
The application now works as expected and displays the value 30 in the Result box.
- 15. In the Left Operand box, replace 10 with John, select the – Subtraction button, and then select Calculate.
Visual Studio drops into the debugger and reports a `FormatException` exception again. This time, the error has occurred in the `subtractValues` method, which
