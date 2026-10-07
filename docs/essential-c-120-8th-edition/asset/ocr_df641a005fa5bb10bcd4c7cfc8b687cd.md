# Chapter 4: Operators and Control Flow

A switch statement should have at least one switch; switch(x){} is legal but will generate a warning. Also, the guideline provided earlier was to avoid omitting braces in general. One exception to this rule of thumb is to omit braces for case and break statements because they serve to indicate the beginning and end of a block.

Listing 4.50, with a switch statement, is semantically equivalent to the series if statements in Listing 4.49.

# Listing 4.50: Replacing the if Statement with a switch Statement

```
public static bool ValidateAndMove(
    int[] playerPositions, int currentPlayer, string input)
{
    bool valid = false;

    // Check the current player's input
    switch(input)
    {
        case "1":
        case "2":
        case "3":
        case "4":
        case "5":
        case "6":
        case "7":
        case "8":
        case "0":
            // Save/move as the player directed
            // ...
            valid = true;
            break;
        case "quit":
            valid = true;
            break;
        default:
            // If none of the other case statements
            // is encountered then the text is invalid
            Console.WriteLine(
                "ERROR: Enter a value from 1-9. "
                + "PUSH ENTER to quit");
            break;
    }
}
```