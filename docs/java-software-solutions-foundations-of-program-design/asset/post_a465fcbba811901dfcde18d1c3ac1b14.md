
## 5.4 The while Statement

As we discussed in the introduction of this chapter, a repetition statement (or loop) allows us to execute another statement multiple times. A while statement is a loop that evaluates a boolean condition just as an if statement does and executes a statement (called the body of the loop) if the condition is true. However, unlike the if statement, after the body is executed, the condition is evaluated again. If it is still true, the body is executed again. This repetition continues until the condition becomes false; then processing continues with the statement after the body of the while loop. Figure 5.7 shows this processing.

### While Statement

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_257_0.png)

The while loop repeatedly executes the specified Statement as long as the boolean Expression is true. The Expression is evaluated first; therefore the Statement might not be executed at all. The Expression is evaluated again after each execution of Statement until the Expression becomes false.

Example:

```
while (total > max)
{
    total = total / 2;
    System.out.println ("Current total: " + total);
}
```

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_257_1.png)

FIGURE 5.7 The logic of a while loop

The following loop prints the values from 1 to 5. Each iteration through the loop prints one value, then increments the counter.

```
int count = 1;
while (count <= 5)
{
    System.out.println (count);
    count++;
}
```

KEY CONCEPT
A while statement executes the same statement until its condition becomes false.

Note that the body of the while loop is a block containing two statements. The entire block is repeated on each iteration of the loop.

Let’s look at another program that uses a while loop. The Average program shown in Listing 5.7 reads a series of integer values from the user, sums them up, and computes their average.

We don’t know how many values the user may enter, so we need to have a way to indicate that the user has finished entering numbers. In this program, we designate zero to be a sentinel value that indicates the end of the input. The while loop continues to process input values until the user enters zero. This assumes that zero

### LISTING 5.7

```
//****************************************************************
// Average.java        Author: Lewis/Loftus
//
// Demonstrates the use of a while loop, a sentinel value, and a
// running sum.
//****************************************************************

import java.text.DecimalFormat;
import java.util.Scanner;

public class Average
{
    //-------------------------------------------------------------
    // Computes the average of a set of values entered by the user.
    // The running sum is printed as the numbers are entered.
    //-------------------------------------------------------------
    public static void main (String[] args)
    {
        int sum = 0, value, count = 0;
        double average;

        Scanner scan = new Scanner (System.in);
```

### LISTING 5.7 continued

```
System.out.print ("Enter an integer (0 to quit): ");
value = scan.nextInt();

while (value != 0) // sentinel value of 0 to terminate loop
{
    count++;

    sum += value;
    System.out.println ("The sum so far is " + sum);

    System.out.print ("Enter an integer (0 to quit): ");
    value = scan.nextInt();
}

System.out.println ();

if (count == 0)
    System.out.println ("No values were entered.");
else
{
    average = (double)sum / count;

    DecimalFormat fmt = new DecimalFormat ("0.###");
    System.out.println ("The average is " + fmt.format(average));
}
}
```

### OUTPUT

```
Enter an integer (0 to quit): 25
The sum so far is 25
Enter an integer (0 to quit): 164
The sum so far is 189
Enter an integer (0 to quit): -14
The sum so far is 175
Enter an integer (0 to quit): 84
The sum so far is 259
Enter an integer (0 to quit): 12
The sum so far is 271
Enter an integer (0 to quit): -35
The sum so far is 236
Enter an integer (0 to quit): 0

The average is 39.333
```

is not one of the valid numbers that should contribute to the average. A sentinel value must always be outside the normal range of values entered.

Note that in the Average program, a variable called sum is used to maintain a running sum, which means it is the sum of the values entered thus far. The variable sum is initialized to zero, and each value read is added to and stored back into sum.

