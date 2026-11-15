

```
// decimal.Parse convert the ReadLine to a decimal.
input = decimal.Parse(System.Console.ReadLine());

// Initialize current and previous to 1, the first
// two numbers in the Fibonacci series.
current = previous = 1;

// While the current Fibonacci number in the series is
// less than the value input by the user.
while(current <= input)
{
    temp = current;
    current = previous + current;
    previous = temp;
}

System.Console.WriteLine(
    "The Fibonacci number following this is {0}",
    current);
}
```

A Fibonacci number is a member of the Fibonacci series, which includes all numbers that are the sum of the previous two numbers in the series, beginning with 1 and 1. In Listing 3.41, you prompt the user for an integer. Then you use a while loop to find the Fibonacci number that is greater than the number the user entered.

## BEGINNER TOPIC

## When to Use a while Loop

The remainder of this chapter considers other types of statements that cause a block of code to execute repeatedly. The term loop refers to the block of code that is to be executed within the while statement, since the code is executed in a “loop” until the exit condition is achieved. It is important to understand which loop construct to select. You use a while construct to iterate while the condition evaluates to true. A for loop is used most appropriately whenever the number of repetitions is known, such as counting from 0 to n. A do/while is similar to a while loop, except that it will always loop at least once.

The do/while loop is very similar to the while loop except that a do/while loop is preferred when the number of repetitions is from 1 to n and n is indeterminate when iterating begins. This pattern occurs most commonly when repeatedly prompting a user for input. Listing 3.42 is taken from the tic-tac-toe program.

## LISTING 3.42: do/while Loop Example

```
// Repeatedly request player to move until he
// enter a valid position on the board.
do
{
    valid = false;

    // Request a move from the current player.
    System.Console.Write(
        "Player {0}: Enter move.", currentplayer);
    input = System.Console.ReadLine();

    // Check the current player's input.
    // ...
} while (!valid);
```

In Listing 3.42, you always initialize valid to false at the beginning of each iteration, or loop repetition. Next, you prompt and retrieve the number the user input. Although not shown here, you then check whether the input was correct, and if it was, you assign valid equal to true. Since the code uses a do/while statement rather than a while statement, the user will be prompted for input at least once.

The general form of the do/while loop is as follows:

```
do
statement
while(boolean-expression );
```

As with all the control flow statements, the code blocks are not part of the general form. However, a code block is generally used in place of a single statement in order to allow multiple statements.

## The for Loop

Increment and decrement operators are frequently used within a for loop. The for loop iterates a code block until a specified condition is reached in a way similar to the while loop. The difference is that the for loop has built-in syntax for initializing, incrementing, and testing the value of a counter.

Listing 3.43 shows the for loop used to display an integer in binary form. The results of this listing appear in Output 3.21.

```
LISTING 3.43: Using the for Loop

public class BinaryConverter
{
    public static void Main()
    {
        const int size = 64;
        ulong value;
        char bit;

        System.Console.Write("Enter an integer: ");
        // Use long.Parse() so as to support negative numbers
        // Assumes unchecked assignment to ulong.
        value = (ulong)long.Parse(System.Console.ReadLine());

        // Set initial mask to 100....
        ulong mask = 1ul << size - 1;
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

Output 3.21:

Enter an integer: -42
111111111111111111111111111111111111111111111111111111111111111010

Listing 3.43 performs a bit mask 64 times, once for each bit in the number. The for loop declares and initializes the variable count, escapes once the count reaches 64, and increments the count during each iteration. Each expression within the for loop corresponds to a statement. (It is easy to remember that the separation character between expressions is a semicolon and not a comma, because each expression could be a statement.)

You write a for loop generically as follows:

```
for(initial; boolean-expression; loop) statement
```

Here is a breakdown of the for loop.

- The initial expression performs operations that precede the first iteration. In Listing 3.43, it declares and initializes the variable count. The initial expression does not have to be a declaration of a new variable. It is possible, for example, to declare the variable beforehand and simply initialize it in the for loop. Variables declared here, however, are bound within the scope of the for statement.

- The boolean-expression portion of the for loop specifies an end condition. The loop exits when this condition is false in a manner similar to the while loop’s termination. The for loop will repeat only as long as boolean-expression evaluates to true. In the preceding example, the loop exits when count increments to 64.

- The loop expression executes after each iteration. In the preceding example, count++ executes after the right shift of the mask (mask >>= 1), but before the Boolean expression is evaluated. During the sixty-fourth iteration, count increments to 64, causing boolean-expression to be false and, therefore, terminating the loop. Because each expression may be thought of as a separate statement, each expression in the for loop is separated by a semicolon.

- The statement portion of the for loop is the code that executes while the conditional expression remains true.

If you wrote out each for loop execution step in pseudocode without using a for loop expression, it would look like this:

- 1. Declare and initialize count to 0.
- 2. Verify that count is less than 64.
- 3. Calculate bit and display it.
- 4. Shift the mask.
- 5. Increment count by one.
- 6. If count<64, then jump back to line 3.

The for statement doesn't require any of the elements between parentheses. for(;;) { ... } is perfectly valid; although there still needs to be a means to escape from the loop to avoid executing infinitely. Similarly, the initial and loop expressions can be a complex expression involving multiple subexpressions, as shown in Listing 3.44.

## LISTING 3.44: for Loop Using Multiple Expressions

```
for(int x=0, y=5; ((x<5) && (y>0)); y--, x++)
{
    System.Console.Write("{0}{1}{2}\t",
        x, (x<y ? '<' : '>'), y);
}
```

The results of Listing 3.44 appear in Output 3.22.

## OUTPUT 3.22:

```
0<5   1<4   2<3   3>2   4>1   5>0
```

In this case, the comma behaves exactly as it does in a declaration statement, one that declares and initializes multiple variables. However, programmers should avoid complex expressions such as this one because they are difficult to read and understand.

Generically, you can write the for loop as a while loop, as shown here:

```
initial;
while(boolean-expression)
{
    statement;
    loop;
}
```

## BEGINNER TOPIC

## Choosing between for and while Loops

Although you can use the two statements interchangeably, generally you would use the for loop whenever there is some type of counter, and the total number of iterations is known when the loop is initialized. In contrast, you would typically use the while loop when iterations are not based on a count or when the number of iterations is indeterminate when iterating commences.

## The foreach Loop

The last loop statement within the C# language is foreach. foreach is designed to iterate through a collection of items, setting a variable to represent each item in turn. During the loop, operations may be performed on the item. One feature of the foreach loop is that it is not possible to accidentally miscount and iterate over the end of the collection.

The general form of the foreach statement is as follows:

```
foreach(type variable in collection)
statement;
```

Here is a breakdown of the foreach statement.

- type is used to declare the data type of the variable for each item within the collection.
- variable is a read-only variable into which the foreach construct will automatically assign the next item within the collection. The scope of the variable is limited to the foreach loop.
- collection is an expression, such as an array, representing multiple items.
- statement is the code that executes for each iteration within the foreach loop.

Consider the foreach loop in the context of the simple example shown in Listing 3.45.

