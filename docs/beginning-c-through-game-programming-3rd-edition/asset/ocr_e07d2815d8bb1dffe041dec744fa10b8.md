*Show player how much of the secret word he or she has guessed*
*Get player's next guess*
*While player has entered a letter that he or she has already guessed*
*Get player's guess*
*Add the new guess to the group of used letters*
*If the guess is in the secret word*
*Tell the player the guess is correct*
*Update the word guessed so far with the new letter*
*Otherwise*
*Tell the player the guess is incorrect*
*Increment the number of incorrect guesses the player has made*
*If the player has made too many incorrect guesses*
*Tell the player that he or she has been hanged*
*Otherwise*
*Congratulate the player on guessing the secret word*

Although the pseudocode doesn’t account for every line of C++ I’ll write, I think it does a good job describing what I need to do. Then I begin writing the program.

# Setting Up the Program

As usual, I start with some comments and include the files I need.

```
// Hangman
// The classic game of hangman

#include <iostream>
#include <string>
#include <vector>
#include <algorithm>
#include <ctime>
#include <cctype>

using namespace std;
```

Notice that I include a new file—cctype. It’s part of the standard library and it includes functions for converting characters to uppercase, which I use so I can compare apples to apples (uppercase to uppercase) when I compare individual characters.