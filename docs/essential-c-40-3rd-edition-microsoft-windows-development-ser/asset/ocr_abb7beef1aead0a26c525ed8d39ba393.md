immediately jumps to the first instruction following the loop. Listing 348 examines the foreach loop from the tic-tac-toe program.

# LISTING 3.48: Using break to Escape Once a Winner is Found

```
class TicTacToe // Declares the TicTacToe class.
{
static void Main() // Declares the entry point of the program.
{
// int winner=0;
// Stores locations each player has moved.
int[] playerPositions = {0,0};
// Hardcoded board position
// X | 2 | 0
// ---+---+---
// 0 | 0 | 6
// ---+---+---
// X | X | X
playerPositions[0] = 449;
playerPositions[1] = 28;
// Determine if there is a winner
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
"Player {0} was the winner", winner);
}
}
```

Output 3.24 shows the results of Listing 3.48.