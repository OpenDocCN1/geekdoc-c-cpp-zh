
## The syntax for a try-catch statement that accesses the exception

```
try { statements }
catch(ExceptionClass exceptionName) { statements }
```

## Two common properties for all exceptions

| Property | Description |
|---|---|
| Message | Gets a message that briefly describes the current exception. |
| StackTrace | Gets a string that lists the methods that were called before the exception occurred. |

## A common method for all exceptions

| Method | Description |
|---|---|
| GetType() | Gets the type of the current exception. |

## A try-catch statement that accesses the exception

```
try
{
    decimal subtotal = Convert.ToDecimal(txtSubtotal.Text);
}
catch(Exception ex)
{
    MessageBox.Show(ex.Message + "\n\n" + ex.GetType().ToString() + "\n" + ex.StackTrace, "Exception");
}
```

## The dialog box that’s displayed if an exception occurs

![](img/844f608d10a44654833ea5efc8a2e7a7_226_0.png)

## Description

- If you want to use the properties or methods of the exception in the catch block, you must supply a name for the exception.
- The stack trace is a list of the methods that were called before the exception occurred. The list appears in reverse order, from the last method called to the first method called.

## Note

- If you’re coding the try-catch statement within an event handler, you can’t use e for the name of the exception because it’s used as the name of a parameter for the handler.

## How to catch specific types of exceptions

In some cases, the statements in the try block of a try-catch statement can throw more than one type of exception. Then, you may want to handle each exception differently. To do that, you can code catch blocks like the ones shown in figure 7-5. Here, the first catch block catches a FormatException, the second catch block catches an OverflowException, and the third catch block catches any other exceptions.

When you catch specific exceptions, you should realize that you must code the catch blocks for the most specific exceptions in a class hierarchy first, and you must code the catch blocks for the least specific exceptions last. In this figure, for example, the FormatException type and the OverflowException type are both specific than the Exception type. As a result, their catch blocks must be coded before the catch block for the Exception type. If they were coded after the Exception type, you would get a build error when you tried to compile the project. That’s because the catch blocks are evaluated in sequence, which means that the catch block for the Exception type would catch any exception that occurred. In other words, the other catch blocks would never be executed.

Although you have to code the catch blocks for the FormatException and OverflowException types before the catch block for the Exception type, you don’t have to code the catch block for the FormatException type before the OverflowException type. That’s because the OverflowException class is a subclass of the ArithmeticException class, not the FormatException class. In other words, the least specific exception to most specific exception rule applies only within subclasses that are based on the same class.

When you code try-catch statements, you may find that you have some code that should run regardless of whether an exception is thrown or what type of exception is thrown. For example, if your application is using system resources such as database connections, it’s common to perform some cleanup code that releases those resources when they’re no longer needed. Instead of including this code in the try block and each catch block, you can code it in a finally block. Then, this code is executed after all of the statements in the try block are executed. Or, if an exception is thrown, it’s executed after the statements in the catch block. This allows you to store cleanup code in a single location instead of multiple locations, which results in code that’s easier to read and maintain.

## The syntax for a try-catch statement that catches specific types of exceptions

```
```csharp
try { statements }
[catch(MostSpecificException [exceptionName]) { statements } ]...
[catch(NextMostSpecificException [exceptionName]) { statements } ]...
[catch([LeastSpecificException [exceptionName]]) { statements }]
[finally { statements }]
```
```

## A try-catch statement that catches two specific exceptions

```
```csharp
try
{
    decimal monthlyInvestment =
        Convert.ToDecimal(txtMonthlyInvestment.Text);
    decimal yearlyInterestRate =
        Convert.ToDecimal(txtInterestRate.Text);
    int years = Convert.ToInt32(txtYears.Text);
}
catch(FormatException)        // a specific exception
{
    MessageBox.Show(
        "A format exception has occurred. Please check all entries.",
        "Entry Error");
}
catch(OverflowException)      // another specific exception
{
    MessageBox.Show(
        "An overflow exception has occurred. Please enter smaller values.",
        "Entry Error");
}
catch(Exception ex)           // all other exceptions
{
    MessageBox.Show(ex.Message, ex.GetType().ToString());
}
finally      // this code runs whether or not an exception occurs
{
    PerformCleanup();
}
```
```

## Description

- You can code one catch block for each type of exception that may occur in the try block. If you code more than one catch block, you must code the catch blocks for the most specific types of exceptions first.
- Since all exceptions are subclasses of the Exception class, a catch block for the Exception class will catch all types of exceptions.
- You can code a *finally* block after all the catch blocks. The code in this block is executed whether or not an exception occurs. It’s often used to free any system resources.

![](img/844f608d10a44654833ea5efc8a2e7a7_228_0.png)

## How to throw an exception

Now that you’ve learned how to catch exceptions, you’re ready to learn how to throw exceptions from the methods that you code. To do that, you can use the throw statement as shown in figure 7-6. As you can see, you can use this statement either to throw a new exception or to throw an existing exception.

To throw a new exception, you code the throw keyword followed by the new keyword and the name of the exception class you want to create the exception from. (As you’ll see later in this book, the new keyword is the keyword that’s used to create an object from a class.) When you do that, you can also supply a string argument that provides a brief description of the exception. This argument is assigned to the Message property of the exception. Then, when you handle the exception, you can use the Message property to get this string.

This use of the throw statement is illustrated in the first example in this figure. Here, before performing its calculation, the CalculateFutureValue() method checks if the values used in the calculation are less than or equal to zero. If so, an exception that’s created from the Exception class is thrown. Both of the throw statements shown here include a string that briefly describes the cause of the exception.

In general, you should throw an exception only when a truly exceptional condition occurs. In the first example, the CalculateFutureValue() method can’t perform the calculation when it receives a negative number. As a result, this is an exceptional condition, and it makes sense to throw an exception. Another way to handle this situation would be to return a negative decimal value (such as -1.0m) to indicate that the calculation can’t be performed. However, throwing an exception allows you to provide a description of the exceptional condition, which is often helpful to other programmers who might want to use this method.

You can also use the throw statement to test an exception handling routine as shown in the second example. Here, the throw statement is coded within the try block of a try-catch statement. Then, when this statement is executed, the code within the catch block is executed so you can be sure that it works properly.

The third example in this figure shows how to throw an existing exception. This technique is useful if you need to catch an exception, perform some processing that partially handles the exception, and then throw the exception again so another exception handler can finish handling the exception. In this case, the ToDecimal() method is used within a try block to convert the value the user enters into a text box to a decimal. If the user enters a value that’s not a valid decimal, a FormatException is thrown. Then, the catch block catches this exception, moves the focus to the text box, and rethrows the exception. That way, the calling method can also catch the exception and perform some additional processing.

With C# 7.0, you can also throw an exception using a throw expression. Throw expressions are written just like throw statements, but they can be used in some contexts where throw statements can’t be used. For example they can be used in a null-coalescing expression as shown in the last example in this figure. They can also be used in conditional expressions like the ones you learned about
