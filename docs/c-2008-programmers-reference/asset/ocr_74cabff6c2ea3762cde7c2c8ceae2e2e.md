(continued)

```
Console.WriteLine("The result of {0}/{1} is {2}", num1, num2, result);
Console.ReadLine();
}
}
```

In this example, there are several opportunities for exceptions to occur:

+   - If the user enters a noninteger value for num1 or num2.
+   - If the user enters a non-numeric value for num1 and num2.
+   - If num2 is zero, resulting in a division by zero error.

Figure 12-1 shows the program halting abruptly when the user enters 3.5 for num1.

![](bbox=[0.2, 0.54, 0.8, 0.82])

Figure 12-1

Hence, you need to anticipate all the possible scenarios and handle the exceptions gracefully.

# Handling Exceptions Using the try-catch Statement

In C#, you can use the try-catch statement to enclose a block of code statements that may potentially cause exceptions to be raised. You enclose these statements within the catch block and that block to catch the different types of exceptions that may occur.

Using the previous example, you can enclose the statements that ask the user to input num1 and num2 and then performs the division within a catch block. You then use the catch block to catch possible exceptions, like this:

```
static void Main(string[] args)
{
    int num1, num2, result;
    try
    {
```