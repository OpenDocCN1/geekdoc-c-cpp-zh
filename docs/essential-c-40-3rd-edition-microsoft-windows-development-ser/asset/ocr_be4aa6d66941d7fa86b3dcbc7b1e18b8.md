```
default:
    // If none of the other case statements
    // is encountered, then the text is invalid.
    System.Console.WriteLine(
        "\nERROR: Enter a value from 1-9. "
        + "Push ENTER to quit");
    break;
}
return valid;
}
```

```
static void DisplayBoard(int[] playerPositions)
{
    // This represents the borders between each cell
    // for one row.
    string[] borders = {
        "|", "|", "|", "\n-|-", "|", "\n-|-", "|", "|",
        "\n-+-+-+", "|", "|", "|",
    };

    // Display the current board;
    int border = 0; // set the first border (border[0] = "|")
```

```
#if CSHARP2
    System.Console.Clear();
#endif
```

```
for (int position = 1;
     position <= 256;
     position <<= 1, border++)
{
    char token = CalculateToken(
        playerPositions, position);

    // Write out a cell value and the border that
    // comes after it.
    System.Console.Write("{0} {1}",
        token, borders[border]);
}
```

```
static char CalculateToken(
    int[] playerPositions, int position)
{
    // Initialize the players to 'X' and 'O'
    char[] players = { 'X', 'O' };

    char token;
    // If player has the position set,
```