# how cin works

When a program reaches a cin statement, it waits for input to be entered from the keyboard. It sets the first variable equal the first value typed at the keyboard, the second variable to the second value typed, and so forth. the program does not read the input until user presses the Return key. This allows the user to backtrack and correct mistakes when entering a line of input. Display 1.5 illustrates reading an int and a string in the same program with a simple calculation.

Numbers in the input must be separated by one or more spaces or by a line break. These delimiters are called whitespace. When you use cin statements, the computer will skip any number of spaces or line breaks until it finds the next input value. Thus, it does not matter whether numbers are separated by one space or several spaces or even a line break. This behavior holds when you are reading data into a string. This means sometimes errors occur, as indicated in Display 1.5, Sample Dialogue 2. In this case, the user intends to enter "Mr. Boangles as the name of the pet, but the string is only read up to "Mr." since the next character is a space. The "Boangles" string is ignored by this program would be read if there was another cin statement. Chapter 9 describes a technique to input a string that may include spaces.

You can read integers, floating-point numbers, characters, or strings using cin. Later in this book we will discuss the reading of other kinds of data using cin.

# Display 1.5 Using cin and cout with a string (1 of 2)

```
//Program to demonstrate cin and cout with strings
#include <iostream>
#include <string>
// Needed to access the string class.

using namespace std;
int main() {
    string dogName;
    int actualAge;
    int humanAge;

    cout << "How many years old is your dog?" << endl;
    cin >> actualAge;
    humanAge = actualAge * 7;

    cout << "What is your dog's name?" << endl;
    cin >> dogName;

    cout << dogName << " 's is approximately " <<
        "equivalent to a " << humanAge << " year old human."
        cout << endl;

    return 0;
}
```

(continued)