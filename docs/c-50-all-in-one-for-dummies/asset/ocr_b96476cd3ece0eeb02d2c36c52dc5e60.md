```
int factorial = 1;

// Loop from value down to 1, each time multiplying
// the previous accumulator value by the result.
do
{
    factorial *= value;
} while(--value > 1);

// Return the accumulated value.
return factorial;
}
}

public class Program
{
public static void Main(string[] args)
{
// Here's the exception handler.
try
{
// Call factorial in a loop from 6 down to -6.
for (int i = 6; i > -6; i--)
{
// Calculate the factorial of the number.
int factorial = MyMathFunctions.Factorial(i);

// Display the result of each pass.
Console.WriteLine("i = {0}, factorial = {1}",
    i, factorial);
}
}
catch(ArgumentException e)
{
// This is a "last-chance" exception handler -- the buck stops at Main().
// Probably all you can do here is alert the user before quitting.
Console.WriteLine("Fatal error:");
// When you're ready to release the program, change this
// output to something in plain English, preferably with guide-
// lines for what to do about the problem.
Console.WriteLine(e.ToString());
}

// Wait for user to acknowledge.
Console.WriteLine("Press Enter to terminate...");
Console.Read();
}
}
```

This “exceptional” version of Main() wraps almost its entire contents in a try block. The catch block at the end of Main() catches the ArgumentException object and uses its ToString() method to display most of the error information contained within the exception object in a single string.

We chose to use ArgumentException here because it most accurately describes the problem: an unacceptable argument to Factorial().

![](bbox=[0.13, 0.84, 0.22, 0.96])