
```cs
// CalculateInterestTableMoreForgiving -- Calculate the interest paid on a
// given principal over a period of years. This version gives the user
// multiple chances to input the legal principal and interest.
using System;
namespace CalculateInterestTableMoreForgiving
{
    using System;
    public class Program
    {
        public static void Main(string[] args)
        {
            // Define a maximum interest rate.
            int maximumInterest = 50;
            // Prompt user to enter source principal; keep prompting
            // until the correct value is entered.
            decimal principal;
            while(true)
            {
                Console.Write("Enter principal: ");
                string principalInput = Console.ReadLine();
                principal = Convert.ToDecimal(principalInput);
                // Exit if the value entered is correct.
                if (principal >= 0)
                {
                    break;
                }
                // Generate an error on incorrect input.
                Console.WriteLine("Principal cannot be negative");
                Console.WriteLine("Try again");
                Console.WriteLine();
            }
            // Now enter the interest rate.
            decimal interest;
            while(true)
            {
                Console.Write("Enter interest: ");
                string interestInput = Console.ReadLine();
                interest = Convert.ToDecimal(interestInput);
                // Don't accept interest that is negative or too large . . .
                if (interest >= 0 && interest <= maximumInterest)
                {
                    break;
                }
                // . . . generate an error message as well.
                Console.WriteLine("Interest cannot be negative " +
                    "or greater than " + maximumInterest);
                Console.WriteLine("Try again");
                Console.WriteLine();
            }
            // Both the principal and the interest appear to be
            // legal; finally, input the number of years.
            Console.Write("Enter number of years: ");
            string durationInput = Console.ReadLine();
            int duration = Convert.ToInt32(durationInput);
            // Verify the input.
            Console.WriteLine(); // Skip a line.
            Console.WriteLine("Principal      = " + principal);
            Console.WriteLine("Interest       = " + interest + "%");
            Console.WriteLine("Duration       = " + duration + " years");
            Console.WriteLine();
            // Now loop through the specified number of years.
            int year = 1;
            while(year <= duration)
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
                Console.WriteLine(year + "-" + principal);
                // Skip over to next year.
                year = year + 1;
            }
            // Wait for user to acknowledge the results.
            Console.WriteLine("Press Enter to terminate . . .");
            Console.Read();
        }
    }
}
```

This program works largely the same way as do the examples in previous sections of this chapter, except in the area of user input. This time, a while loop replaces the if statement used in earlier examples to detect invalid input:

```cs
decimal principal;
while(true)
{
    Console.Write("Enter principal: ");
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

![](img/6df7bb88e9302e98442acc219cfbd7fc_125_0.png)

This section of code inputs a value from the user within a loop. If the value of the text is okay, the program exits the input loop and continues. However, if the input has an error, the user sees an error message and control passes back to the program flow to start over.

The program continues to loop until the user enters the correct input. (In the worst case, the program could loop until an obtuse user dies of old age.)

Notice that the conditionals have have reversed because the question is no longer whether illegal input should generate an error message but, rather, whether the correct input should exit the loop. In the interest section, for example, consider this test:

```cs
principal < 0 || principal > maximumInterest
```

This test changes to this:

```cs
interest >= 0 && interest <= maximumInterest
```

Clearly, interest >= 0 is the opposite of interest < 0. What may not be as obvious is that the OR (| |) operator is replaced with an AND (&&) operator. It says, “Exit the loop if the interest is greater than zero AND less than the maximum amount (in other words, if it is correct).”

By the way, how could you revise CalculateInterestTableForgiving to let the user run calculation after calculation and enter new principal and interest figures every time until she wants to quit? Hint: Use another while(true) loop with its own exit condition.

Note that the principal variable must be declared outside the loop because of scope rules, which I explain in the next section.

![](img/6df7bb88e9302e98442acc219cfbd7fc_126_0.png)

It may sound obvious, but the expression true evaluates to true. Therefore, while(true) is your archetypical infinite loop. It’s the embedded break command that exits the loop. Therefore, if you use the while(true) loop, make sure that your break condition can occur.

The output from a sample execution of this program (showing the author’s ignorance) appears this way:

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

Principal      = 1000
Interest       = 10%
Duration       = 5 years

1-1100.0
2-1210.00
3-1331.00
4-1464.10
5-1610.51
Press Enter to terminate . . .
```

The program refuses to accept a negative principal or interest amount and patiently explains the mistake on each loop.

![](img/6df7bb88e9302e98442acc219cfbd7fc_127_0.png)

Explain exactly what the user did wrong before looping back for further input or else that person will become extremely confused. Showing an example may also help, especially for formatting problems. A little diplomacy can’t hurt, either, as Grandma may have pointed out.

# Focusing on scope rules

A variable declared within the body of a loop is only defined within that loop. Consider this code snippet:

```cs
int days = 1;
while(days < duration)
{
    int average = value / days;
    // . . . some series of commands . . .
    days = days + 1;
}
```

![](img/6df7bb88e9302e98442acc219cfbd7fc_127_1.png)

The variable average isn’t defined outside the while loop. Various reasons for this exist, but consider this one: The first time the loop executes, the program encounters the declaration int average and the variable is defined. On the second loop, the program again encounters the declaration for average, and were it not for scope rules, it would be an error because the variable is already defined.

I could provide other, more convincing reasons than this, but this one should do for now.

Suffice it to say that the variable average goes away, as far as C# is concerned, as soon as the program reaches the closed brace — and is redefined each time through the loop.

![](img/6df7bb88e9302e98442acc219cfbd7fc_127_2.png)

Experienced programmers say that the scope of the variable average is limited to the while loop.

# Lo a Specified Number of Times with for

The while loop is the simplest and second most commonly used looping structure in C#. Compared to the for loop, however, the while loop is used about as often as metric tools in an American machine shop.

The for loop has this structure:

```cs
for(initExpression; condition; incrementExpression)
{
    // . . . body of code . . .
}
```

When the for loop is encountered, the program first executes the initExpression expression and then executes the condition. If the condition
