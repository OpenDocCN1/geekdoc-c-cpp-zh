```
```
char go_first = askYesNo("Do you require the first move?");
if (go_first == 'y')
{
    cout << "\nThen take the first move. You will need it.\n";
    return X;
}
else
{
    cout << "\nYour bravery will be your undoing... I will go first.\n";
    return 0;
}
}
```
```

# The opponent() Function

This function gets a piece (either an 'X' or an 'O') and returns the opponent's piece (either an 'X' or an 'O').

```
```
char opponent(char piece)
{
    if (piece == X)
    {
        return 0;
    }
    else
    {
        return X;
    }
}
```
```

# The displayBoard() Function

This function displays the board passed to it. Because each element in the board is either a space, an 'X', or an 'O', the function can display each one. I use a few other characters on my keyboard to draw a decent-looking Tic-Tac-Toe board.

```
```
void displayBoard(const vector<char>& board)
{
    cout << "\n\t" << board[0] << " | " << board[1] << " | " << board[2];
    cout << "\n\t" << "_______";
    cout << "\n\t" << board[3] << " | " << board[4] << " | " << board[5];
    cout << "\n\t" << "_______";
```
```