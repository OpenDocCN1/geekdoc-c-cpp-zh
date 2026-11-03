# # Writing a C program

In C programs the code statements to be executed are contained within "functions", which are defined using this syntax format:

*data-type function-name* ( ) { *statements-to-be-executed* }

After a function has been called upon to execute the statements it contains, it can return a value to the caller. This value must be of the data type specified before the function name.

A program can contain one or many functions but must always have a function named "main". The **main()** function is the starting point of all C programs, and the C compiler will not compile the code unless it finds a **main()** function within the program.

Other functions in a program may be given any name you like using letters, digits, and the underscore character, but the name may not begin with a digit. Also, the C keywords, listed in the table on the front inner cover of this book, must be avoided.

The ( ) parentheses that follow the function name may, optionally, contain values to be used by that function. These take the form of a comma-separated list and are known as function "arguments" or "parameters".

The { } curly brackets (braces) contain the statements to be executed whenever that function is called. Each statement must be terminated by a semi-colon, in the same way that English language sentences must be terminated by a period/full stop.

Traditionally, the first program to attempt when learning any programming language is that which simply generates the message "Hello World".

+   1. Open a plain text editor, such as Notepad, then type this line of code at the start of the page, exactly as it is listed `#include <stdio.h>`

The program begins with an instruction to the C compiler to include information from the standard input/output **stdio.h** library file. This makes the functions contained within that library available for use within this program. The instruction is more properly called a "preprocessor instruction" or "preprocessor directive" and must always appear at the start of the page, before the actual program code is processed.

![](bbox=[0.07, 0.09, 0.24, 0.22])

Do not use word processor applications to create program code as they store additional formatting information that prevents code compilation.

![](bbox=[0.07, 0.38, 0.24, 0.48])

Preprocessor instructions begin with a # hash character and must enclose standard library names within < > angled brackets.

![](bbox=[0.19, 0.71, 0.28, 0.78])

hello.c