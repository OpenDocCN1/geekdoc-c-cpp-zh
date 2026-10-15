```
finally
{
Console.WriteLine("Result is : " +div);
Console.ReadLine();
}
```

In the preceding code snippet, when the statement inside the try block executes, the control may transfer to catch block depending upon the value of the number variable. Suppose, the value of the number variable is then DivideByZeroException is raised and the program control transfers to the catch block and executes the statements inside the catch block and after that the statements inside the finally block are executed. If value of the number variable is other than zero, then the program control is not transferred to the catch block is then directly transferred to the finally block and statements inside the finally block are executed.

# The throw Statement

The throw statement is used to raise an exception in case an error occurs in a program. In C#, it is also possible to throw an exception programmatically. You can use the throw keyword to throw an exception. The following code snippet shows an example of the throw statement:

```
try
{
throw new DivideByZeroException();
}
catch(DivideByZeroException e)
{
Console.WriteLine("Exception");
}
```

In the preceding code snippet, you can see that we have thrown a new DivideByZeroException explicitly.

# Checked and Unchecked Statements

Checked and unchecked statements are used to check the memory overflow exceptions. The checked keyword is used to check the overflow for integral-type arithmetic operations and conversions. Overflow occurs when the value of a variable exceeds the required original length of the variable. The unchecked keyword ignores the overflow-checking of the integral-type arithmetic operations and conversions. Arithmetic overflow exceptions are raised in a checked context; whereas, in case of unchecked context, arithmetic overflow is ignored and the program displays the truncated integers from the result.

The following code snippet shows an example of checked and unchecked statements:

```
byte number1, number2;
byte result;
number1 = 127;
number2 = 127;
try
{
result = unchecked((byte)(number1 * number2));
Console.WriteLine("Unchecked result: " + result);
result = checked((byte)(number1 * number2));
Console.WriteLine("checked result: " + result);
}
catch (OverflowException exc)
{
Console.WriteLine(exc);
}
```

In the preceding code snippet, you can see that the OverflowException class is used to catch the overflow exception.

Let’s now move towards the Immediate Solutions section to see the practical implementation of the concepts discussed in the In Depth section.