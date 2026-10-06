# Creating Loops with the while Statement

# TWO TRUTHS & A LIE

# Creating Loops with the while Statement

+   1. To make a while loop that executes correctly, a loop control variable is initialized before entering the loop.
2. To make a while loop that executes correctly, the loop control variable is tested in the while expression.
3. To make a while loop that executes correctly, the body of the while statement must never alter the value of the loop control variable.

> The false statement is #3. To make a while loop that executes correctly, the body of the while statement alters the value of the loop control variable.

# You Do It

Using a while Loop

In the next steps, you write a program that continuously prompts the user for a valid ID number until the user enters one. For this application, assume that a valid ID number must be between 1000 and 9999, inclusive.

+   1. Open a new project named ValidID, and enter the beginning of the program by declaring variables for an ID number, the user's input, and constant values for the highest and lowest acceptable ID numbers.

```
using System;
using static System.Console;
class ValidID
{
    static void Main()
{
        int idNum;
        string input;
        const int LOW = 1000;
        const int HIGH = 9999;
    }
```

(continues)