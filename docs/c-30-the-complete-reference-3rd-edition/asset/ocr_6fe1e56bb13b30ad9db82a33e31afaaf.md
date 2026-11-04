this statement says “add to sum the value of sum plus i, then increment i.” Thus, it is the same as this sequence of statements:

```
sum = sum + i;
i++;
```

# Declaring Loop Control Variables Inside the for Loop

Often the variable that controls a for loop is needed only for the purposes of the loop and is not used elsewhere. When this is the case, it is possible to declare the variable inside the initialization portion of the for. For example, the following program computes both the summation and the factorial of the numbers 1 through 5. It declares its loop control variable i inside the for.

```
// Declare loop control variable inside the for.
using System;
class ForVar {
    static void Main() {
        int sum = 0;
        int fact = 1;

        // Compute the factorial of the numbers 1 through 5.
        for(int i = 1; i <= 5; i++) {
            sum += i; // i is known throughout the loop.
            fact *= i;
        }

        // But, i is not known here.

        Console.WriteLine("Sum is " + sum);
        Console.WriteLine("Factorial is " + fact);
    }
}
```

When you declare a variable inside a for loop, there is one important point to remember: The scope of that variable ends when the for statement does. (That is, the scope of the variable is limited to the for loop.) Outside the for loop, the variable will cease to exist. Thus, in the preceding example, i is not accessible outside the for loop. If you need to use the loop control variable elsewhere in your program, you will not be able to declare it inside the for loop.

Before moving on, you might want to experiment with your own variations on the for loop. As you will find, it is a fascinating loop.

# The while Loop

Another of C#’s loops is the while. The general form of the while loop is

    while(condition) statement;

where statement can be a single statement or a block of statements, and condition defines the condition that controls the loop and may be any valid Boolean expression. The statement is performed while the condition is true. When the condition becomes false, program control passes to the line immediately following the loop.