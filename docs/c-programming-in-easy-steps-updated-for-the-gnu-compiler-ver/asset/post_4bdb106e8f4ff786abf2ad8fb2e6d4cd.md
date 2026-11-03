
## 1 Getting Started

*Welcome to the world of C. This chapter demonstrates how to create a C program in text, then how to compile it into executable byte form.*

- 8 Introducing the C language
- 10 Installing a C compiler
- 12 Writing a C program
- 14 Compiling a C program
- 16 Understanding compilation
- 18 Summary

### Introducing the C language

![](img/d1dfb0563339ba187decb78799155b7f_9_0.png)

Dennis M Ritchie, creator of the C programming language.

C is a compact, general-purpose computer programming language that was originally developed by Dennis MacAlistair Ritchie for the Unix operating system. It was first implemented on the Digital Equipment Corporation PDP-11 computer in 1972.

This new programming language was named “C” as it succeeded an earlier programming language named “B” that had been introduced around 1970.

The Unix operating system and virtually all Unix applications are written in the C language. However, C is not limited to a particular platform and programs can be created on any machine that supports C, including those running the Windows platform.

The flexibility and portability of C made it very popular and the language was formalized in 1989 by the American National Standards Institute (ANSI). The ANSI standard unambiguously defined each aspect of C, thereby eliminating previous uncertainty about the precise syntax of the language.

ANSI C has become the recognized standard for the C language and is described, and demonstrated by examples, in this book.

### Why learn C programming?

The C language has been around for quite some time and has seen the introduction of newer programming languages like Java, C++, and C#. Many of these new languages are derived, at least in part, from C – but are much larger in size. The more compact C is better to start out in programming because it’s simpler to learn.

It is easier to move on to learn the newer languages once the principles of C programming have been grasped. For instance, C++ is an extension of C and can be difficult to learn unless you have mastered C programming first.

Despite the extra features available in newer languages, C remains popular because it is versatile and efficient. It is used today on a large number of platforms, for everything from micro-controllers to the most advanced scientific systems. Programmers around the world embrace C because it allows them maximum control and efficiency in their programs.

![](img/d1dfb0563339ba187decb78799155b7f_9_1.png)

Programs written 20 years ago in C are still just as valid today as they were back then.

### Standard C libraries

ANSI C defines a number of standard libraries that contain tried-and-tested functions, which can be used in your own C programs.

The libraries are contained in "header files" that each has a file extension of ".h". The names of the standard C library header files are listed in the table below with a description of their purpose:

| Library | Description |
|---|---|
| stdio.h | Contains input and output functions, types, and macro definitions. This library is used by most C programs and represents almost one third of the entire C libraries |
| ctype.h | Contains functions for testing characters |
| string.h | Contains functions for manipulating strings |
| math.h | Contains mathematical functions |
| stdlib.h | Contains utility functions for number conversion, storage allocation, etc. |
| assert.h | Contains a function that can be used to add diagnostics to a program |
| stdarg.h | Contains a function that can be used to step through a list of function arguments |
| setjmp.h | Contains a function that can be used to avoid the normal call and return sequence |
| signal.h | Contains functions for handling exceptional conditions that may arise in a program |
| time.h | Contains functions for manipulating date and time components |
| limits.h | Contains constant definitions for the size of C data types |
| float.h | Contains constant definitions relating to floating-point arithmetic |

![](img/d1dfb0563339ba187decb78799155b7f_10_0.png)

A function is a piece of code that can be re-used repeatedly in a C program. A description of each function in the C library is given in the Reference section starting on page 161.

- 1. With an internet connection open, launch a web browser then navigate to sourceforge.net/projects/mingw and click the "Download" button to get the MinGW setup installer
- 2. Launch the setup installer and accept the suggested location of C:\MinGW in the "Installation Manager" dialog
- 3. Choose the "Basic" and "C++ Compiler" items then click Installation, Apply Changes to complete the installation
- 4. In Windows' Control Panel, click the System icon then select the Advanced System Settings item to launch the "System Properties" dialog
- 5. In the System Properties dialog, click the Environment Variables button, select the Path system variable, then click the Edit button and add the location C:\MinGW\bin;
- 6. Click OK to close each dialog, then open a "Command Prompt" window and enter the command gcc -v to see the compiler respond with version information

![](img/d1dfb0563339ba187decb78799155b7f_12_0.png)

The MinGW C++ Compiler is a binary executable file located at C:\MinGW\bin. To allow it to be accessible from any system location, this folder should now be added to the System Path:

![](img/d1dfb0563339ba187decb78799155b7f_12_1.png)

![](img/d1dfb0563339ba187decb78799155b7f_12_2.png)

Because C++ is an extension of C, any C++ development tool can also be used to compile C programs.

![](img/d1dfb0563339ba187decb78799155b7f_12_3.png)

Location addresses in the Path statement must end with a ; semi-colon.

![](img/d1dfb0563339ba187decb78799155b7f_12_4.png)

![](img/d1dfb0563339ba187decb78799155b7f_12_5.png)

The MinGW installation process may be subject to change, but current guidance can be found at mingw.org/wiki/Getting_Started

![](img/d1dfb0563339ba187decb78799155b7f_12_6.png)

### Writing a C program

In C programs the code statements to be executed are contained within "functions", which are defined using this syntax format:

*data-type function-name* ( ) { *statements-to-be-executed* }

After a function has been called upon to execute the statements it contains, it can return a value to the caller. This value must be of the data type specified before the function name.

A program can contain one or many functions but must always have a function named "main". The **main()** function is the starting point of all C programs, and the C compiler will not compile the code unless it finds a **main()** function within the program.

Other functions in a program may be given any name you like using letters, digits, and the underscore character, but the name may not begin with a digit. Also, the C keywords, listed in the table on the front inner cover of this book, must be avoided.

The ( ) parentheses that follow the function name may, optionally, contain values to be used by that function. These take the form of a comma-separated list and are known as function "arguments" or "parameters".

The { } curly brackets (braces) contain the statements to be executed whenever that function is called. Each statement must be terminated by a semi-colon, in the same way that English language sentences must be terminated by a period/full stop.

Traditionally, the first program to attempt when learning any programming language is that which simply generates the message "Hello World".

- 1. Open a plain text editor, such as Notepad, then type this line of code at the start of the page, exactly as it is listed `#include <stdio.h>`

The program begins with an instruction to the C compiler to include information from the standard input/output **stdio.h** library file. This makes the functions contained within that library available for use within this program. The instruction is more properly called a "preprocessor instruction" or "preprocessor directive" and must always appear at the start of the page, before the actual program code is processed.

![](img/d1dfb0563339ba187decb78799155b7f_13_0.png)

Do not use word processor applications to create program code as they store additional formatting information that prevents code compilation.

![](img/d1dfb0563339ba187decb78799155b7f_13_1.png)

Preprocessor instructions begin with a # hash character and must enclose standard library names within < > angled brackets.

![](img/d1dfb0563339ba187decb78799155b7f_13_2.png)

hello.c
