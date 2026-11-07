
> **NOTE**  
> Outputting or accessing the value of a variable in an expression does not destroy or modify the contents of the variable.

Let us now take a close look at the newline character, `\n`. Consider the following C++ statements:

```cpp
cout << "Hello there.";
cout << "My name is James.";
```

If these statements are executed in sequence, the output is:

```text
Hello there.My name is James.
```

Now consider the following C++ statements:

```cpp
cout << "Hello there.\n";
cout << "My name is James.";
```

The output of these C++ statements is:

```text
Hello there.
My name is James.
```

When `\n` is encountered in the string, the insertion point is positioned at the beginning of the next line. Note also that `\n` may appear anywhere in the string. For example, the output of the statement:

```cpp
cout << "Hello \nthere. \nMy name is James.";
```

is:

```text
Hello
there.
My name is James.
```

Also, note that the output of the statement:

```cpp
cout << '\n';
```

is the same as the output of the statement:

```cpp
cout << "\n";
```

which is equivalent to the output of the statement:

```cpp
cout << endl;
```

Thus, the output of the sequence of statements:

```cpp
cout << "Hello there.\n";
cout << "My name is James.";
```

is equivalent to the output of the sequence of statements:

```cpp
cout << "Hello there." << endl;
cout << "My name is James.";
```

### EXAMPLE 2-23

Consider the following C++ statements:

```cpp
cout << "Hello there.\nMy name is James.";
```

or

```cpp
cout << "Hello there.";
cout << "\nMy name is James.";
```

or

```cpp
cout << "Hello there.";
cout << endl << "My name is James.";
```

In each case, the output of the statements is:

```text
Hello there.
My name is James.
```

### EXAMPLE 2-24

The output of the C++ statements:

```cpp
cout << "Count...\n....1\n......2\n.......3";
```

or

```cpp
cout << "Count..." << endl << "....1" << endl
     << "......2" << endl << ".......3";
```

is:

```text
Count...
....1
......2
.......3
```

### EXAMPLE 2-25

Suppose that you want to output the following sentence in one line as part of a message:

It is sunny, warm, and not a windy day. We can go golfing.

Obviously, you will use an output statement to produce this output. However, in the programming code, this statement may not fit in one line as part of the output statement. Of course, you can use multiple output statements as follows:

```cpp
cout << "It is sunny, warm, and not a windy day. ";
cout << "We can go golfing." << endl;
```

Note the semicolon at the end of the first statement and the identifier `cout` at the beginning of the second statement. Also, note that there is no manipulator `endl` at the end of the first statement. Here, two output statements are used to output the sentence in one line. Equivalently, you can use the following output statement to output this sentence:

```cpp
cout << "It is sunny, warm, and not a windy day. "
     << "We can go golfing." << endl;
```

In this statement, note that there is no semicolon at the end of the first line, and the identifier `cout` does not appear at the beginning of the second line. Because there is no semicolon at the end of the first line, this output statement continues at the second line. Also, note the double quotation marks at the beginning and end of the sentences on each line. The string is broken into two strings, but both strings are part of the same output statement.

If a string appearing in an output statement is long and you want to output the string in one line, you can break the string by using either of the previous two methods. However, the following statement would be incorrect:

```cpp
cout << "It is sunny, warm, and not a windy day.
          We can go golfing." << endl;        //illegal
```

In other words, the return (or Enter) key on your keyboard cannot be part of the string. That is, in programming code, a string *cannot* be broken into more than one line by using the return (Enter) key on your keyboard.

Recall that the newline character is `\n`, which causes the insertion point to move to the beginning of the next line. There are many escape sequences in C++, which allow you to control the output. Table 2-4 lists some of the commonly used escape sequences.

### TABLE 2-4 Commonly Used Escape Sequences

|  | Escape Sequence | Description |
|---|---|---|
| `\n` | Newline | Cursor moves to the beginning of the next line |
| `\t` | Tab | Cursor moves to the next tab stop |
| `\b` | Backspace | Cursor moves one space to the left |
| `\r` | Return | Cursor moves to the beginning of the current line (not the next line) |
| `\\` | Backslash | Backslash is printed |
| `\'` | Single quotation | Single quotation mark is printed |
| `\"` | Double quotation | Double quotation mark is printed |

The following example shows the effect of some of these escape sequences.

### EXAMPLE 2-26

The output of the statement:

```cpp
cout << "The newline escape sequence is \\n" << endl;
```

is:

```text
The newline escape sequence is \n
```

The output of the statement:

```cpp
cout << "The tab character is represented as '\\t'" << endl;
```

is:

```text
The tab character is represented as '\t'
```

Note that the single quote can also be printed without using the escape sequence. Therefore, the preceding statement is equivalent to the following output statement:

```cpp
cout << "The tab character is represented as '\\t'" << endl;
```

The output of the statement:

```cpp
cout << "The string \"Sunny\" contains five characters." << endl;
```

is:

```text
The string "Sunny" contains five characters.
```

> **NOTE**  
> The Web site accompanying this text contains the C++ program that shows the effect of the statements in Example 2-26. The program is named `Example2_26.cpp`.

To use `cin` and `cout` in a program, you must include a certain header file. The next section explains what this header file is, how to include a header file in a program, and why you need header files in a program. Chapter 3 will provide a full explanation of `cin` and `cout`.

## Preprocessor Directives

Only a small number of operations, such as arithmetic and assignment operations, are explicitly defined in C++. Many of the functions and symbols needed to run a C++ program are provided as a collection of libraries. Every library has a name and is referred to by a header file. For example, the descriptions of the functions needed to perform input/output (I/O) are contained in the header file `iostream`. Similarly, the descriptions of some very useful mathematical functions, such as power, absolute, and sine, are contained in the header file `cmath`. If you want to use I/O or math functions, you need to tell the computer where to find the necessary code. You use preprocessor directives and the names of header files to tell the computer the locations of the code provided in libraries. Preprocessor directives are processed by a program called a preprocessor.

Preprocessor directives are commands supplied to the preprocessor that cause the preprocessor to modify the text of a C++ program before it is compiled. All preprocessor commands begin with `#`. There are no semicolons at the end of preprocessor commands because they are not C++ statements. To use a header file in a C++ program, use the preprocessor directive `include`.

The general syntax to include a header file (provided by the IDE) in a C++ program is:

```cpp
#include <headerFileName>
```

For example, the following statement includes the header file `iostream` in a C++ program:

```cpp
#include <iostream>
```

Preprocessor directives to include header files are placed as the first line of a program so that the identifiers declared in those header files can be used throughout the program. (Recall that in C++, identifiers must be declared before they can be used.)

Certain header files are required to be provided as part of C++. Appendix F describes some of the commonly used header files. Individual programmers can also create their own header files, which is discussed in the chapter Classes and Data Abstraction, later in this book.

Note that the preprocessor commands are processed by the preprocessor before the program goes through the compiler.

From Figure 1–3 (Chapter 1), we can conclude that a C++ system has three basic components: the program development environment, the C++ language, and the C++ library. All three components are integral parts of the C++ system. The program development environment consists of the six steps shown in Figure 1–3. As you learn the C++ language throughout the book, we will discuss components of the C++ library as we need them.
