# LISTING 3.45: Determining Remaining Moves Using the foreach Loop

```
class TicTacToe // Declares the TicTacToe class.
{
    static void Main() // Declares the entry point of the program.
    {
        // Hardcode initial board as follows
        // | 1 | 2 | 3
        // | 4 | 5 | 6
        // | 7 | 8 | 9
        char[] cells = {
            '1', '2', '3', '4', '5', '6', '7', '8', '9'
        };

        System.Console.Write(
            "The available moves are as follows: ");

        // Write out the initial available moves
        foreach (char cell in cells)
        {
            if (cell != 'O' && cell != 'X')
            System.Console.Write("{0} ", cell);
        }
    }
}
```

Output 3.23 shows the results of Listing 3.45.

# Output 3.23:

```
The available moves are as follows: 1 2 3 4 5 6 7 8 9
```

When the execution engine reaches the foreach statement, it assigns to the variable cell the first item in the cells array—in this case, the value '1'. It then executes the code within the foreach statement block. The if statement determines whether the value of cell is 'O' or 'X'. If it is neither, then the value of cell is written out to the console. The next iteration then assigns the next array value to cell, and so on.