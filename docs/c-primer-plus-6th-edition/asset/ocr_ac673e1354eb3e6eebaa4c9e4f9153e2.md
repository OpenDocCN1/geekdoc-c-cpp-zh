# Chapter 3 Dealing with Data

When you're displaying a number, endl is a bit easier to type than "\n" or '\n', when you're displaying a string, ending the string with a newline character requires less typing:

```
cout << x << endl;           // easier than cout << x << "\n"
cout << "Dr. X.\n";      // easier than cout << "The Dr. X." << endl;
```

Finally, you can use escape sequences by the octal or hexadecimal codes for a character. For example, Ctrl+Z is an ASCII code of 26, which is 032 in octal and 0xa in hexadecimal. You can represent this character with either of the following escape sequences: \032 or \xa. You can make constants out of these by enclosing them in single quotes, as in '\032', and you use them as parts of a string, as in "hi\xa there".

# Tip

When you choose to use a numeric escape sequence or a symbolic escape sequence, as in \0x8 versus \b, use the symbolic code. The numeric representation is tied to a particular code, such as ASCII, but the symbolic representation works with all codes and is more readable.

Listing 3.7 demonstrates a few escape sequences. It uses the alert character to get your attention, the newline character to advance the cursor (one small step for a cursor, giant step for cursor), and the backspace character to back the cursor one space to the left (Houdini once a picture of the Hudson River using only escape sequences; he was, of course, a great artist.)

# Listing 3.7 bondini.cpp

```
// bondini.cpp -- using escape sequences
#include <iostream>
int main()
{
    using namespace std;
    cout << "\aHyperType\" is now activated!\n";n    cout << "\aEnter your agent code: \b\b\b\b\b\b";n    long code;
    cin >> code;
    cout << "\aYou entered " << code << "...\n";
    cout << "\aCode verified: Proceed with Plan Z!\n";n    return 0;
}
```

# Note

Some systems might behave differently, displaying the \b as a small rectangle rather than backspacing, for example, or erasing while backspacing, perhaps ignoring \a.