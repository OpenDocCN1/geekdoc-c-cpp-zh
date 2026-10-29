facilities in C++ are similar to what you would find in other programming languages. Memory management in C++ is similar to that in C. The programmer must allocate his or her own memory and handle his or her own garbage collection. Most compilers will allow you to do C-style memory management in C++, since C is essentially a subset of C++. However, C++ also has its own syntax for a C++ style of memory management, and you are advised to use the C++ style of memory management when coding in C++. This book uses only the C++ style of memory management.

# C++ TERMINOLOGY

All procedure-like entities are called functions in C++. Things that are called procedures, methods, functions, or subprograms in other languages are all called functions in C++. As we will see in the next subsection, a C++ program is basically just a function called main; when you run a program, the run-time system automatically invokes the function named main. Other C++ terminology is pretty much the same as most other programming languages, and in any case, will be explained when each concept is introduced.

# A SAMPLE C++ PROGRAM

Display 1.1 contains a simple C++ program and two possible screen displays that might be generated when a user runs the program. A C++ program is really a function definition for a function named main. When the program is run, the function named main is invoked. The body of the function main is enclosed in braces, {}. When the program is run, the statements in the braces are executed.

The following two lines set up things so that the libraries with console input and output facilities are available to the program. The details concerning these two lines and related topics are covered in Section 1.3 and in Chapters 9, 11, and 12.

```
#include <iostream>
using namespace std;
```

The following line says that main is a function with no parameters that returns an int (integer) value:

```
int main()
```

Some compilers will allow you to omit the int or replace it with void, which indicates a function that does not return a value. However, the above form is the most universally accepted way to start the main function of a C++ program.

The program ends when the following statement is executed:

```
return 0;
```

This statement ends the invocation of the function main and returns 0 as the function's value. According to the ANSI/ISO C++ standard, this statement is not required, but many compilers still require it. Chapter 3 covers all these details about C++ functions.