We also have to count the number of values that are entered so that after the loop concludes we can divide by the appropriate value to compute the average. Note that the sentinel value is not counted. Consider the unusual situation in which the user immediately enters the sentinel value before entering any valid values. The if statement at the end of the program avoids a divide-by-zero error.

Let's examine yet another program that uses a while loop. The WinPercentage program shown in Listing 5.8 computes the winning percentage of a sports team based on the number of games won.

We use a while loop in the WinPercentage program to validate the input, meaning we guarantee that the user enters a value that we consider to be valid. In this example, that means that the number of games won must be greater than or equal to zero and less than or equal to the total number of games played. The while loop continues to execute, repeatedly prompting the user for valid input, until the entered number is indeed valid.

```
//******************************
// WinPercentage.java Author: Lewis/Loftus
// Demonstrates the use of a while loop for input validation.
//******************************
import java.text.NumberFormat;
import java.util.Scanner;

public class WinPercentage
{
//----------------------
// Computes the percentage of games won by a team.
//----------------------
public static void main (String[] args)
{
final int NUM_GAMES = 12;
int won;
double ratio;
```

### LISTING 5.8 continued

```
Scanner scan = new Scanner (System.in);

System.out.print ("Enter the number of games won (0 to "
    + NUM_GAMES + "):");
won = scan.nextInt();

while (won < 0 || won > NUM_GAMES)
{
    System.out.print ("Invalid input. Please reenter: ");
    won = scan.nextInt();
}

ratio = (double)won / NUM_GAMES;

NumberFormat fmt = NumberFormat.getPercentInstance();

System.out.println ();
System.out.println ("Winning percentage: " + fmt.format(ratio));
}
```

### OUTPUT

```
Enter the number of games won (0 to 12): -5
Invalid input. Please reenter: 13
Invalid input. Please reenter: 7

Winning percentage: 58%
```

We generally want our programs to be robust, which means that they handle potential problems as elegantly as possible. Validating input data and avoiding errors such as dividing by zero are situations that we should consciously address when designing a program. Loops and conditionals help us recognize and deal with such situations.

### Infinite Loops

It is the programmer’s responsibility to ensure that the condition of a loop will eventually become false. If it doesn’t, the loop body will execute forever, or at least until the program is interrupted. This situation, referred to as an infinite loop, is a common mistake.

The following is an example of an infinite loop:

```
int count = 1;
while (count <= 25)  // Warning: this is an infinite loop!
{
    System.out.println (count);
    count = count - 1;
}
```

If you execute this loop, you should be prepared to interrupt it. On most systems, pressing the Control-C keyboard combination (hold down the Control key and press C) terminates a running program.

In this example, the initial value of count is 1, and it is decremented in the loop body. The while loop will continue as long as count is less than or equal to 25. Because count gets smaller with each iteration, the condition will always be true, or at least until the value of count gets so small that an underflow error occurs. The point is that the logic of the code is clearly wrong.

> KEY CONCEPT
> We must design our programs carefully to avoid infinite loops.

Let’s look at some other examples of infinite loops:

```
int count = 1;
while (count != 50)  // infinite loop
    count += 2;
```

In this code fragment, the variable count is initialized to 1 and is moving in a positive direction. However, note that it is being incremented by 2 each time. This loop will never terminate because count will never equal 50. It begins at 1 and then changes to 3, then 5, and so on. Eventually it reaches 49, then changes to 51, then 53, and continues forever.

Now consider the following situation:

```
double num = 1.0;
while (num != 0.0)  // infinite loop
    num = num - 0.1;
```

Once again, the value of the loop control variable seems to be moving in the correct direction. And, in fact, it seems like num will eventually take on the value 0.0. However, this loop is infinite (at least on most systems), because num will never have a value exactly equal to 0.0. This situation is similar to one we discussed earlier in this chapter when we explored the idea of comparing floating point values in the condition of an if statement. Because of the way the values are represented in binary, minute computational errors occur internally, making it problematic to compare two floating point values for equality.
