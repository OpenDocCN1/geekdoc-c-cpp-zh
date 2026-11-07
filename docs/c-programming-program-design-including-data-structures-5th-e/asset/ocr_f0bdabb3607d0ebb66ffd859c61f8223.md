```
b. else
{
    1. Determine the winning object. (Call function winningObject)
    2. Output each player's choice.
    3. Determine the winning player.
    4. Return the winning player via a reference parameter to the
       function main so that the function main can update the
       winning player's win count.
}

The definition of this function is:

void gameResult(objectType play1, objectType play2,
                int& winner)
{
    objectType winnerObject;

    if (play1 == play2)
    {
        winner = 0;
        cout << "Both players selected ";
        convertEnum(play1);
        cout << ". This game is a tie." << endl;
    }
    else
    {
        winnerObject = winningObject(play1, play2);

        //Output each player's choice
        cout << "Player 1 selected ";
        convertEnum(play1);
        cout << " and player 2 selected ";
        convertEnum(play2);
        cout << ".";

        //Decide the winner
        if (play1 == winnerObject)
            winner = 1;
        else if (play2 == winnerObject)
            winner = 2;

        //Output the winner
        cout << "Player " << winner << " wins this game."
             << endl;
    }
}
```

Function Because enumeration types cannot be output directly, let’s write the function convertEnum to output objects of the enum type objectType. This function has one parameter, of type objectType. It outputs the string that corresponds to the objectType. In pseudocode, this function is: