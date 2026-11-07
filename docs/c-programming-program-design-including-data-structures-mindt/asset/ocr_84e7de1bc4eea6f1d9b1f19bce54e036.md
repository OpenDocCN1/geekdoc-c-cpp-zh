This program is divided into the following functions, which the ensuing sections describe in detail.

+   - **displayRules:** This function displays some brief information about the game and its rules.
+   - **validSelection:** This function checks whether a player's selection is valid. The only valid selections are `R`, `r`, `P`, `p`, `S`, and `s`.
+   - **retrievePlay:** Because enumeration types cannot be read directly, this function converts the entered choice (`R`, `r`, `P`, `p`, `S`, or `s`) and returns the appropriate object type.
+   - **gameResult:** This function outputs the players' choices and the winner of the game.
+   - **convertEnum:** This function is called by the function `gameResult` to output the enumeration type values.
+   - **winningObject:** This function determines and returns the winning object.
+   - **displayResults:** After the game is over, this function displays the final results.

# Function `displayRules`

This function has no parameters. It consists only of output statements to explain the game and rules of play. Essentially, this function’s definition is:

```
void displayRules()
{
    cout << "Welcome to the game of Rock, Paper, "
         << "and Scissors." << endl;
    cout << "This is a game for two players. For each "
         << "game, each" << endl;
    cout << "A player selects one of the objects, Rock, "
         << "Paper or Scissors." << endl;
    cout << "The rules for winning the game are: " << endl;
    cout << "1. If both players select the same object, it "
         << "is a tie." << endl;
    cout << "2. Rock breaks Scissors: So player who selects "
         << "Rock wins." << endl;
    cout << "3. Paper covers Rock: So player who selects "
         << "Paper wins." << endl;
    cout << "4. Scissors cut Paper: So player who selects "
         << "Scissors wins." << endl;
    cout << "Enter R or r to select Rock, P or p to select "
         << "Paper, and S or s to select Scissors." << endl;
}
```

# Function `validSelection`

This function checks whether a player’s selection is valid.

```
if selection is 'R' or 'r' or 'S' or 's' or 'P' or 'p', then it
    is a valid selection;
otherwise the selection is invalid.
```