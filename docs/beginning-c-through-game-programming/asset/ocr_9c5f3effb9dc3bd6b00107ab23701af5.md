In the preceding code, I created a copy of the word jumble to...well, jumble. I generated two random positions in the string object and swapped the characters at those positions. I did this a number of times equal to the length of the word.

# Welcoming the Player

Now it's time to welcome the player, which is what I do next.

```
```
cout << "\t\t\tWelcome to Word Jumble!\n\n";
cout << "Unscramble the letters to make a word.\n";
cout << "Enter 'hint' for a hint.\n";
cout << "Enter 'quit' to quit the game.\n\n";
cout << "The jumble is: " << jumble;

string guess;
cout << "\n\nYour guess: ";
cin >> guess;
```
```

I gave the player instructions on how to play, including how to quit and how to ask for a hint.

# Hint

> As enthralling as you think your game is, you should always provide a way for the player to exit it.

# Entering the Game Loop

Next, I enter the game loop.

```
```
while ((guess != theWord) && (guess != "quit"))
{
    if (guess == "hint")
    {
        cout << theHint;
    }
    else
    {
        cout << "Sorry, that's not it.";
    }

    cout <<"\n\nYour guess: ";
```
```