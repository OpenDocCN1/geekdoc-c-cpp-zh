
## 2. Getting Started

Let us take an example. Open a text editor of your choice on whichever operating system, copy the following C++ code and paste it into the text editor. This code only displays *Hello World!!!* on the screen. You do not have to understand the code for now, just learn the compilation and execution procedure.

```cpp
#include <iostream>

using namespace std;

int main()
{
    cout << endl << "Hello World!!!" << endl << endl;
    return 0;
}
```

Save the file at a convenient location as *helloworld.cpp*. Open Command Prompt on Windows or Terminal on Linux/MAC. Navigate to the directory where *helloworld.cpp* has been placed using the *cd* command.

With GCC compiler on Windows, compile the code using the following command:

```bash
g++ helloworld.cpp -o helloworld
```

If the compilation procedure is successful, no error messages will be returned and *helloworld.exe* file will be generated:

```text
P:\cpp> g++ helloworld.cpp -o helloworld
P:\cpp>
```

Cross check whether *helloworld.exe* file is present using the *dir* command or by manually going to the directory using *File Explorer*. Here is the output of the *dir* command:

```text
P:\cpp> g++ helloworld.cpp -o helloworld
P:\cpp> dir
 Volume in drive P is Data
 Volume Serial Number is ...
 Directory of P:\cpp
...
24-05-2018  12:24 ...  helloworld.cpp
24-05-2018  12:24 ...  helloworld.exe
...
P:\cpp>
```

As seen, *helloworld.exe* has been created. To execute, just type *helloworld.exe* and hit Enter. The output should look like this:

```text
P:\cpp> helloworld.exe
Hello World!!!
P:\cpp>
```

This is the compilation and execution procedure that will be followed throughout the course of this book.

If you are using GCC compiler on Linux/MAC, the same command:

```bash
$> g++ helloworld.cpp -o helloworld
```

Should compile the *helloworld.cpp* program and will create an executable file called *helloworld* (and not *helloworld.exe* as in Windows). To execute this file, use the following command:

```bash
$> ./helloworld
```

The following screenshot explains compilation (using g++) and execution procedure on Linux and MAC:

![](img/cda5b023e23ffd0b87fc37b1da33973d_23_0.png)

If you are using Clang compiler on Linux/MAC, use the following command:

```bash
$> clang++ helloworld.cpp -o helloworld
```

This command will compile *helloworld.cpp* and generate an executable file *helloworld*. To execute this file, use the following command:

```bash
$> ./helloworld
```

The following screenshot explains compilation (using clang++) and execution procedure on Linux and MAC.

![](img/cda5b023e23ffd0b87fc37b1da33973d_24_0.png)

Whichever operating system you may be using, you must have realized that the compilation and execution procedure remains more or less the same. In the following sections of the book we will learn several C++ concepts and compile and execute many C++ programs. Whichever OS/Text Editor/Compiler you choose, you should be very comfortable when it comes to compiling a program and then executing it.

## 3. Syntax

C++ is a case sensitive language. This means, “ebook” and “eBook” are treated differently. In this section, we will discuss the basic syntax of C++ and also learn to write a basic program.

### 3.1 Statements

A statement in a programming language carries out some computational function. Statements in C++ end with a semi-colon ( ; ). Although it is possible to have as many statements as desired on one line with each statement being separated with a semi-colon, it is not really recommended as the code will look messy and the code-readability will reduce. It is best practice to have one statement on one line. Some examples of statements are:

```cpp
c = 50;
cout << "Hello World";
int a = c * 2;
```

### 3.2 Blocks

A block is a group of statements enclosed within curly brackets ( { } ). Here is an example:

```cpp
{
    int a, b, c;
    cout << "This is a block";
}
```

The usage of blocks is significant while working with decision making, loops, functions and classes. We will cover each of these in detail in the sections to follow.

### 3.3 Pre-processor directives

Pre-processor directives are statements that begin with a hash (#) symbol. Unlike normal statements, these do not end with a semi-colon and hence each pre-processor directive must be written on a new line. Pre-processor directives are processed before the compilation process begins. In a way, these provide meta information to the compiler. Here are some examples of pre-processor directives:

```cpp
#include <iostream>
#define PI 3.14
#pragma startup myfunction
```

Pre-processor directives other than #include and #define are for advanced programmers, this book covers only the ones required.

### 3.4 Comments

Comments are ignored by the compiler and will not have any effect on the outcome of the compilation process. Usually, comments are explanatory statements but you can use them for any annotation purpose. C++ offers single-line and multi-line comments. Single line comments start with double-slash ( // ) and must terminate on the same line. Multi line comments are like a block of comments and are enclosed within this character sequence -- slash-asterisk ( /* ) and asterisk-slash ( */ ).

#### Single Line Comment Example:

```cpp
//This is a comment
//This is another comment
```

As seen each comment on a new line must begin with a double-slash.

#### Multi Line Comment Example:

```cpp
/*
Comment block begins here.
As many lines can be added within the block.
No need for double slash ( // )
*/
```

### 3.5 Identifiers

Identifiers are used to identify variables, functions, classes & objects, etc. Identifier names can contain alphabets (a-z, A-Z), numbers (0-9) and underscore (_) but cannot start with a number and cannot contain any other special character.

### 3.6 Keywords

Keywords in C++ are reserved words which cannot be used as identifier names. Keywords have a specific meaning which tells the compiler what to do. Here is a list of them in alphabetical order:

| | | | |
| --- | --- | --- | --- |
| asm | else | new | this |
| auto | enum | operator | throw |
| bool | explicit | private | true |
| break | export | protected | try |
| case | extern | public | typedef |
| catch | false | register | typeid |
| char | float | reinterpret_cast | typename |
| class | for | return | union |
| const | friend | short | unsigned |
| const_cast | goto | signed | using |
| continue | if | sizeof | virtual |
| default | inline | static | void |
| delete | int | static_cast | volatile |
| do | long | struct | wchar_t |
| double | mutable | switch | while |
| dynamic_cast | namespace | template | |

### 3.7 Basic C++ Program Structure

A very basic standalone C++ program must have the following constituents:

- 1. `#include <iostream>` Statement:

  As discussed in *Section 3.3*, all statements that start with a hash (#) symbol are pre-processor directives. A **#include** directive instructs the compiler which *header* to include. A *header* contains the definitions of variables, functions and classes & objects which can be used for various purposes. General syntax to include a header is as follows:

```cpp
#include <header here>
Eg:
#include <iostream>
#include <fstream>
```

The **#include** statement can also be used to include header file, either provided by the compiler or user defined local ones (placed in the same directory as the program). To include a local header file, the file name must be placed inside double quotes and not inside angle brackets as follows:

```cpp
#include "my_header_file.h"
```

The **`#include <iostream>`** statement instructs the compiler to include the *iostream* header which provides an **Input/Output Stream** used to read data from the user and display data on the screen. If you want to write a standalone C++ program that interacts with the user either by accepting inputs or displaying something on the screen, you have to place **`#include <iostream>`** in your program, usually on the first few lines.

There are many such built-in headers provided by different compilers. For example, *fstream* header is used for File Input/Output, *iomanip* is used for formatting output to be displayed on the screen, *cmath* provides definitions to carry out mathematical functions and so on. C++ is also backward compatible with most of the conventional C header files (the ones that end with .h), for example – *stdlib.h, stdio.h, math.h,*
