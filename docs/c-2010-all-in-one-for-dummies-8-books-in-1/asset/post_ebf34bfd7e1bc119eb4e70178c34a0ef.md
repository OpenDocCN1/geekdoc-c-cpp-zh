
## Here We Go Loop-the-Loop 101

```csharp
// Prompt user to enter principal; keep prompting
// until the correct value is entered.
decimal principal;
while(true) {
    Console.Write("Enter principal: ");
    string principalInput = Console.ReadLine();
    principal = Convert.ToDecimal(principalInput);
    // Exit if the value is correct
    if (principal >= 0) {
        break;
    }
    // Generate an error on incorrect input.
    Console.WriteLine("Principal cannot be negative");
    Console.WriteLine("Try again");
    Console.WriteLine();
}
// Now enter the interest rate.
while(true) {
    Console.Write("Enter interest: ");
    string interestInput = Console.ReadLine();
    decimal interest = Convert.ToDecimal(interestInput);
    // Don't accept if interest is negative or too large
    if (interest >= 0 && interest <= maximumInterest) {
        break;
    }
    // generate an error message as well.
    Console.WriteLine("* cannot be negative or greater than " + maximumInterest);
    Console.WriteLine("Try again");
    Console.WriteLine();
}
// Both the principal and the interest appear to be
// final; Input the number of years.
Console.Write("Enter number of years: ");
string durationInput = Console.ReadLine();
int duration = Convert.ToInt32(durationInput);
// Verify the input.
Console.WriteLine("Skip a line.");
Console.WriteLine("Principal = " + principal);
Console.WriteLine("Interest = " + interest + "%");
Console.WriteLine("Duration = " + duration + " years");
Console.WriteLine();
// Now loop through the specified number of years.
int year = 1;
while(year <= duration) {
    // Calculate the value of the principal plus interest.
    decimal interestPaid = principal * (interest / 100);
    // Now calculate the new principal by adding
    principal = principal + interestPaid;
    // Round off the principal to the nearest cent.
    principal = decimal.Round(principal, 2);
    // Output the result.
    Console.WriteLine(year + " - " + principal);
    // Skip over to next year.
    year = year + 1;
}
```

Book I Getting into the Program Flow

## 102 Here We Go Loop-the-Loop

```csharp
year = year * 1;
}
// Wait for user to acknowledge the results.
Console.WriteLine("Press Enter to terminate . . ");
Console.Read();

```

This program works largely the same way as the examples in previous sections of this chapter, except in the area of user input. This time, a while loop replaces the if statement used in earlier examples to detect invalid input:

```csharp
decimal principal;
while(true)
{
    Console.WriteLine("Enter principal: ");
    string principalInput = Console.ReadLine();
    principal = Convert.ToDecimal(principalInput);
    // Exit when the value entered is correct.
    if (principal >= 0)
    {
        break;
    }
    // Generate an error on incorrect input.
    Console.WriteLine("Principal cannot be negative");
    Console.WriteLine("Try again");
    Console.WriteLine();
}
```

This section of code inputs a value from the user within a loop. If the value of the text is okay, the program exits the input loop and continues. However, if the input has an, the user sees an error message and control passes back to the program to start over.

The program continues to loop until the user enters the correct input. (In the worst case, the program could loop until an obtuse user dies of old age.)

Notice that the conditionals have been reversed because the question is no longer whether illegal input should generate an error message but, whether the correct input should exit the loop. In the interest section, for example, consider this:

```csharp
principal < 0 || principal > maximumInterest
```

This test changes to:

```csharp
interest >= 0 && interest <= maximumInterest
```

Clearly, interest >= 0 is the opposite of interest < 0. What may not be as obvious is that the OR (|) operator is replaced with an AND (&&) operator. "Exit the loop if the interest is greater than zero AND less than the maximum amount (in other words, if it is correct"

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_127_0.png)

## Here We Go Loop-the-Loop 103

By the way, how could you revise CalculateInterestTableMoreForgiving to let the user run calculation after calculation and enter new principal and interest figures until time she wants to quit? **Hint:** Use another `while (true)` loop with its own exit condition.

Note that the principal variable must be declared outside the loop of scope rules, which I explain in the next section.

It may sound obvious, but the expression true evaluates to true. Therefore, `while(true)` is your archetypal infinite loop. It's the embedded break command that exits the loop. Therefore, if you use the `while(true)` loop, make sure that your break condition can occur.

The output from a sample execution of this program (showing one of the author’s ignorance) appears this way:

```
Enter principal: -1000
Principal cannot be negative
Try again

Enter principal: 1000
Enter interest: -10
Interest cannot be negative or greater than 50
Try again

Enter interest: 10
Enter number of years: 5

Principal = 1000
Interest = 10%
Duration = 5 years

1-1100.00
2-1210.00
3-1331.00
4-1464.10
5-1610.51
Press Enter to terminate . . .
```

The program refuses to accept a negative principal or interest amount and painfully explains the mistake on each loop.

Explain exactly what the user did before looping back for further input or else that person will become extremely confused. Showing an example may also help, especially for formatting problems. A little diplomacy can’t hurt, as Grandma may have pointed out.

A variable declared within the body of a loop is *only defined within* that loop. Consider this code snippet:

## 104 Looping a Specified Number of Times with

```csharp
int days = 1;
while(days < duration)
{
    int average = value / days;
    // ... some series of commands
    days = days + 1;
}
```

The variable average is not defined outside the while loop.

## 105 Looping a Specified Number of Times with

```csharp
year = year * 1;
}
```

Book I
Chapter 5

## An example

You can see how the for loop works in this example:

```csharp
a = 1;
// Now loop for.
for(int year = 1; year < duration; year + 1)
{
    // . . body of code .
}
// The program continues here.
a = 2;
```