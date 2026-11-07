```
case SCISSORS:
    cout << "Scissors";
}
}
```

# Function `winningObject`

To decide the winner of the game, you look at the players’ selections and then at the rules of the game. For example, if one player chooses ROCK and another chooses PAPER, the player who chose PAPER wins. In other words, the winning object is PAPER. The function winningObject, given two objects, decides and returns the winning object. Clearly, this function has two parameters of type objectType, and the value returned by this function is also of type objectType. The definition of this function is:

```
objectType winningObject(objectType play1, objectType play2)
{
    if ((play1 == ROCK && play2 == SCISSORS)
        || (play2 == ROCK && play1 == SCISSORS))
        return ROCK;
    else if ((play1 == ROCK && play2 == PAPER)
             || (play2 == ROCK && play1 == PAPER))
        return PAPER;
    else
        return SCISSORS;
}
```

# Function `displayResults`

After the game is over, this function outputs the final results—that is, the total number of plays and the number of plays won by each player. The total number of plays is stored in the variable gameCount, the number of plays won by player 1 is stored in the variable winCount1, and the number of plays won by player 2 is stored in the variable winCount2. This function has three parameters corresponding to these three variables. Essentially, the definition of this function is:

```
void displayResults(int gCount, int wCount1, int wCount2)
{
    cout << "The total number of plays: " << gCount
         << endl;
    cout << "The number of plays won by player 1: "
         << wCount1 << endl;
    cout << "The number of plays won by player 2: "
         << wCount2 << endl;
}
```

We are now ready to write the algorithm for the function main.

# MAIN ALGORITHM

+   1. Declare the variables.
+   2. Initialize the variables.
+   3. Display the rules.
+   4. Prompt the users to play the game.