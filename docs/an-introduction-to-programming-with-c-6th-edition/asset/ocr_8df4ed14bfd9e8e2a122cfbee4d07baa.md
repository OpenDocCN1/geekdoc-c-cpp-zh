# APPENDIX A Answers to Mini-Quizzes and Labs

```
//clear the screen
system("cls");

//start guessing
cout << "Guess this word: " <<
displayWord << endl;
while (gameOver == 'N')
{
    cout << "Enter an uppercase letter: ";
    cin >> letter;

    //search for the letter in the original word
for (int x = 0; x < numChars; x += 1)
    {
        //if the current character matches
        //the letter, replace the corresponding
        //dash in the display variable and
        //set the dashReplaced variable to 'Y'
        if (origWord.substr(x, 1) == letter)
        {
            displayWord.replace(x, 1, letter);
            dashReplaced = 'Y';
        }
    }

    //if a dash was replaced, check whether
    //displayWord variable contains any dashes
    if (dashReplaced == 'Y')
    {
        //if the displayWord variable does not
        //contain any dashes, the game is over
        if (displayWord.find("-", 0) == -1)
        {
            gameOver = 'Y';
            cout << "Yes, the word is " <<
            origWord << endl;
            cout << "Great guessing!" << endl;
        }
        else //otherwise, continue guessing
        {
            cout << "Guess this word: " <<
            displayWord << endl;
            dashReplaced = 'N';
        }
    }
    else //processed when dashReplaced contains 'N'
    {
        //add 1 to the number of incorrect guesses
        numIncorrect += 1;
        //if the number of incorrect guesses is 10,
        if (numIncorrect == 10)
        {
            gameOver = 'Y';
        }
    }
}
```