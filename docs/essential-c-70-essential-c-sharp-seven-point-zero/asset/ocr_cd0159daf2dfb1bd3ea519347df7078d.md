# Guidelines

**DO NOT** use `continue` as the jump statement that exits a `switch` section. This is legal when the `switch` is inside a loop, but it is easy to become confused about the meaning of `break` in a later `switch` section.

A `switch` statement should have at least one `switch` section; `switch(x){}` is legal but will generate a warning. Also, the guideline provided earlier was to avoid omitting braces in general. One exception to this rule of thumb is to omit braces for `case` and `break` statements because they serve to indicate the beginning and end of a block.

Listing 4.49, with a `switch` statement, is semantically equivalent to the series of `if` statements in Listing 4.48.

# **LISTING 4.49:** Replacing the if Statement with a switch Statement

```
```csharp
static bool ValidateAndMove(
    int[] playerPositions, int currentPlayer, string input)
{
    bool valid = false;

    // Check the current player's input
    switch (input)
    {
        case "1" :
        case "2" :
        case "3" :
        case "4" :
        case "5" :
        case "6" :
        case "7" :
        case "8" :
        case "9" :
            // Save/Move as the player directed
            ...
            valid = true;
            break;

        case "" :
        case "quit" :
            valid = true;
            break;

        default :
            // If none of the other case statements
            // is encountered, then the text is invalid
```
```