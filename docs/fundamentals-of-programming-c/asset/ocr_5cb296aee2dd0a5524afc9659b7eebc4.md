# 3.7. CHARACTERS

since a string cannot be assigned to a character variable.

Internally, char are stored as integer values, and C++ permits assigning numeric values to char variables and assigning characters to numeric values. The statement

```
ch = 65;
```

assigns a number to a char to show that this is perfectly legal. The value 65 is the ASCII code for the character A. If ch is printed, as in

```
ch = 65;
cout << ch;
```

the corresponding character, A, would be printed ch's declared type is char, not int or some other numeric type.

Listing 31.1: charexample.cpp shows how characters can be used within a program.

```
Listing 31.1: charexample.cpp
#include <iostream>

using namespace std;

int main() {
    char ch1, ch2;
    ch1 = 65;
    ch2 = 'A';
    cout << ch1 << " " << ch2 << " " << 'A' << endl;
}
```

The program displays

A, A, A

The first A is printed because the statement

```
ch1 = 65;
```

assigns the ASCII code for A to ch1. The second A is printed because the statement

```
ch2 = 'A';
```

assigns the literal character A to ch2. The third A is printed because the literal 'A' is sent directly to the output stream.

Integers can be freely assigned to each other, but the range of chars is much smaller than the range of ints, so care must be taken when assigning an int value to a char variable.

Some characters are non-printable characters. The ASCII chart lists several common non-printable characters:

+   * '
'—the newline character
* ''—the carriage return character
* ''—the backspace character