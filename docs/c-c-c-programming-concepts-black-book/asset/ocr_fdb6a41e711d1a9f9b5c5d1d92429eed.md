To conclude, the main feature of any structured language is that its code or data can be compartmentalized. It allows a block of code to differentiate itself and hide itself from the rest of the program. One of the ways to achieve this is to use functions (main structural components of C) and local variables inside that code.

# Writing your First C Program

A program consists of one or multiple modules called functions. One of the functions that need to be always present in a C program is the main function. A program always starts with the execution of the main function and all the other functions are subsequently called from the main function. Function definitions must be declared separately whether before or after the main function. Each function must contain:

+   - A function heading that defines the name of the function. It is followed by a list of arguments, which forms the parameter list for that function. The list of parameters is enclosed inside parenthesis. This list of parameters can also be empty.
+   - An argument list.
+   - A compound statement, which forms the rest of the function.

Arguments represent information that is being passed from one function to another. Each compound statement must be enclosed within a pair of curly braces {}. A compound statement can be nested within the other. Each statement must terminate with a semicolon.

Listing 1.1 shows a simple C program:

Listing 1.1: Showing a Simple C Program

```
```c
/* Writing first C program */

#include<stdio.h>       // Header File Inclusion

main()                  // Defining main function
{                       // Beginning of function
    int test;           // Variable Declaration

    printf("Enter a number ");  // Output Statement
    scanf("%d",&test);          // Input Statement

}                       // End of Function
```
```

In Listing 1.1, you can notice the following things:

+   - The program is written in lower case, which is a standard convention for writing programs in C.
+   - The first line of the program indicates a comment. Use of comments in C increases the readability of the code. There are two standard ways of writing comments in C. Originally, only /* and */ were used for writing comments. However, with the advent of C99 version, we can also use the // sign to write single line comments.
+   - The second line tells us about the inclusion of a special file (stdio.h) that contains the information to be used while compiling the file. This statement is also called the preprocessor directive, as it tells the preprocessor to include the file before compilation starts for the program. The file contains information about the standard input/output library, and these files are also referred to as header files in C.
+   - The third line forms the heading of the main function. Empty parenthesis signifies an empty argument list for the main function.
+   - The next line marks the beginning of the function. Any function written in C must have its body inside curly braces and the main function is no different.
+   - The remaining lines form the body of the main function.