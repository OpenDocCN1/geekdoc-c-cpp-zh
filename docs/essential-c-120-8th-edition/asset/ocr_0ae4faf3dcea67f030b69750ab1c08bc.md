# Chapter 4: Operators and Control Flow

TABLE 4.1: Control Flow Statements (continued)
| Statement | General Syntax Structure | Example |
| :--- | :--- | :--- |
| goto default; | | |

Each C# control flow statement in Table 4.1 appears in the tic-tac-toe² program and is available in Chapter 4's source code in the file TicTacToe.cs (https://github.com/IntelliTec/EssentialCSharp/blob/v9.0/src/Chapter04/TicTacToe.cs). The program displays the tic-tac-toe board, prompts each player, and updates with each move.

The rest of this chapter looks at each statement in more detail. After covering the if statement, it introduces code blocks, scope, Boolean expressions, and bitwise operators before continuing with the remaining control flow statements. Readers find Table 4.1 familiar because of C#'s similarities to other languages can jump ahead to the statement titled "C# Preprocessor Directives" or skip to the Summary at the end of the chapter.

# if Statement

The if statement is one of the most common statements in C#. It evaluates a Boolean expression (an expression that results in either true or false) called the condition. If the condition is true, the consequence statement executes. If any statement may optionally have an else clause that contains an alternative statement to be executed if the condition is false. The general form is as follows:

```
if (condition)
    consequence-statement
else
    alternative-statement
```

In Listing 4.21, if the user enters 1, the program displays Play against computer selected. Otherwise, it displays Play against another player.

+   2. Known as noughts and crosses to readers outside the United States.