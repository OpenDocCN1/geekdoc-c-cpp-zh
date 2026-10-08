# 194 Can I Get an Exceptional?

```
// Here's the exception handler.
try {
    // Call factorial in a loop from 6 down to -6.
    for (int i = 6; i > -6; i--)
    {
        // Calculate the factorial of the number,
        int factorial = MyMathFunctions.Factorial(i);
    }
    // Display the result of each pass.
    Console.WriteLine("i = {}, factorial = (1)**",
        factorial);
    }
} catch (ArgumentException e) {
    // This is a "just-chance" exception handler -- the buck stops at Main.
    // Probably all you can do here is alert the user before quitting.
    Console.WriteLine("Fatal error:");
    // When you're ready to release the program, change this
    // output to something in plain English, preferably with guide-
    // lines for what to do about the problem.
    Console.WriteLine(e.ToString());
}
// Wait for user to acknowledge.
Console.WriteLine("Press Enter to terminate...\*");
Console.Read();
}
```

This "exceptional" version of Main() wraps almost its entire contents in a try block. The catch block at the end of Main() catches the ArgumentException object and uses its ToString() to display most of the error information contained within the exception object in a single string.

I chose to use ArgumentException here because it most accurately describes the problem: an unacceptable argument to Factorial().

# Knowing what makes the example exceptional

The version of the Factorial() method in the preceding section includes the same check for a negative argument as the previous version. (The test for an integer is no longer relevant because we changed the Factorial() parameter and returns to int.) If its argument is negative, Factorial() can't continue, it formats an error message that describes the problem, including the value found to be offensive. Factorial() then bundles this information into a newly created ArgumentException object, which it throws back to the calling method.

I recommend running the program in the debugger to watch the exception occur in real time. (I tell you more about the debugger in Book IV.)

![](bbox=[0.145, 0.633, 0.233, 0.933])