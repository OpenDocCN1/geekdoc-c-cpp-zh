Notice that you can put more than one statement on a line or place a statement on more than one line. Except for strings, quotation marks, identifiers, and keywords, C++ ignores all **white space**. (White space refers to any combination of blank spaces, tabs, or new lines.) For example, changing the white space in Program 1.1 and making sur not to split the string `Hello there world!` across two lines results in the following valid program:

```
```cpp
#include <iostream>
using namespace std;
int main
{
}
{
cout <<
"Hello there world!";
    return 0;
}
```
```

Although this version of `main()` does work, it’s an example of poor programming style because it’s difficult to read and understand. For readability, the `main()` function should always be written in this standard form:

```
```cpp
int main()
{
    program statements in here;
    return 0;
}
```
```

In this standard form, the function name starts at the left margin (call this column 1) and is placed with the required parentheses on a line by itself. The opening brace of the function body follows in column 1 on the next line, directly under the first letter of the line containing the function’s name. Similarly, the closing function brace is placed by itself in column 1 (lined up with the opening brace) as the last line of the function. This structure highlights the function as a single unit.

Within the function, all program statements are indented at least two spaces. Indentation is another sign of good programming practice, especially if the same indentation is used for similar groups of statements. Notice in Program 1.2 that the same indentation was used for both cout statements.

As you progress in your understanding and mastery of C++, you’ll develop your own indentation standards. Just keep in mind that the final form of your programs should be consistent and always aids others in reading and understanding your programs.

# Comments

Comments are explanatory remarks made in a program. When used carefully, comments can be helpful in clarifying the overall program’s purpose, explaining what a group of statements is meant to accomplish, or explaining what one line is intended to do. C++ supports two types of comments: line and block. Both types can be placed anywhere in a program and have no effect on program execution. The compiler ignores all comments—they are there only for the convenience of those reading the program.