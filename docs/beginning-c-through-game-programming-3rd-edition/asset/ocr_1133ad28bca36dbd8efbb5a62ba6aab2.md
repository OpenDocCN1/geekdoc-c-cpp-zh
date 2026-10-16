this program from the Course Technology website (www.courseptr.com/downloads). The program is in the Chapter 1 folder; the filename is game_over2.cpp.

```
// Game Over 2.0
// Demonstrates a using directive

#include <iostream>
using namespace std;

int main()
{
    cout << "Game Over!" << endl;
    return 0;
}
```

# Employing a using Directive

The program starts in the same way. I use two opening comments and then include iostream for output. But next, I have a new type of statement.
using namespace std;

This using directive gives me direct access to elements of the std namespace. Again, if a namespace is like an area code, then this line says that all of the elements in the std namespace should be like local phone numbers to me now. That is, I don’t have to use their area code (the std:: prefix) to access them.

I can use cout and endl, without any kind of prefix. This might not seem like a big deal to you now, but when you have dozens or even hundreds of references to these objects, you’ll thank me.

# Introducing the Game Over 3.0 Program

Okay, there’s another way to accomplish what I did in Game Over 2.0: set up the file so that I don’t have to explicitly use the std:: prefix to access cout and endl. And that’s exactly what I’m going to show you in the Game Over 3.0 program, which displays the same text as its predecessors. You can download the code for this program from the Course Technology website (www.courseptr.com/downloads). The program is in the Chapter 1 folder; the filename is game_over3.cpp.

```
// Game Over 3.0
// Demonstrates using declarations
```