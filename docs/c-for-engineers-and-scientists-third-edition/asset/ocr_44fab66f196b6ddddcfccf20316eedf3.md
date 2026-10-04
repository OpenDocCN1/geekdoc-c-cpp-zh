# Chapter 2

# Point of Information

The Character '\n' and the String "\n"
The compiler recognizes both '\n' and "\\n\" as containing the newline character. The difference is in the data type used. Formally, '\n' is a character literal, and "\n\" is a string literal. From a practical standpoint, both cause the same thing to happen: A new line is forced in the output display, encountering the character value '\n', however, the compiler translates it by using the ASCII code 00000010 (see Table 2.4). In encoding the string value '\n", the compiler translates it by using the correct character code but also adds an end-of-string character, which is '\0'.

Good programming practice requires ending the last output with a newline sequence. This practice ensures that the first line of output from one program doesn't end on the last line displayed by the previously executed program.

![](bbox=[0.107, 0.383, 0.178, 0.423])

# Program 2.5

```
#include <iostream>
using namespace std;

int main() {
cout << "\nData Type Bytes"
<< "\n----------------------"
     << "\nint " << sizeof(int)
     << "\nchar " << sizeof(char)
     << "\nnbool " << sizeof(bool)
     << "\n";

  return 0;
}
```

In Program 2.5, notice that a single character value is inserted in the display by enclosing it in single quotation marks, as in the escape sequence '\n' at the end of the cout statement. In the first five lines displayed, this character is included in each output string. Each time the compiler encounters the newline escape sequence, as a single character or as part of a string, it is translated as a single character that forces the display to start at the beginning of a line. Although quotation marks can be used for the final newline insertion, "\n", they designate a string. When only a single character is being transmitted, and to emphasize that single characters are designated by using single quotation marks, '\n' is used instead of "\n". From a practical standpoint, however, both notations force a new line in the display.