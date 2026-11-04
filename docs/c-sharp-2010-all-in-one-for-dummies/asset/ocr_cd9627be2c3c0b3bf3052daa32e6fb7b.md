```
```csharp
// 1a -- Retrieve the principal.
principal = InputPositiveDecimal("principal");
// 1b -- Now enter the interest rate.
interest = InputPositiveDecimal("interest");
// 1c -- Finally, the duration.
duration = InputPositiveDecimal("duration");
// InputPositiveDecimal -- Return a positive decimal number
// from the keyboard.
public static decimal InputPositiveDecimal(string prompt)
{
    // Keep trying until the user gets it right.
    while(true)
    {
        // Prompt the user for input.
        Console.Write("Enter " + prompt + ": ");
        // Retrieve a decimal value from the keyboard.
        string input = Console.ReadLine();
        decimal value = Convert.ToDecimal(input);
        // Exit the loop if the value that's entered is correct.
        if (value >= 0)
        {
            // Return the valid decimal value entered by the user.
            return value;
        }
        // Otherwise, generate an error on incorrect input.
        Console.WriteLine(prompt + " cannot be negative");
        Console.WriteLine("Try again");
        Console.WriteLine();
    }
}
// OutputInterestTable -- Given the principal and interest,
// generate a future value table for the number of periods
// indicated in duration. (Implements Section 3.)
public static void OutputInterestTable(decimal principal,
    decimal interest,
    decimal duration)
{
    for (int year = 1; year <= duration; year++)
    {
        // Calculate the value of the principal plus interest.
        decimal interestPaid;
        interestPaid = principal * (interest / 100);
        // Now calculate the new principal by adding
        // the interest to the previous principal.
        principal = principal + interestPaid;
        // Round off the principal to the nearest cent.
        principal = decimal.Round(principal, 2);
        // Output the result.
        Console.WriteLine(year + " " + principal);
    }
}
```
```

I divided the Main() method into three clearly distinguishable parts, each marked with boldfaced comments. I further divided the first section into subsections labeled 1a, 1b, and 1c.