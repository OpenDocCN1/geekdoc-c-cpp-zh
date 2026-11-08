```
```cpp
int main()
{
    //Step 1
    int gameCount; //variable to store the number of
                   //games played
    int winCount1; //variable to store the number of games
                   //won by player 1
    int winCount2; //variable to store the number of games
                   //won by player 2
    int gamewinner;
    char response; //variable to get the user's response to
                   //play the game
    char selection1;
    char selection2;
    objectType play1; //player1's selection
    objectType play2; //player2's selection

    //Initialize variables; Step 2
    gameCount = 0;
    winCount1 = 0;
    winCount2 = 0;

    displayRules();                                      //Step 3

    cout << "Enter Y/y to play the game: ";              //Step 4
    cin >> response;                                     //Step 5
    cout << endl;
    while (response == 'Y' || response == 'y')           //Step 6
    {
        cout << "Player 1 enter your choice: ";          //Step 6a
        cin >> selection1;                               //Step 6b
        cout << endl;

        cout << "Player 2 enter your choice: ";          //Step 6c
        cin >> selection2;                               //Step 6d
        cout << endl;

        //Step 6e
        if (validSelection(selection1)
            && validSelection(selection2))
        {
            play1 = retrievePlay(selection1);
            play2 = retrievePlay(selection2);
            gameCount++;                                 //Step 6e.i
            gameResult(play1, play2, gamewinner);        //Step 6e.ii

            if (gamewinner == 1)                         //Step 6e.iii
                winCount1++;
            else if (gamewinner == 2)
                winCount2++;
        }//end if
```
```