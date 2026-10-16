
In the following lines, I use MAX_ITEMS to protect myself before adding another item to the hero’s inventory:

```
if (numItems < MAX_ITEMS)
{
    inventory[numItems++] = "healing potion";
}
else
{
    cout << "You have too many items and can't carry another.";
}
```

In the preceding code, I first checked to see whether numItems is less than MAX_ITEMS. If it is, then I can safely use numItems as an index and assign a new string object to the array. In this case numItems is 3, so I assign the string "healing potion" to array position 3. If this hadn’t been the case, then I would have displayed the message, “You have too many items and can’t carry another.”

So what happens if you do attempt to access an array element outside the bounds of the array? It depends, because you’d be accessing some unknown part of the computer’s memory. At worst, if you attempt to assign some value to an element outside the bounds of an array you could cause your program to do unpredictable things and it might even crash.

Testing to make sure that an index number is a valid array position before using it is called bounds checking. It’s critical for you to perform bounds checking when there’s a chance that an index you want to use might not be valid.

## UNDERSTANDING C-STYLE STRINGS

Before string objects came along, C++ programmers represented strings with arrays of characters terminated by a null character. These arrays of characters are now called C-style strings because the practice began in C programs. You can declare and initialize a C-style string like you would any other array:

```
char phrase[] = "Game Over!!!";
```

C-style strings terminate with a character called the null character to signify their end. You can write the null character as '\0'. I didn’t need to use the null character in the previous code because it is stored at the end of the string for me. So technically, phrase has 13 elements. (However, functions that work with

C-style strings will say that phrase has a length of 12, which makes sense and is in line with how string objects work.)

As with any other type of array, you can specify the array size when you define it. So another way to declare and initialize a C-style string is

```
char phrase[81] = "Game Over!!!";
```

The previous code creates a C-style string that can hold 80 printable characters (plus its terminating null character).

C-style strings don’t have member functions. But the cstring file, which is part of the standard library, contains a variety of functions for working with C-style strings.

A nice thing about string objects is that they’re designed to work seamlessly with C-style strings. For example, all of the following are completely valid uses of C-style strings with string objects:

```
string word1 = "Game";
char word2[] = "Over";
string phrase = word1 + word2;

if (word1 != word2)
{
	cout << "word1 and word2 are not equal.\n";
}

if (phrase.find(word2) != string::npos)
{
	cout << "word2 is contained in phrase.\n";
}
```

You can concatenate string objects and C-style strings, but the result is always a string object (so the code char phrase[] = word1 + word2; would produce an error). You can compare string objects and C-style strings using the relational operators. And you can even use C-style strings as arguments in string object member functions.

C-style strings have the same shortcomings as arrays. One of the biggest is that their lengths are fixed. So the moral is: Use string objects whenever possible, but be prepared to work with C-style strings if necessary.

## Using Multidimensional Arrays

As you’ve seen, sequences are great for games. You can use them in the form of a string to store a player’s name, or you can use them in the form of an array to store a list of items in an RPG. But sometimes part of a game cries out for more than a linear list of things. Sometimes part of a game literally requires more dimension. For example, while you could represent a chessboard with a 64-element array, it really is much more intuitive to work with it as a two-dimensional entity of 8 × 8 elements. Fortunately, you can create an array of two or three (or even more) dimensions to best fit your game’s needs.

### Introducing the Tic-Tac-Toe Board Program

The Tic-Tac-Toe Board program displays a tic-tac-toe board. The program displays the board and declares X the winner. Although the program could have been written using a one-dimensional array, it uses a two-dimensional array to represent the board. Figure 3.5 illustrates the program.

You can download the code for this program from the Course Technology website (www.courseptr.com/downloads). The program is in the Chapter 3 folder; the filename is `tic-tac-toe_board.cpp`.

![](img/34f09be0ed6217c465debc4490197d4f_125_0.png)

**Figure 3.5**  
The tic-tac-toe board is represented by a two-dimensional array.

```
for (int j = 0; j < COLUMNS; ++j)
{
    cout << board[i][j];
}

cout << endl;
}
```

By using a pair of nested for loops, I move through the two-dimensional array and display the character elements as I go, forming a tic-tac-toe board.

## INTRODUCING WORD JUMBLE

Word Jumble is a puzzle game in which the computer creates a version of a word where the letters are in random order. The player has to guess the word to win the game. If the player is stuck, he or she can ask for a hint. Figure 3.6 shows the game.

![](img/34f09be0ed6217c465debc4490197d4f_128_0.png)

Figure 3.6
Hmm...the word looks "jumbled."

## Real World

Even though puzzle games don’t usually break into the top-ten list of games, major companies still publish them year after year. Why? For one simple reason: They’re profitable. Puzzle games, while not usually blockbusters, can still sell well. There are many gamers out there (casual and hardcore) who are drawn to the Zen of a well-designed puzzle game. And puzzle games cost much less to produce than the high-profile games that require large production teams and years of development time.

## Setting Up the Program

As usual, I start with some comments and include the files I need. You can download the code for this program from the Course Technology website (www.coursetech.com/downloads). The program is in the Chapter 3 folder; the filename is word_jumble.cpp.

```
// Word Jumble
// The classic word jumble game where the player can ask for a hint

#include <iostream>
#include <string>
#include <cstdlib>
#include <ctime>

using namespace std;
```

## Picking a Word to Jumble

My next task is to pick a word to jumble—the word the player will try to guess. First, I create a list of words and hints:

```
int main()
{
    enum fields {WORD, HINT, NUM_FIELDS};
    const int NUM_WORDS = 5;
    const string WORDS[NUM_WORDS][NUM_FIELDS] =
    {
        {"wall", "Do you feel you're banging your head against something?"},
        {"glasses", "These might help you see the answer."},
        {"labored", "Going slowly, is it?"},
        {"persistent", "Keep at it."},
        {"jumble", "It's what the game is all about."}
    };
};
```

```
cin >> guess;
}
```

The loop continues to ask the player for a guess until the player either guesses the word or asks to quit.

## Saying Goodbye

When the loop ends, the player has either won or quit, so it’s time to say goodbye.

```
if (guess == theWord)
{
    cout << "\nThat's it! You guessed it!\n";
}

cout << "\nThanks for playing.\n";

return 0;
}
```

If the player has guessed the word, I congratulate him or her. Finally, I thank the player for playing.

## SUMMARY

In this chapter, you learned the following concepts:

- The for loop lets you repeat a section of code. In a for loop, you can provide an initialization statement, an expression to test, and an action to take after each loop iteration.
- for loops are often used for counting or looping through a sequence.
- Objects are encapsulated, cohesive entities that combine data (called data members) and functions (called member functions).
- string objects (often just called strings) are defined in the file string, which is part of the standard library. string objects allow you to store a sequence of characters and also have member functions.
- string objects are defined so that they work intuitively with familiar operators, such as the concatenation operator and the relational operators.
