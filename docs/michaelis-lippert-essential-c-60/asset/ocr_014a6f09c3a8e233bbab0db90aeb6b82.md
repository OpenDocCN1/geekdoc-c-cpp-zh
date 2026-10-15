# OUTPUT 3.13

```
What is the maximum number of turns in tic-tac-toe? (Enter 0 to exit.): 9
Correct, tic-tac-toe has a maximum of 9 turns.
```

Assume the user enters 9 when prompted at line 14. Here is the execution path:

+   1. Line 16: Check if input is less than 0. Since it is not, jump to line 20.
+   2. Line 20: Check if input is less than 9. Since it is not, jump to line 26.
+   3. Line 26: Check if input is greater than 9. Since it is not, jump to line 33.
+   4. Line 33: Display that the answer was correct.

Listing 3.21 contains nested if statements. To clarify the nesting, the lines are indented. However, as you learned in Chapter 1, whitespace does not affect the execution path. If this code was written without the indenting and without the newlines, the execution would be the same. The code that appears in the nested if statement in Listing 3.22 is equivalent to Listing 3.21.

# LISTING 3.22: if/else Formatted Sequentially

```
if (input < 0)
    System.Console.WriteLine("Exiting...");
else if (input < 9)
    System.Console.WriteLine(
        $"tic-tac-toe has more than {input}" +
        " maximum turns.");
else if(input < 9)
    System.Console.WriteLine(
        $"tic-tac-toe has less than {input}" +
        " maximum turns.");
else
    System.Console.WriteLine(
        "Correct, tic-tac-toe has a maximum " +
        " of 9 turns.");
```

Although the latter format is more common, in each situation you should use the format that results in the clearest code.

Both of the if statement listings omit the braces. However, as discussed next, this is not in accordance with the guidelines, which advocate the use of code blocks except, perhaps, in the simplest of single-line scenarios.