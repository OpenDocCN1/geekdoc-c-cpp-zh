# 61. DEFINING HELPER METHODS INSIDE METHODS (LOCAL FUNCTIONS)

Local functions in C# are methods declared inside another method. They're useful for isolating helper logic that doesn't need to be exposed outside the containing method.

Here’s a simple example showing how a local function is defined and used inside another method.

[Code Example]

```
using System;

class Program
{
    static void Main()
    {
        int number = 5;

        // Call the method that uses a local function
        int result = CalculateFactorial(number);
        Console.WriteLine($"Factorial of {number} is {result}");
    }

    static int CalculateFactorial(int n)
    {
        // Local function defined inside the method

        int Factorial(int x)
        {
            if (x <= 1) return 1;
            return x * Factorial(x - 1); // Recursive call
        }

        return Factorial(n); // Calling the local function
    }
}
```