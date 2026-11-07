
## 2 Introduction to C++ Programming, Input/Output and Operators

> What's in a name? that
> which we call a rose
> By any other name
> would smell as sweet.
>
> —William Shakespeare

> High thoughts must have high
> language.
>
> —Aristophanes

> One person can make a
> difference and every person
> should try.
>
> —John F. Kennedy

### Objectives

In this chapter you'll learn:

- To write simple computer programs in C++.
- To write simple input and output statements.
- To use fundamental types.
- Basic computer memory concepts.
- To use arithmetic operators.
- The precedence of arithmetic operators.
- To write simple decision-making statements.

![](img/b42ba5cd262b1358d16610173f975e4d_73_0.png)

### Comments

Lines 1 and 2

```cpp
// Fig. 2.1: fig02_01.cpp
// Text-printing program.
```

each begin with `//`, indicating that the remainder of each line is a **comment**. You insert comments to *document* your programs and to help other people read and understand them. Comments do not cause the computer to perform any action when the program is run—they’re *ignored* by the C++ compiler and do *not* cause any machine-language object code to be generated. The comment Text-printing program describes the purpose of the program. A comment beginning with `//` is called a **single-line comment** because it terminates at the end of the current line. (*Note:* You also may use comments containing one or more lines enclosed in `/*` and `*/`.)

![](img/b42ba5cd262b1358d16610173f975e4d_75_0.png)

> **Good Programming Practice 2.1**
>
> Every program should begin with a comment that describes the purpose of the program.

### #include Preprocessing Directive

Line 3

```cpp
#include <iostream> // allows program to output data to the screen
```

is a **preprocessing directive**, which is a message to the C++ preprocessor (introduced in Section 1.9). Lines that begin with `#` are processed by the preprocessor *before* the program is compiled. This line notifies the preprocessor to include in the program the contents of the **input/output stream header `<iostream>`**. This header is a file containing information used by the compiler when compiling any program that outputs data to the screen or inputs data from the keyboard using C++’s stream input/output. The program in Fig. 2.1 outputs data to the screen, as we’ll soon see. We discuss headers in more detail in Chapter 6 and explain the contents of `<iostream>` in Chapter 13.

![](img/b42ba5cd262b1358d16610173f975e4d_75_1.png)

> **Common Programming Error 2.1**
>
> Forgetting to include the `<iostream>` header in a program that inputs data from the keyboard or outputs data to the screen causes the compiler to issue an error message.

### Blank Lines and White Space

Line 4 is simply a blank line. You use blank lines, space characters and tab characters (i.e., “tabs”) to make programs easier to read. Together, these characters are known as **white space**. White-space characters are normally *ignored* by the compiler.

### The main Function

Line 5

```cpp
// function main begins program execution
```

is another single-line comment indicating that program execution begins at the next line.

Line 6

```cpp
int main()
```

is a part of every C++ program. The parentheses after main indicate that **main** is a program building block called a **function**. C++ programs typically consist of one or more functions and classes (as you’ll learn in Chapter 3). Exactly one **function** in every program *must* be named main. Figure 2.1 contains only one function. C++ programs begin executing at function main, even if main is not the first function defined in the program. The keyword int to the left of main indicates that main “returns” an integer (whole number) value. A **keyword** is a word in code that is reserved by C++ for a specific use. The complete list of C++ keywords can be found in Fig. 4.3. We’ll explain what it means for a function to “return a value” when we demonstrate how to create your own functions in Section 3.3. For now, simply include the keyword int to the left of main in each of your programs.

The **left brace**, `{`, (line 7) must *begin* the **body** of every function. A corresponding **right brace**, `}`, (line 11) must *end* each function’s body.

### An Output Statement

Line 8

```cpp
std::cout << "Welcome to C++!\\n"; // display message
```

instructs the computer to perform an **action**—namely, to print the characters contained between the double quotation marks. Together, the quotation marks and the characters between them are called a **string**, a **character string** or a **string literal**. In this book, we refer to characters between double quotation marks simply as strings. White-space characters in strings are not ignored by the compiler.

