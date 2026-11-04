
```
// Calculate the value of the principal plus interest.
decimal interestPaid;
interestPaid = principal * (interest / 100);
// Now calculate the total.
decimal total = principal + interestPaid;
```

The first equation multiplies the principal times the interest to produce the interest to be paid — interestPaid. (You divide by 100 because interest is usually calculated by entering a percentage amount.) The interest to be paid is then added back into the principal, resulting in a new principal, which is stored in the variable total.

The program must anticipate almost anything when dealing with human input. For example, you don't want your program to accept a negative principal or interest amount (well, maybe a negative interest). The following CalculateInterest program includes checks to ensure that neither of these entries happens:

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_112_0.png)

```
// CalculateInterest -- Calculate the interest amount paid
// on a given principal. If either the principal or the
// interest rate is negative, generate an error message.
using System;
namespace CalculateInterest
{
    public class Program
    {
        public static void Main(string[] args)
        {
            // Prompt user to enter source principal.
            Console.Write("Enter principal: ");
            string principalInput = Console.ReadLine();
            decimal principal = Convert.ToDecimal(principalInput);

            // Make sure that the principal is not negative.
            if (principal < 0)
            {
                Console.WriteLine("Principal cannot be negative");
                principal = 0;
            }

            // Enter the interest rate.
            Console.Write("Enter interest: ");
            string interestInput = Console.ReadLine();
            decimal interest = Convert.ToDecimal(interestInput);

            // Make sure that the interest is not negative either.
            if (interest < 0)
            {
                Console.WriteLine("Interest cannot be negative");
                interest = 0;
            }

            // Calculate the value of the principal plus interest.
            decimal interestPaid;
            interestPaid = principal * (interest / 100);

            // Now calculate the total.
            decimal total = principal + interestPaid;

            // Output the result.
            Console.WriteLine(); // Skip a line.
            Console.WriteLine("Principal   = " + principal);
            Console.WriteLine("Interest    = " + interest + "%");
            Console.WriteLine();
            Console.WriteLine("Interest paid = " + interestPaid);
            Console.WriteLine("Total      = " + total);
            // Wait for user to acknowledge the results.
            Console.WriteLine("Press Enter to terminate . . .");
            Console.Read();
        }
    }
}
```

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_113_0.png)

The CalculateInterest program begins by prompting the user for his name using `WriteLine()` to write a string to the console. Tell the user exactly what you want and, if possible, specify the format. Users don't respond well to uninformative prompts, such as `>`.

The sample program uses the `ReadLine()` command to read in whatever the user types; the program returns the value entered, in the form of a string, when the user presses Enter. Because the program is looking for the principal in the form of a decimal, the input string must be converted using the `Convert.ToDecimal()` command. The result is stored in `principalInput`.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_113_1.png)

The `ReadLine()`, `WriteLine()`, and `ToDecimal()` commands are all examples of method calls. A *method call* delegates some work to another part of the program, called a *method*. I describe method calls in detail in Book II; these particular method calls are straightforward. You should be able to get the gist of the meaning using my extraordinarily insightful explanatory narrative. If that doesn't work, ignore the narrative. If *that* doesn't work, see Book II.

The next line in the example checks `principal`. If it's negative, the program outputs a polite "nastygram" indicating that the user has fouled up. The program does the same thing for the interest rate, and then it performs the simplistic interest calculation outlined earlier, in the "Introducing the If Statement," and spits out the result, using a series of `WriteLine()` commands.

The program generates the following output with a legitimate principal amount and a usurious interest rate that is perfectly legal in most states:

```
Enter principal: 1234
Enter interest: 21

Principal      = 1234
Interest       = 21%

Interest paid = 259.14
Total          = 1493.14
Press Enter to terminate . . .
```

Executing the program with illegal input generates the following output:

```
Enter principal: 1234
Enter interest: -12.5
Interest cannot be negative

Principal      = 1234
Interest       = 0%
Interest paid = 0
Total = 1234
Press Enter to terminate . . .
```

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_114_0.png)

Indent the lines within an if clause to enhance readability. This type of indentation is ignored by C# but is helpful to us humans. Most programming editors support autoindenting, whereby the editor automatically indents as soon as you enter the if command. To set autoindenting in Visual Studio, choose Tools→Options. Then expand the Text Editor node. From there, expand C#. Finally, click Tabs. On this page, enable Smart Indenting and set the number of spaces per indent to your preference. (I use two spaces per indent in this book.) Set the tab size to the same value.

## Examining the else statement

Sometimes, your code must check for mutually exclusive conditions. For example, the following code segment stores the maximum of two numbers, a and b, in the variable max:

```
// Store the maximum of a and b into the variable max.
int max;
// If a is greater than b . . .
if (a > b)
{
  // . . . save a as the maximum.
  max = a;
}
// If a is less than or equal to b . . .
if (a <= b)
{
  // . . . save b as the maximum.
  max = b;
}
```

The second if statement causes needless processing because the two conditions are mutually exclusive. If a is greater than b, it can't possibly be less than or equal to b. C# defines an else clause for just this case. The else keyword defines a block of code that's executed if the if block is not.

The code segment to calculate the maximum now appears this way:

```
// Store the maximum of a and b into the variable max.
int max;
// If a is greater than b . . .
if (a > b)
{
  // . . . save a as the maximum; otherwise . . .
  max = a;
}
else
{
  // . . . save b as the maximum.
  max = b;
}
```

```
}
    // Wait for user to acknowledge the results
    Console.WriteLine("Press Enter to terminate . . .");
    Console.Read();
}
}
```

The program first reads the principal from the user. If the principal is negative, the program outputs an error message and quits. If the principal is not negative, control passes to the else clause, where the program continues executing.

The interest rate test has been improved in this example. Here, the program requires an interest rate that's nonnegative (a mathematical law) and less than a maximum rate (a judiciary law — I can only wish that credit cards had an interest rate limit). This if statement uses the following compound test:

```
if (interest < 0 || interest > maximumInterest)
```

This statement is true if interest is less than 0 or greater than maximumInterest. Notice that I declare maximumInterest at the top of the program rather than hard-code it as a constant number here. Hard-coding refers to using values directly in your code, rather than creating a constant to hold them.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_117_0.png)

Define important constants at the top of your program. Giving a constant a descriptive name (rather than just a number) makes it easy to find and easier to change. If the constant appears ten times in your code, you still have to make only one change to change all references.

Entering a correct principal but a negative interest rate generates this output:

```
Enter principal: 1234
Enter interest: -12.5
Interest cannot be negative or greater than 50.
Press Enter to terminate . . .
```

Only when the user enters both a legal principal and a legal interest rate does the program generate the correct calculation:

```
Enter principal: 1234
Enter interest: 12.5

Principal   = 1234
Interest    = 12.5%
Interest paid = 154.250
Total       = 1388.250
Press Enter to terminate . . .
```

## Running the switchboard

You often want to test a variable for numerous different values. For example, maritalStatus may be 0 for unmarried, 1 for married, 2 for divorced, 3 for
