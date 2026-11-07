# MAIN ALGORITHM

+   1. Get the string.
+   2. Call the function `pigLatinString` to find the pig Latin form of the string.
+   3. Output the pig Latin form of the string.

# PROGRAM LISTING

```
```cpp
//*********************************************************************
// Author: D.S. Malik
//
// Program: Pig Latin Strings
// This program reads a string and outputs the pig Latin form
// of the string.
//*********************************************************************

#include <iostream>
#include <string>

using namespace std;

bool isVowel(char ch);
string rotate(string pstr);
string pigLatinString(string pstr);

int main()
{
    string str;

    cout << "Enter a string: ";
    cin >> str;
    cout << endl;

    cout << "The pig Latin form of " << str << " is: "
         << pigLatinString(str) << endl;

    return 0;
}
//Place the definitions of the functions isVowel, rotate, and
//pigLatinString and as described previously here.
```
```

**Sample Runs:** In these sample runs, the user input is shaded.

# Sample Run 1:

Enter a string: `eye`

The pig Latin form of eye is: eye-way