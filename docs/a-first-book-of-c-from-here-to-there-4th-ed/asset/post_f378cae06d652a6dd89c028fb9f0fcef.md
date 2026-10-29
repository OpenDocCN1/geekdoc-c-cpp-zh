
When Program 1.2 is run, the following is displayed:

```text
Computers, computers everywhere
as far as I can see
```

You might be wondering why the `\n` didn't appear in the output. The characters `\` and `n`, when used together, are called a newline escape sequence. They tell `cout` to send instructions to the display device to move to the beginning of a new line. In C++, the backslash (`\`) character provides an "escape" from the normal interpretation of the character following it and alters its meaning. If the backslash were omitted from the second `cout` statement in Program 1.2, the `n` would be printed as the letter "n," and the program would output the following:

```text
Computers, computers everywheren as far as I can see
```

Newline escape sequences can be placed anywhere in the message passed to `cout`. See whether you can determine the display Program 1.3 produces.

## Program 1.3

```cpp
#include <iostream>
using namespace std;

int main()
{
    cout << "Computers everywhere\n as far as\n\nI can see.";

    return 0;
}
```

This is the output for Program 1.3:

```text
Computers everywhere
as far as

I can see.
```

## EXERCISES 1.3

- 1. (Program) Enter and run Program 1.1 on a computer. (Note: You must understand the procedures for entering and running a C++ program on the particular computer installation you're using.)

- 2. (Program) a. Using `cout`, write a C++ program that prints your name on one line, your street address on a second line, and your city, state, and zip code on the third line.
  - b. Run the program you wrote for Exercise 2a on a computer.

- 3. (Program) a. Write a C++ program to display the following verse:

  ```text
  Computers, computers everywhere
  as far as I can see.
  I really, really like these things,
  Oh joy, Oh joy for me!
  ```

  b. Run the program you wrote for Exercise 3a on a computer.

- 4. (Practice) a. How many `cout` statements would you use to display the following?

  | PART NO. | PRICE |
  |----------|-------|
  | T1267    | $6.34 |
  | T1300    | $8.92 |
  | T2401    | $65.40 |
  | T4482    | $36.99 |

  b. What's the minimum number of `cout` statements that could be used to print the table in Exercise 4a?
  c. Write a complete C++ program to produce the output shown in Exercise 4a.
  d. Run the program you wrote for Exercise 4c on a computer.

- 5. (For thought) In response to a newline escape sequence, `cout` positions the next displayed character at the beginning of a new line. This positioning of the next character actually represents two distinct operations. What are they?

## 1.4 Programming Style

C++ programs start execution at the beginning of the `main()` function. Because a program can have only one starting point, every C++ program must contain one and only one `main()` function. As you have seen, all the statements making up the `main()` function are then included within the braces following the function name. Although the `main()` function must be present in every C++ program, C++ doesn't require placing the word `main`, the parentheses, or the braces in any particular form. The form used in the previous section

```cpp
int main()
{
    program statements in here;
    return 0;
}
```

was chosen strictly for clarity and ease in reading the program but is not required. For example, this general form of a `main()` function also works:

```cpp
int main
( ) { first statement;second statement;
            third statement;fourth
statement;
return 0;}
```

Notice that you can put more than one statement on a line or place a statement on more than one line. Except for strings, quotation marks, identifiers, and keywords, C++ ignores all **white space**. (White space refers to any combination of blank spaces, tabs, or new lines.) For example, changing the white space in Program 1.1 and making sure not to split the string `Hello there world!` across two lines results in the following valid program:

```cpp
#include <iostream>
using namespace std;
int main
(
)
{
cout <<
"Hello there world!";
    return 0;
}
```

Although this version of `main()` does work, it's an example of poor programming style because it's difficult to read and understand. For readability, the `main()` function should always be written in this standard form:

```cpp
int main()
{
    program statements in here;
    return 0;
}
```

In this standard form, the function name starts at the left margin (call this column 1) and is placed with the required parentheses on a line by itself. The opening brace of the function body follows in column 1 on the next line, directly under the first letter of the line containing the function's name. Similarly, the closing function brace is placed by itself in column 1 (lined up with the opening brace) as the last line of the function. This structure highlights the function as a single unit.

Within the function, all program statements are indented at least two spaces. Indentation is another sign of good programming practice, especially if the same indentation is used for similar groups of statements. Notice in Program 1.2 that the same indentation was used for both `cout` statements.

As you progress in your understanding and mastery of C++, you'll develop your own indentation standards. Just keep in mind that the final form of your programs should be consistent and always aids others in reading and understanding your programs.

### Comments

Comments are explanatory remarks made in a program. When used carefully, comments can be helpful in clarifying the overall program's purpose, explaining what a group of statements is meant to accomplish, or explaining what one line is intended to do. C++ supports two types of comments: line and block. Both types can be placed anywhere in a program and have no effect on program execution. The compiler ignores all comments—they are there only for the convenience of those reading the program.

A line comment begins with two slashes (`//`) and continues to the end of the line. For example, the following are line comments:

```text
// this is a comment
// this program prints out a message
// this program calculates a square root
```

The symbols `//`, with no white space between them, designate the start of the line comment. The end of the line on which the comment is written designates the end of the comment. A line comment can be written on a line by itself or at the end of the line containing a program statement. Program 1.4 shows using line comments in a program.

### Program 1.4

```cpp
// this program displays a message
#include <iostream>
using namespace std;

int main()
{
cout << "Hello there world!"; // this produces the display
return 0;
}
```

The first comment appears on a line by itself at the top of the program and describes what the program does. This location is generally a good place to put a short comment describing the program's purpose. If more comments are required, they can be added, one per line. When a comment is too long to be contained on one line, it can be separated into two or more line comments, with each comment preceded by two slashes (`//`). For example, the following comment generates a C++ error message because the second line doesn't start with the `//` symbols:

```text
// this comment is invalid because it
extends over two lines
```

This comment is correct, written as follows:

```text
// this comment is used to illustrate a
// comment that extends across two lines
```

Comments extending across two or more lines are, however, more conveniently written as block comments than as multiple-line comments. Block comments begin with the symbols `/*` and end with the symbols `*/`, as in this example:

```text
/* This is a block comment that
   spans
   three lines */
```

In C++, a program's structure is intended to make it readable and understandable, so extensive comments aren't necessary. This guideline is reinforced by selecting function names carefully to convey their purpose, as discussed previously. However, if the program element's purpose still isn't clear from its structure, name, or context, include comments where clarification is needed.

Obscure code with no comments is a sure sign of bad programming, especially when other people must maintain or read the program. Similarly, excessive comments are a sign of bad programming because not enough thought was given to making the code self-explanatory. Typically, any program you write should begin with comments including a short program description, your name, and the date the program was written or last modified. For space considerations and because all programs in this book were written by the author, these initial comments are used only for short program descriptions when they aren't provided as part of the accompanying text.

## EXERCISES 1.4

- 1. (Debug) a. Will the following program work?

  ```cpp
  #include <iostream>
  using namespace std;
  int main() {cout << "Hello there world!"; return 0;}
  ```

  b. Even if the program in Exercise 1a works, explain why it's not a good program.

- 2. (Modify) Rewrite the following programs to conform to good programming practice and correct syntax:

  a.

  ```cpp
  #include <iostream>
      int main(
      ){
          cout        <<
          "The time has come"
          ; return 0;}
  ```

  b.

  ```cpp
  #include <iostream>
  using namespace std;
      int main
      () { cout << "Newark is a city\n"; cout <<
      "In New Jersey\n"; cout <<
      "It is also a city\n"
      ; cout << "In Delaware\n"
      ; return 0;}
  ```

  c.

  ```cpp
  #include <iostream>
  using namespace std;
      int main() { cout << Reading a program\n"; cout <<
      "is much easier\n"
      ; cout << "if a standard form for main() is used\n")
      ; cout
  ```
