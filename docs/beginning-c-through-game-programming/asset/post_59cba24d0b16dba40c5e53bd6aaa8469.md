
structures. Although they are not official containers, they look and feel just like them. Table 4.1 lists the container types offered by the STL.

Table 4.1 STL Containers

| Container | Type | Description |
|---|---|---|
| deque | Sequential | Double-ended queue |
| list | Sequential | Linear list |
| map | Associative | Collection of key/value pairs in which each key is associated with exactly one value |
| multimap | Associative | Collection of key/value pairs in which each key may be associated with more than one value |
| multiset | Associative | Collection in which each element is not necessarily unique |
| priority_queue | Adaptor | Priority queue |
| queue | Adaptor | Queue |
| set | Associative | Collection in which each element is unique |
| stack | Adaptor | Stack |
| vector | Sequential | Dynamic array |

## PLANNING YOUR PROGRAMS

So far, all the programs you've seen have been pretty simple. The idea of formally planning any of them on paper probably seems like overkill. It's not— planning your programs (even the small ones) will almost always result in time (and frustration) saved.

Programming is a lot like construction. Imagine a contractor building a house for you without a blueprint. Yikes! You might end up with a house that has 12 bathrooms, no windows, and a front door on the second floor. Plus, it probably would cost you 10 times the estimated price. Programming is the same way. Without a plan, you'll likely struggle through the process and waste time. You might even end up with a program that doesn't quite work.

### Using Pseudocode

Many programmers sketch out their programs using pseudocode—a language that falls somewhere between English and a formal programming language. Anyone who understands English should be able to follow pseudocode. Here's an example: Suppose I want to make a million dollars. A worthy goal, but what do I do to achieve it? I need a plan. So I come up with one and put it in pseudocode.

```
If you can think of a new and useful product
Then that's your product
Otherwise
    Repackage an existing product as your product
    Make an infomercial about your product
    Show the infomercial on TV
    Charge $100 per unit of your product
    Sell 10,000 units of your product
```

Even though anyone, even a non-programmer, can understand my plan, my pseudocode feels vaguely like a program. The first four lines resemble an if statement with an else clause, and that's intentional. When you write your plan, you should try to incorporate the feel of the code that you're representing with pseudocode.

### Using Stepwise Refinement

Your programming plan might not be finished after only one draft. Often, pseudocode needs multiple passes before it can be implemented in programming code. Stepwise refinement is one process used to rewrite pseudocode to make it ready for implementation. Stepwise refinement is pretty simple. Basically, it means, “Make it more detailed.” By taking each step described in pseudocode and breaking it down into a series of simpler steps, the plan becomes closer to programming code. Using stepwise refinement, you keep breaking down each step until you feel the entire plan could be fairly easily translated into a program. As an example, take a step from my master plan to make a million dollars:

```
Create an infomercial about your product
```

This might seem like too vague of a task. How do you create an infomercial? Using stepwise refinement, you can break down the single step into several others. So it becomes

```
Write a script for an infomercial about your product
Rent a TV studio for a day
Hire a production crew
Hire an enthusiastic audience
Film the infomercial
```

If you feel these five steps are clear and achievable, then that part of the pseudocode has been thoroughly refined. If you're still unclear about a step, refine it some more. Continue with this process and you will have a complete plan—and a million dollars.

## INTRODUCING HANGMAN

In the Hangman program, the computer picks a secret word and the player tries to guess it one letter at a time. The player is allowed eight incorrect guesses. If he or she fails to guess the word in time, the player is hanged and the game is over. Figure 4.6 shows the game.

![](img/c7e8651578bccd573227f684823b8754_163_0.png)

Figure 4.6

The Hangman game in action

### Planning the Game

Before I write a single line in C++, I plan the game program using pseudocode.

```
Create a group of words
Pick a random word from the group as the secret word
While player hasn't made too many incorrect guesses and hasn't guessed the secret word
    Tell player how many incorrect guesses he or she has left
    Show player the letters he or she has guessed
Show player how much of the secret word he or she has guessed
Get player's next guess
While player has entered a letter that he or she has already guessed
    Get player's guess
Add the new guess to the group of used letters
If the guess is in the secret word
    Tell the player the guess is correct
    Update the word guessed so far with the new letter
Otherwise
    Tell the player the guess is incorrect
    Increment the number of incorrect guesses the player has made
If the player has made too many incorrect guesses
    Tell the player that he or she has been hanged
Otherwise
    Congratulate the player on guessing the secret word
```

Although the pseudocode doesn't account for every line of C++ I'll write, I think it does a good job describing what I need to do. Then I begin writing the program.

### Setting Up the Program

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

Notice that I include a new file—cctype. It's part of the standard library and it includes functions for converting characters to uppercase, which I use so I can compare apples to apples (uppercase to uppercase) when I compare individual characters.

### Initializing Variables and Constants

Next I start the main() function and initialize variables and constants for the game.

```cpp
int main()
{
    //setup
    const int MAX_WRONG = 8;  //maximum number of incorrect guesses allowed

    vector<string> words;  //collection of possible words to guess
    words.push_back("GUESS");
    words.push_back("HANGMAN");
    words.push_back("DIFFICULT");

    srand(static_cast<unsigned int>(time(0)));
    random_shuffle(words.begin(), words.end());
    const string THE_WORD = words[0];  //word to guess
    int wrong = 0;                     //number of incorrect guesses
    string soFar(THE_WORD.size(), '-'); //word guessed so far
    string used = "";                  //letters already guessed

    cout << "Welcome to Hangman. Good luck!\n";
}
```

MAX_WRONG is the maximum number of incorrect guesses the player can make. words is a vector of possible words to guess. I randomize words using the random_shuffle() algorithm, and then I assign the first word in the vector to THE_WORD, which is the secret word the player must guess. wrong is the number of incorrect guesses the player has made. soFar is the word guessed so far by the player. soFar starts out as a series of dashes—one for each letter in the secret word. When the player guesses a letter that's in the secret word, I replace the dash at the corresponding position with the letter.

### Entering the Main Loop

Next I enter the main loop, which continues until the player has made too many incorrect guesses or has guessed the word.

```cpp
//main loop
while ((wrong < MAX_WRONG) && (soFar != THE_WORD))
{
cout << "\n\nYou have " << (MAX_WRONG - wrong);
cout << " incorrect guesses left.\n";
cout << "\nYou've used the following letters:\n" << used << endl;
cout << "\nSo far, the word is:\n" << soFar << endl;
```

### Getting the Player's Guess

Next I get the player's guess.

```cpp
char guess;
cout << "\n\nEnter your guess: ";
cin >> guess;
guess = toupper(guess); //make uppercase since secret word in uppercase
while (used.find(guess) != string::npos)
{
    cout << "\nYou've already guessed " << guess << endl;
    cout << "Enter your guess: ";
    cin >> guess;
    guess = toupper(guess);
}
used += guess;

if (THE_WORD.find(guess) != string::npos)
{
    cout << "That's right! " << guess << " is in the word.\n";
    //update soFar to include newly guessed letter
    for (int i = 0; i < THE_WORD.length(); ++i)
    {
        if (THE_WORD[i] == guess)
        {
            soFar[i] = guess;
        }
    }
}
else
{
    cout << "Sorry, " << guess << " isn't in the word.\n";
    ++wrong;
}
```
