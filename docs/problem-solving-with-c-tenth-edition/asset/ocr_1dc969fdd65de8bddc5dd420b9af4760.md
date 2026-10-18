```
```cpp
if (answer == guess)
{
    cout<< "You're right! You win!" <<endl;
    return true;
}
else if (answer < guess)
    cout<< "Your guess is too high." <<endl;
else
    cout<< "Your guess is too low." <<endl;
return false;
}
void play(Player &player1, Player &player2)
{
    int answer = 0, guess = 0;
    answer = rand() % 100;
    bool win = false;
    while (!win)
    {
        cout<< "Player 1's turn to guess." <<endl;
        guess = player1.getGuess();
        win = checkForWin(guess, answer);
        if (win) return;
        cout<< "Player 2's turn to guess." <<endl;
        guess = player2.getGuess();
        win = checkForWin(guess, answer);
    }
}
```
```

The play function takes as input two Player objects. Define the Player class with a virtual function named getGuess(). The implementation of Player::getGuess() can simply return 0. Next, define a class named HumanPlayer derived from Player. The implementation of HumanPlayer::getGuess() should prompt the user to enter a number and return the value entered from the keyboard. Next, define a class named ComputerPlayer derived from Player. The implementation of ComputerPlayer::getGuess() should randomly select a number between 0 and 99 (see Appendix 4 for information on random number generation). Finally, construct a main function that invokes play(Player &player1, Player &player2) with two instances of a HumanPlayer (human versus human), an instance of a HumanPlayer and ComputerPlayer (human versus computer), and two instances of ComputerPlayer (computer versus computer).

+   11. The computer player in Programming Project 10 does not play very well in the number guessing game, since it only makes random guesses. Modify the program so that the computer plays a more informed game. The specific strategy is up to you, but you must add function(s) to the Player and ComputerPlayer classes so that the play(Player& player1, Player