
# Chapter 4 Compound Types

```cpp
char boss[8] = "Bozo";
```

| B | o | z | o | \0 | \0 | \0 |
|---|---|---|---|---|---|---|
| | | | null character | remaining |
| | | | automatically added at end | set to \0 |

Figure 4.2 Initializing an array to a string.

Note that a string constant (with double quotes) is not interchangeable with a character constant (with single quotes). A character, such as 'S', is a shorthand notation for the code. On an ASCII system, 'S' is just another way of writing 83. Thus, the following statement assigns the value 83 to shirt_size:

```cpp
char shirt_size = 'S'; // this is fine
```

But "S" is not a character constant; it represents the string consisting of two characters, the S and \0 characters. Even worse, "S" represents the memory address at which the string is stored. A statement like the following assigns a memory address to shirt_size:

```cpp
char shirt_size = "S"; // illegal type mismatch
```

Because a string is a separate type in C++, a C++ compiler won't allow this sort of nonsense. (We'll return to this point later in this chapter—we've discussed pointers.)

# Concatenating String Literals

Sometimes a string may be too long to fit on one line of code. C++ enables you to concatenate string literals—that is, to combine two quoted strings into one. Indeed, any two strings separated only by whitespace (spaces, tabs, and newlines) are automatically joined into one. Thus, the following output statements are equivalent to each other:

```cpp
cout << "I'd give my right arm to be " " a great violinist.\n";
cout << "I'd give my right arm to be a great violinist.\n";
cout << "I'd give my right arm ar" "m" to be a great violinist.\n";
```

Note that join adds any spaces to the joined strings. The first character of the second string immediately follows the last character, \0, of the first string. The \0 character from the first is replaced by the first character of the last string.

# Using Strings in an Array

The two most common ways of getting a string into an array are to initialize an array to a string constant and to read keyboard or file input into an array. Listing 4.2 demonstrates these approaches by initializing one array to a quoted string and using cin to place the input into a second array. The program also uses the C library function strlen() to get the length of a string. The standard cstring header file (or string.h for older implementations) provides declarations for this and many other string-related functions.

Listing 4.2 strings.cpp

```cpp
// strings.cpp -- storing strings in an array
#include <iostream>
#include <cstring> // for the strlen()
int main()
{
    using namespace std;
    const int Size = 15;
    char name[Size]; // empty array
    char name2[Size] = "C++Cowboy"; // initialized array
    // NOTE: some implementations may require the static keyword
    // to initialize the array name2

    cout << "Howdy! I'm " << name2 << "\n";
    cout << "! What's your name?\n";
    cin >> name;
    cout << "Well, " << name << ", your name has \n";
    cout << strlen(name) << " letters and is stored\n";
    cout << "In an array of " << sizeof(name) << " bytes.\n";
    cout << "Your initial is " << name[0] << "\n";
    name2[3] = '0'; // set to null character
    cout << "Here are the first 3 characters of my name: \n";
    cout << name2 << endl;

    return 0;
}
```

Here is a sample run of the program in Listing 4.2:

Howdy! I'm C++Cowboy! What's your name?
Basicman
Well, Basicman, your name has 8 letters and is stored
in an array of 15 bytes.
Your initial is B.
Here are the first 3 characters of my name: C++

# Program Notes

What can you learn from Listing 4.2? First, note that the size operator gives the size of the entire array, 15 bytes, but the strlen() function returns the size of the string stored in the array and not the size of the array itself. Also, strlen() counts just the visible characters and not the null character. Thus, it returns a value of 8, not 9, for the length of Basicman. If cosmic is a string, the minimum array size for holding that string is strlen(cosmic) + 1.

Because name1 and name2 are arrays, you can use an index to identify individual characters in the array. For example, the program uses name1[0] to find the first character in that array. Also the program sets name2[3] to the null character. That makes the string end after three characters, even though characters remain in the array (see Figure 4.3).

```cpp
const int ArSize = 15;
char name2[ArSize] = "C++Cowboy";
```

string

| C | + | o | w | b | o | y | \0 |
|---|---|---|---|---|---|---|---|

name2[3] = '\0';

string

| C | + | \0 | w | b | o | y | \0 |
|---|---|---|---|---|---|---|---|

Figure 4.3 Shortening a string

# Adventures in String Input

Listing 4.3 instrl.cpp

```cpp
// instrl.cpp
#include <iostream>
int main()
{
    using namespace std;
    const int ArSize = 20;
    char name[ArSize];
    char dessert[ArSize];

    cout << "Enter your name: ";
    cin >> name;
    cout << "Enter your dessert: ";
    cin >> dessert;
    cout << "Your name is " << name << ".\n";
    cout << "Your dessert is " << dessert << ".\n";

    return 0;
}
```
