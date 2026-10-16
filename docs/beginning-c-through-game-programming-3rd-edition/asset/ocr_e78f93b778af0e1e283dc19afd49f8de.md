# Real World

Even though puzzle games don’t usually break into the top-ten list of games, major companies still publish them year after year. Why? For one simple reason: They’re profitable. Puzzle games, while not usually blockbusters, can still sell well. There are many gamers out there (casual and hardcore) who are drawn to the Zen of a well-designed puzzle game. And puzzle games cost much less to produce than the high-profile games that require large production teams and years of development time.

# Setting Up the Program

As usual, I start with some comments and include the files I need. You can download the code for this program from the Course Technology website (www.coursetech.com/downloads). The program is in the Chapter 3 folder; the filename is word_jumble.cpp.

```
```cpp
// Word Jumble
// The classic word jumble game where the player can ask for a hint

#include <iostream>
#include <string>
#include <cstdlib>
#include <ctime>

using namespace std;
```
```

# Picking a Word to Jumble

My next task is to pick a word to jumble—the word the player will try to guess. First, I create a list of words and hints:

```
```cpp
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