The entire line 8, including `std::cout`, the **<< operator**, the string `"Welcome to C++!\n"` and the **semicolon (;)**, is called a **statement**. Most C++ statements end with a semicolon, also known as a **statement terminator** (we’ll see some exceptions to this soon). Preprocessing directives (like `#include`) do not end with a semicolon. Typically, output and input in C++ are accomplished with **streams** of characters. Thus, when the preceding statement is executed, it sends the stream of characters Welcome to C++!\n to the **standard output stream object—std::cout**—which is normally “connected” to the screen.

> **Common Programming Error 2.2**
>
> *Omitting the semicolon at the end of a C++ statement is a syntax error. The syntax of a programming language specifies the rules for creating proper programs in that language. A syntax error occurs when the compiler encounters code that violates C++’s language rules (i.e., its syntax). The compiler normally issues an error message to help you locate and fix the incorrect code. Syntax errors are also called compiler errors, compile-time errors or compilation errors, because the compiler detects them during the compilation phase. You cannot execute your program until you correct all the syntax errors in it. As you’ll see, some compilation errors are not syntax errors.*

![](img/b42ba5cd262b1358d16610173f975e4d_76_0.png)

> **Good Programming Practice 2.2**
>
> Indent the body of each function one level within the braces that delimit the function’s body. This makes a program’s functional structure stand out and makes the program easier to read.

![](img/b42ba5cd262b1358d16610173f975e4d_76_1.png)

> **Good Programming Practice 2.3**
>
> Set a convention for the size of indent you prefer, then apply it uniformly. The tab key may be used to create indents, but tab stops may vary. We prefer three spaces per level of indent.

![](img/b42ba5cd262b1358d16610173f975e4d_76_2.png)

### The std Namespace

The std:: before cout is required when we use names that we’ve brought into the program by the preprocessing directive `#include <iostream>`. The notation `std::cout` specifies that we are using a name, in this case cout, that belongs to the namespace std. The names cin (the standard input stream) and cerr (the standard error stream)—introduced in Chapter 1—also belong to namespace std. Namespaces are an advanced C++ feature that we discuss in depth in Chapter 23, Other Topics. For now, you should simply remember to include `std::` before each mention of cout, cin and cerr in a program. This can be cumbersome—the next example introduces using declarations and the using directive, which will enable you to omit `std::` before each use of a name in the std namespace.

### The Stream Insertion Operator and Escape Sequences

In the context of an output statement, the << operator is referred to as the stream insertion operator. When this program executes, the value to the operator’s right, the right operand, is inserted in the output stream. Notice that the operator points in the direction of where the data goes. A string literal’s characters normally print exactly as they appear between the double quotes. However, the characters \n are not printed on the screen (Fig. 2.1). The backslash (\\) is called an escape character. It indicates that a “special” character is to be output. When a backslash is encountered in a string of characters, the next character is combined with the backslash to form an escape sequence. The escape sequence \n means newline. It causes the cursor (i.e., the current screen-position indicator) to move to the beginning of the next line on the screen. Some common escape sequences are listed in Fig. 2.2.

| Escape sequence | Description |
|---|---|
| `\n` | Newline. Position the screen cursor to the beginning of the next line. |
| `\t` | Horizontal tab. Move the screen cursor to the next tab stop. |
| `\r` | Carriage return. Position the screen cursor to the beginning of the current line; do not advance to the next line. |
| `\a` | Alert. Sound the system bell. |
| `\\` | Backslash. Used to print a backslash character. |
| `\'` | Single quote. Used to print a single quote character. |
| `\"` | Double quote. Used to print a double quote character. |

**Fig. 2.2**  |  Escape sequences.

### The return Statement

Line 10

```cpp
return 0; // indicate that program ended successfully
```

is one of several means we’ll use to exit a function. When the return statement is used at the end of main, as shown here, the value 0 indicates that the program has terminated successfully. The right brace, }, (line 11) indicates the end of function main. According to the
