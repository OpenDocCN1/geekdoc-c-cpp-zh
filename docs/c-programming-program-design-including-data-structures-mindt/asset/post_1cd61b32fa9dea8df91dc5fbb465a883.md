
In other words, the Return (or Enter) key on your keyboard cannot be part of the string. That is, in programming code, a string *cannot* be broken into more than one line by using the return (Enter) key on your keyboard.

Recall that the newline character is **\n**, which causes the insertion point to move to the beginning of the next line. There are many escape sequences in C++, which allow you to control the output. Table 2-4 lists some of the commonly used escape sequences.

**TABLE 2-4  Commonly Used Escape Sequences**

| Escape Sequence | Description |
|---|---|
| `\n` | Newline — Cursor moves to the beginning of the next line |
| `\t` | Tab — Cursor moves to the next tab stop |
| `\b` | Backspace — Cursor moves one space to the left |
| `\r` | Return — Cursor moves to the beginning of the current line (not the next line) |
| `\\` | Backslash — Backslash is printed |
| `\'` | Single quotation — Single quotation mark is printed |
| `\"` | Double quotation — Double quotation mark is printed |

The following example shows the effect of some of these escape sequences.

### EXAMPLE 2-26

The output of the statement:

```cpp
cout << "The newline escape sequence is \\n" << endl;
```

is:

```
The newline escape sequence is \n
```

The output of the statement:

```cpp
cout << "The tab character is represented as '\\t'" << endl;
```

is

```
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

```
The string "Sunny" contains five characters.
```

> **NOTE**
>
> The website accompanying this text contains the C++ program that shows the effect of the statements in Example 2-26. The program is named `Example2_26.cpp`.

To use `cin` and `cout` in a program, you must include a certain header file. The next section explains what this header file is, how to include a header file in a program, and why you need header files in a program. Chapter 3 will provide a detailed explanation of `cin` and `cout`.

## Preprocessor Directives

Only a small number of operations, such as arithmetic and assignment operations, are explicitly defined in C++. Many of the functions and symbols needed to run a C++ program are provided as a collection of libraries. Every library has a name and is referred to by a header file. For example, the descriptions of the functions needed to perform input/output (I/O) are contained in the header file `iostream`. Similarly, the descriptions of some very useful mathematical functions, such as power, absolute, square root, and sine, are contained in the header file `cmath`. If you want to use I/O or math functions, you need to tell the computer where to find the necessary code. You use preprocessor directives and the names of header files to tell the computer the locations of the code provided in libraries. Preprocessor directives are processed by a program called a **preprocessor**.

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

The name of the `namespace` in each of these header files is `std`. Therefore, whenever certain features of a header file in ANSI/ISO Standard C++ are discussed, this book will refer to the identifiers without the prefix `std::`. Moreover, to simplify the accessing of identifiers in programs, the statement `using namespace std;` will be included. Also, if a program uses multiple header files, only one `using` statement is needed. This `using` statement typically appears after all the header files.

### Using the `string` Data Type in a Program

Recall that the `string` data type is a programmer-defined data type and is not directly available for use in a program. To use the `string` data type, you need to access its definition from the header file `string`. Therefore, to use the `string` data type in a program, you must include the following preprocessor directive:

```cpp
#include <string>
```

## Creating a C++ Program

In previous sections, you learned enough C++ concepts to write meaningful programs. You are now ready to create a complete C++ program.

A C++ program is a collection of functions, one of which is the function `main`. Therefore, if a C++ program consists of only one function, then it must be the function `main`. Moreover, a function is a set of instructions designed to accomplish a specific task. Until Chapter 6, you will deal mainly with the function `main`.

The statements to declare variables, the statements to manipulate data (such as assignments), and the statements to input and output data are placed within the function `main`. The statements to declare named constants are usually placed outside of the function `main`.

The syntax of the function `main` used throughout this book has the following form:

```cpp
int main()
{
    statement_1
    .
    .
    statement_n

    return 0;
}
```

In the syntax of the function `main`, each statement (`statement_1`, ..., `statement_n`) is usually either a declarative statement or an executable statement. The statement `return 0;` must be included in the function `main` and must be the last statement. If the statement `return 0;` is misplaced in the body of the function `main`, the results generated by the program may not be to your liking. The full meaning of the statement `return 0;` will be discussed in Chapter 6. For now, think of this statement as the end-of-program statement. In C++, `return` is a reserved word.

A C++ program might use the resources provided by the IDE, such as the necessary code to input the data, which would require your program to include certain header files. You can, therefore, divide a C++ program into two parts: preprocessor directives and the program. The preprocessor directives tell the compiler which header files to include in the program. The program contains statements that accomplish meaningful results. Taken together, the preprocessor directives and the program statements constitute the C++ source code. Recall that to be useful, source code must be saved in a file with the file extension `.cpp`. For example, if the source code is saved in the file `firstProgram`, then the complete name of this file is `firstProgram.cpp`. The file containing the source code is called the source code file or source file.

When the program is compiled, the compiler generates the object code, which is saved in a file with the file extension `.obj`. When the object code is linked with the system resources, the executable code is produced and saved in a file with the file extension `.exe`. Typically, the name of the file containing the object code and the name of the file containing the executable code are the same as the name of the file containing the source code. For example, if the source code is located in a file named `firstProg.cpp`, the name of the file containing the object code is `firstProg.obj`, and the name of the file containing the executable code is `firstProg.exe`.

The extensions as given in the preceding paragraph—that is, `.cpp`, `.obj`, and `.exe`—are system dependent. Moreover, some IDEs maintain the projects in the form of projects. The name of the project and the name of the source file need not be the same. It is possible that the name of the executable file is the name of the project, with the extension `.exe`. To be certain, check your system or IDE documentation.

Because the programming instructions are placed in the function `main`, let us elaborate on this function.

The basic parts of the function `main` are the heading and the body. The first line of the function `main`, that is:

```cpp
int main()
```

is called the **heading** of the function `main`.

The statements enclosed between the curly braces (`{` and `}`) form the body of the function `main`. The body of the function `main` contains two types of statements:

- Declaration statements
- Executable statements

**Declaration statements** are used to declare things, such as variables.
