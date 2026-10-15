```
```csharp
// Determine if there is a winner.
int[] winningMasks = {
    7, 56, 448, 73, 146, 292, 84, 273 };

// Iterate through each winning mask to determine
// if there is a winner.
foreach (int mask in winningMasks)
{
    if ((mask & playerPositions[0]) == mask)
    {
        winner = 1;
        break;
    }
    else if ((mask & playerPositions[1]) == mask)
    {
        winner = 2;
        break;
    }
}

System.Console.WriteLine(
    $"Player { winner } was the winner");
}
```
```

Output 3.24 shows the results of Listing 3.50.

# OUTPUT 3.24

```
```text
Player 1 was the winner
```
```

Listing 3.50 uses a break statement when a player holds a winning position. The break statement forces its enclosing loop (or a switch statement) to cease execution, and control moves to the next line outside the loop. For this listing, if the bit comparison returns true (if the board holds a winning position), the break statement causes control to jump and display the winner.

# BEGINNER TOPIC

# Bitwise Operators for Positions

The tic-tac-toe example (the full listing is available in Appendix B) uses the bitwise operators to determine which player wins the game. First, the code