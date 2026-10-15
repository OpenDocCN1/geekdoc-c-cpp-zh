# LISTING 3.19: Declaring a Constant

```
// ...
public long Main()
{
    const int secondsPerDay = 60 * 60 * 24;  // Constant Expression
    const int secondsPerWeek = secondsPerDay * 7;  // Constant
    // ...
}
```

# Introducing Flow Control

Later in this chapter is a code listing (Listing 3.45) that shows a simple way to view a number in its binary form. Even such a simple program, however, cannot be written without using control flow statements. Such statements control the execution path of the program. This section discusses how to change the order of statement execution based on conditional checks. Later on, you will learn how to execute statement groups repeatedly through loop constructs.

A summary of the control flow statements appears in Table 3.1. Note that the General Syntax Structure column indicates common statement use, not the complete lexical structure. An embedded-statement in Table 3.1 may be any statement other than a labeled statement or a declaration, but it is typically a block statement.

Each C# control flow statement in Table 3.1 appears in the tic-tac-toe³ program and is available in Appendix B and for download with the rest of the source code listings from the book. The program displays the tic-tac-toe board, prompts each player, and updates with each move.

The remainder of this chapter looks at each statement in more detail. After covering the if statement, it introduces code blocks, scope, Boolean expressions, and bitwise operators before continuing with the remaining control flow statements. Readers who find Table 3.1 familiar because of C#’s similarities to other languages can jump ahead to the section titled “C# Preprocessor Directives” or skip to the “Summary” section at the end of the chapter.

3. Known as noughts and crosses to readers outside the United States.