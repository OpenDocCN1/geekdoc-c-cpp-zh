
## Constant Expressions (const)

The preceding chapter discussed literal values, or values embedded directly into the code. It is possible to combine multiple literal values in a **constant expression** using operators. By definition, a constant expression is one that the C# compiler can evaluate at compile time (instead of calculating it when the program runs) because it is composed of constant operands. For example, the number of seconds in a day can be assigned as a constant expression whose result can then be used in other expressions.

The const keyword in Listing 3.19 locks the value at compile time. Any attempt to modify the value later in the code results in a compile error.

### LISTING 3.19:

```
// ...
public long Main()
{
    const int secondsPerDay = 60 * 60 * 24;      Constant Expression
    const int secondsPerWeek = secondsPerDay * 7;
    // ... Constant
}
```

Note that even the value assigned to secondsPerWeek is a constant expression, because the operands in the expression are also constants, so the compiler can determine the result.

## Introducing Flow Control

Later in this chapter is a code listing (Listing 3.43) that shows a simple way to view a number in its binary form. Even such a simple program, however, cannot be written without using control flow statements. Such statements control the execution path of the program. This section discusses how to change the order of statement execution based on conditional checks. Later on, you will learn how to execute statement groups repeatedly through loop constructs.

A summary of the control flow statements appears in Table 3.1. Note that the General Syntax Structure column indicates common statement use, not the complete lexical structure.

### TABLE 3.1: Control Flow Statements

| Statement | General Syntax Structure | Example |
|---|---|---|
| if statement | `if(boolean-expression) embedded-statement` | `if (input == "quit") {<br>   System.Console.WriteLine(<br>      "Game end");<br>   return;<br>}` |
| | `if(boolean-expression) embedded-statement else embedded-statement` | `if (input == "quit") {<br>   System.Console.WriteLine(<br>      "Game end");<br>   return;<br>}<br>else<br>   GetNextMove();` |
| while statement | `while(boolean-expression) embedded-statement` | `while(count < total) {<br>   System.Console.WriteLine(<br>      "count = {0}", count);<br>   count++;<br>}` |

### TABLE 3.1: Control Flow Statements (Continued)

| Statement | General Syntax Structure | Example |
|---|---|---|
| do while statement | `do embedded-statement while(boolean-expression);` | `do { System.Console.WriteLine( "Enter name :"); input = System.Console.ReadLine(); } while(input != "exit");` |
| for statement | `for(for-initializer; boolean-expression; for-iterator) embedded-statement` | `for (int count = 1; count <= 10; count++) { System.Console.WriteLine( "count = {0}", count); }` |
| Foreach statement | `foreach(type identifier in expression) embedded-statement` | `foreach (char letter in email) { if(!insideDomain) { if (letter == '@') { insideDomain = true; continue; } System.Console.Write( letter); } }` |
| continue statement | `continue;` | |

### TABLE 3.1: Control Flow Statements (Continued)

| Statement | General Syntax Structure | Example |
|---|---|---|
| switch statement | `switch(governing-type-expression) { ... case const-expression: statement-list jump-statement default: statement-list jump-statement }` | `switch(input) { case "exit": case "quit": System.Console.WriteLine("Exiting app...."); break; case "restart": Reset(); goto case "start"; case "start": GetMove(); break; default: System.Console.WriteLine(input); break; }` |
| break statement | `break;` | |
| goto statement | `goto identifier; goto case const-expression; goto default;` | |

An embedded-statement in Table 3.1 corresponds to any statement, including a code block (but not a declaration statement or a label).

Each C# control flow statement in Table 3.1 appears in the tic-tac-toe program found in Appendix B. The program displays the tic-tac-toe board, prompts each player, and updates with each move.

The remainder of this chapter looks at each statement in more detail. After covering the if statement, it introduces code blocks, scope, Boolean expressions, and bitwise operators before continuing with the remaining control flow statements. Readers who find the table familiar because of C#'s similarities to other languages can jump ahead to the section titled C# Processor Directives and skip to the Summary section at the end of the chapter.

## if Statement

The if statement is one of the most common statements in C#. It evaluates a Boolean expression (an expression that returns a Boolean), and if the result is true, the following statement (or block) is executed. The general form is as follows:

```
if(condition)
 consequence
 [else
 alternative]
```

There is also an optional else clause for when the Boolean expression is false. Listing 3.20 shows an example.

### LISTING 3.20: if/else Statement Example

```
class TicTacToe // Declares the TicTacToe class.
{
    static void Main() // Declares the entry point of the program.
    {
        string input;

        // Prompt the user to select a 1- or 2- player game.
        System.Console.Write (
            "1 - Play against the computer\n" +
            "2 - Play against another player.\n" +
            "Choose: ");
        input = System.Console.ReadLine();
        if(input=="1")
            // The user selected to play the computer.
            System.Console.WriteLine(
                "Play against computer selected.");
        else
            // Default to 2 players (even if user didn't enter 2).
            System.Console.WriteLine(
                "Play against another player.");
    }
}
```

3. Known as naughts and crosses to readers outside the United States.

In Listing 3.20, if the user enters 1, the program displays "Play against computer selected.". Otherwise, it displays "Play against another player.".

## Nested if

Sometimes code requires multiple if statements. The code in Listing 3.21 first determines whether the user has chosen to exit by entering a number less than or equal to 0; if not, it checks whether the user knows the maximum number of turns in tic-tac-toe.

### LISTING 3.21: Nested if Statements

```
class TicTacToeTrivia
{
    static void Main()
    {
        int input; // Declare a variable to store the input.

        System.Console.Write(
            "What is the maximum number " +
            "of turns in tic-tac-toe?" +
            "(Enter 0 to exit.): ");
        // int.Parse() converts the ReadLine()
        // return to an int data type.
        input = int.Parse(System.Console.ReadLine());

        if (input <= 0)
            // Input is less than or equal to 0.
            System.Console.WriteLine("Exiting...");
        else
            if (input < 9)
                // Input is less than 9.
                System.Console.WriteLine(
                    "Tic-tac-toe has more than {0}" +
                    "maximum turns.", input);
            else
                if(input>9)
                    // Input is greater than 9.
                    System.Console.WriteLine(
                        "Tic-tac-toe has fewer than {0}" +
                        "maximum turns.", input);
                else
                    // Input equals 9.
                    System.Console.WriteLine(
                        "Correct. " +
                        "tic-tac-toe has a max. of 9 turns.");
    }
}
```

### Output 3.13:

```
What's the maximum number of turns in tic-tac-toe? (Enter 0 to exit.): 9
Correct. tic-tac-toe has a max. of 9 turns.
```

Assume the user enters 9 when prompted at line 14. Here is the execution path:

- Line 16: Check if input is less than 0. Since it is not, jump to line 20.
- Line 20: Check if input is less than 9. Since it is not, jump to line 26.
- Line 26: Check if input is greater than 9. Since it is not, jump to line 33.
- Line 33: Display that the answer was correct.

Listing 3.21 contains nested if statements. To clarify the nesting, the lines are indented. However, as you learned in Chapter 1, whitespace does not affect the execution path. Without indenting and without newlines, the execution would be the same. The code that appears in the nested if statement in Listing 3.22 is equivalent to Listing 3.21.

### LISTING 3.22: if/else Formatted Sequentially

```
if (input < 0)
	System.Console.WriteLine("Exiting...");
else if (input < 9)
	System.Console.WriteLine(
```
