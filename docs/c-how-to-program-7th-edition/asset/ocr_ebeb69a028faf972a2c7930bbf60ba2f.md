# Lines 1 and 2

```
```cpp
// Fig. 2.1: fig02_01.cpp
// Text-printing program.
```
```

each begin with `//`, indicating that the remainder of each line is a **comment**. You insert comments to document your programs and to help other people read and understand them. Comments do not cause the computer to perform any action when the program is run—they’re ignored by the C++ compiler and do not cause any machine-language object code to be generated. The comment Text-printing program describes the purpose of the program. A comment beginning with `//` is called a **single-line comment** because it terminates at the end of the current line. *[Note: You also may use C’s style in which a comment—possibly containing many lines—begins with `/*` and ends with `*/`.]*

![](bbox=[0.159, 0.334, 0.216, 0.377])

> **Good Programming Practice 2.1**
> 
> *Every program should begin with a comment that describes the purpose of the program.*

# Line 3

```
```cpp
#include <iostream> // allows program to output data to the screen
```
```

is a **preprocessor directive**, which is a message to the C++ preprocessor (introduced in Section 1.14). Lines that begin with `#` are processed by the preprocessor before the program is compiled. This line notifies the preprocessor to include in the program the contents of the input/output stream header file `<iostream>`. This file must be included for any program that outputs data to the screen or inputs data from the keyboard using C++-style stream input/output. The program in Fig. 2.1 outputs data to the screen, as well soon see. We discuss header files in more detail in Chapter 6 and explain the contents of `<iostream>` in Chapter 15.

![](bbox=[0.159, 0.617, 0.216, 0.659])

> **Common Programming Error 2.1**
> 
> *Forgetting to include the `<iostream>` header file in a program that inputs data from the keyboard or outputs data to the screen causes the compiler to issue an error message, because the compiler cannot recognize references to the stream components (e.g., `cout`).*

Line 4 is simply a blank line. You use blank lines, space characters and tab characters (i.e., “tabs”) to make programs easier to read. Together, these characters are known as white space. White-space characters are normally ignored by the compiler. In this chapter and several that follow, we discuss conventions for using white-space characters to enhance program readability.

![](bbox=[0.159, 0.804, 0.216, 0.844])

> **Good Programming Practice 2.2**
> 
> *Use blank lines, space characters and tabs to enhance program readability.*

# Line 5

```
```cpp
// function main begins program execution
```
```

is another single-line comment indicating that program execution begins at the next line.