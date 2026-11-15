```
int winner = 0;

string input = null;

// Display the board and
// prompt the current player
// for his next move.
for (int turn = 1; turn <= 10; ++turn)
{
    DisplayBoard(playerPositions);

    #region Check for End Game
    if (EndGame(winner, turn, input))
    {
        break;
    }
    #endregion Check for End Game

    input = NextMove(playerPositions, currentPlayer);
    winner = DetermineWinner(playerPositions);

    // Switch players
    currentPlayer = (currentPlayer == 2) ? 1 : 2;
}
}

private static string NextMove(int[] playerPositions,
    int currentPlayer)
{
    string input;

    // Repeatedly prompt the player for a move
    // until a valid move is entered.
    bool validMove;
    do
    {
        // Request a move from the current player.
        System.Console.Write("\nPlayer {0} - Enter move:",
            currentPlayer);
        input = System.Console.ReadLine();
        validMove = ValidateAndMove(playerPositions,
            currentPlayer, input);
    } while ((validMove));

    return input;
}
```