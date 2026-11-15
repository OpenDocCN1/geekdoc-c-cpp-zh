# Full Source Code Listings

MANY OF THE CHAPTERS in this book have source code spread over multiple listings. When listings are large, this makes the code difficult to follow. This appendix includes the code listings as one program, making the individual listings easier to understand as a whole.

# Chapters 3 and 4

# LISTING B.1: Tic-Tac-Toe

```
#define CSHARP2

using System;

#pragma warning disable 1030 // Disable user-defined warnings

// The TicTacToe class enables two players to
// play tic-tac-toe.
class TicTacToeGame // Declares the TicTacToeGame class
{
    static void Main() // Declares the entry point to the program
    {
        // Stores locations each player has moved.
        int[] playerPositions = { 0, 0 };

        // Initially set the currentPlayer to Player 1;
        int currentPlayer = 1;

        // Winning player
```