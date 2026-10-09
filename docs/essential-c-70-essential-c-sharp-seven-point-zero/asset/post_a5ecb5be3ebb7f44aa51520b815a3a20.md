
Combining a bitmap with a mask using something like `fields &= mask` clears the bits in `fields` that are not set in the `mask`. The opposite, `fields &= ~mask`, clears the bits in `fields` that are set in `mask`.

## Bitwise Complement Operator (~)

The **bitwise complement operator** takes the complement of each bit in the operand, where the operand can be an `int`, `uint`, `long`, or `ulong`. The expression `~1`, therefore, returns the value with binary notation 1111 1111 1111 1111 1111 1111 1111 1110, and `~(1<<31)` returns the number with binary notation 0111 1111 1111 1111 1111 1111 1111 1111.

## Control Flow Statements, Continued

Now that we’ve described Boolean expressions in more detail, we can more clearly describe the control flow statements supported by C#. Many of these statements will be familiar to experienced programmers, so you can skim this section looking for details specific to C#. Note in particular the foreach loop, as it may be new to many programmers.

## The while and do/while Loops

Thus far you have learned how to write programs that do something only once. However, computers can easily perform similar operations multiple times. To do so, you need to create an instruction loop. The first instruction loop we discuss is the while loop, because it is the simplest conditional loop. The general form of the while statement is as follows:

```
while (condition)
    statement
```

The computer will repeatedly execute the statement that is the “body” of the loop as long as the condition (which must be a Boolean expression) evaluates to `true`. If the condition evaluates to `false`, code execution skips the body and executes the code following the loop statement. Note that `statement` will continue to execute even if it causes the condition to become `false`. The loop exits only when the condition is reevaluated “at the top of the loop.” The Fibonacci calculator shown in Listing 4.43 demonstrates the while loop.

**LISTING 4.43: while Loop Example**

```
class FibonacciCalculator
{
    static void Main()
    {
        decimal current;
        decimal previous;
        decimal temp;
        decimal input;

        System.Console.Write("Enter a positive integer:");

        // decimal.Parse converts the Readline to a decimal
        input = decimal.Parse(System.Console.ReadLine());

        // Initialize current and previous to 1, the first
        // two numbers in the Fibonacci series
        current = previous = 1;

        // While the current Fibonacci number in the series is
        // less than the value input by the user
        while (current <= input)
        {
            temp = current;
            current = previous + current;
            previous = temp; // Executes even if previous
            // statement caused current to exceed input
        }

        System.Console.WriteLine(
            $"The Fibonacci number following this is { current }");
    }
}
```

A **Fibonacci number** is a member of the **Fibonacci series**, which includes all numbers that are the sum of the previous two numbers in the series, beginning with 1 and 1. In Listing 4.43, you prompt the user for an integer. Then you use a while loop to find the first Fibonacci number that is greater than the number the user entered.

**BEGINNER TOPIC**

**When to Use a while Loop**

The remainder of this chapter considers other statements that cause a block of code to execute repeatedly. The term *loop body* refers to the statement (frequently a code block) that is to be executed within the while statement, since the code is executed in a “loop” until the exit condition is achieved. It is important to understand which loop construct to select. You use a while construct to iterate while the condition evaluates to true. A for loop is used most appropriately whenever the number of repetitions is known, such as when counting from 0 to n. A do/while is similar to a while loop, except that it will always execute the loop body at least once.

The do/while loop is very similar to the while loop except that a do/while loop is preferred when the number of repetitions is from 1 to $n$ and $n$ is not known when iterating begins. This pattern frequently occurs when prompting a user for input. Listing 4.44 is taken from the tic-tac-toe program.

**LISTING 4.44:** do/while Loop Example

```
// Repeatedly request player to move until he
// enters a valid position on the board
bool valid;
do
{
    valid = false;

    // Request a move from the current player
    System.Console.Write(
        $"\nPlayer {currentPlayer}: Enter move:");
    input = System.Console.ReadLine();

    // Check the current player's input
    // ...

} while (!valid);
```

In Listing 4.44, you initialize valid to false at the beginning of each iteration, or loop repetition. Next, you prompt and retrieve the number the user input. Although not shown here, you then check whether the input was correct, and if it was, you assign valid equal to true. Since the code uses a do/while statement rather than a while statement, the user will be prompted for input at least once.

The general form of the do/while loop is as follows:

```
do
    statement
while (condition);
```

As with all the control flow statements, a code block is generally used as the single statement to allow multiple statements to be executed as the loop body. However, any single statement except for a labeled statement or a local variable declaration can be used.

## The for Loop

The for loop iterates a code block until a specified condition is reached. In that way, it is very similar to the while loop. The difference is that the for loop has built-in syntax for initializing, incrementing, and testing the value of a counter, known as the **loop variable**. Because there is a specific location in the loop syntax for an increment operation, the increment and decrement operators are frequently used as part of a for loop.

Listing 4.45 shows the for loop used to display an integer in binary form. The results of this listing appear in Output 4.21.

**LISTING 4.45: Using the for Loop**

```
class BinaryConverter
{
    static void Main()
    {
        const int size = 64;
        ulong value;
        char bit;

        System.Console.Write("Enter an integer: ");
        // Use long.Parse()to support negative numbers
        // Assumes unchecked assignment to ulong
        value = (ulong)long.Parse(System.Console.ReadLine());

        // Set initial mask to 100...
        ulong mask = 1UL << size - 1;
        for (int count = 0; count < size; count++)
        {
            bit = ((mask & value) > 0) ? '1' : '0';
            System.Console.Write(bit);
            // Shift mask one location over to the right
            mask >>= 1;
        }
    }
}
```

**OUTPUT 4.21**

```
Enter an integer: -42
111111111111111111111111111111111111111111111111111111111111010110
```

Listing 4.45 performs a bit mask 64 times, once for each bit in the number. The three parts of the for loop header first declare and initialize the variable count, then describe the condition that must be met for the loop body to be executed, and finally describe the operation that updates the loop variable. The general form of the for loop is as follows:

```
for (initial ; condition ; loop)
statement
```

Here is a breakdown of the for loop:

- The initial section performs operations that precede the first iteration. In Listing 4.45, it declares and initializes the variable count. The initial expression does not have to be a declaration of a new variable (though it frequently is). It is possible, for example, to declare the variable beforehand and simply initialize it in the for loop, or to skip the initialization section entirely by leaving it blank. Variables declared here are in scope throughout the header and body of the for statement.
- The condition portion of the for loop specifies an end condition. The loop exits when this condition is false, exactly like the while loop does. The for loop will execute the body only as long as the condition evaluates to true. In the preceding example, the loop exits when count is greater than or equal to 64.
- The loop expression executes after each iteration. In the preceding example, count++ executes after the right shift of the mask (mask >>= 1) but before the condition is evaluated. During the 64th iteration, count is incremented to 64, causing the condition to become false and therefore terminating the loop.
- The statement portion of the for loop is the "loop body" code that executes while the conditional expression remains true.

If you wrote out each for loop execution step in pseudocode without using a for loop expression, it would look like this:

1. Declare and initialize count to 0.
2. If count is less than 64, continue to step 3; otherwise, go to step 7.
3. Calculate bit and display it.
