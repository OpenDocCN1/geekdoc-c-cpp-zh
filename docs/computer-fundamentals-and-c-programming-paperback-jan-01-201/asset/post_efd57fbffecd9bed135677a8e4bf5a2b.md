
16.2 Consider the following statements that create space for an array of eight ints:

```c
p = malloc(8 * sizeof(int));
p = calloc(8, sizeof(int));
```

Assuming that int uses four bytes, will the same statements work for storing an array of 16 two-byte short integers or a string of 32 characters? Explain with reasons.

16.3 Why should you never write code in the following way?

```c
int *p = malloc(20);
*p = 10;
printf("*p = %d\n", *p);
p = calloc(10, sizeof(short));
```

16.4 List the steps involved in adding and deleting a node in a linked list at any location other than the beginning or end.

16.5 Compare the attributes of the array and linked list and explain the circumstances where one is preferred to the other.

### Programming & Debugging Skills

*Use of array notation is not permitted for the exercises in this section.*

16.1 Point out the errors in the following program:

```c
#include <stdio.h>
#include <stdlib.h>
int main(void)
{
    int *p;
    p = malloc(1, sizeof int);
    *p = 200;
    printf("*p = %d\n", *p);
    return 0;
}
```

16.2 Write a program to accept two integers from the keyboard. Using `malloc`, save them in a single memory block. Print the numbers and their average without using a temporary variable.

16.3 Modify Program C16.2 to accept the integers as command-line arguments. Include error checking to ensure that two arguments are provided by the user.

16.4 Write a program that uses `malloc` to create space for storing 10 integers. Using a loop and the `pow` function of the math library, fill up the space with values of 2 raised to the power n where n varies from 1 to 10. Print the values.

16.5 Write a program that uses `calloc` to create a memory block for storing 10 integers. Save the values of two integers at the end of the block with user input and print the contents of the entire block using a loop. Could the output differ if `malloc` is used instead of `calloc`?

16.6 Write a program that uses `calloc` to create space for an array of 10 pointers to strings. Key in a string (maximum length = 80), save it using `malloc` and store its pointer in the fifth array element.

16.7 Write a program that uses `calloc` for storing an array of two integers and initializes the elements to 1234 and 4321. Overwrite the same space to store four short integers that are input from the keyboard. Print both sets of values.

16.8 What is the following code meant to do and why doesn't it work? What does `printf` otherwise display?

```c
short *p = malloc(8);
printf("Size of block = %d\n", sizeof(p));
*p = 10; *(p + 1) = 20;
free(p + 2);
```

16.9 Write a program that creates an optimized structure comprising the name of the region (maximum = 100 characters), carpet area (maximum = 10,000 sqft) and rate/sqft (maximum = Rs 20,000). Enter the details of two apartments, store the data of one using `calloc` and the other using `realloc`.

16.10 Write a program to create space for an array of 10 int elements using `calloc`. Assign a few elements with non-zero values input from the keyboard using `EOF` to terminate input. Compute the count of values by examining the memory block. Print the count and the entered values before resizing this memory block with `realloc` to free unused space. Will this program work with `malloc` instead of `calloc`?

16.11 Write a program to create a linked list of two nodes containing a data field of type short and the `next` field. Populate the two nodes with keyboard input and `malloc`, and print their contents.

16.12 Modify Program C16.11 to repeat the exercise for n nodes where n is keyed in by the user. Print the contents of the list in reverse order.

## 17 The Preprocessor and Other Features

### What to Learn

- How the preprocessor enhances the productivity of a programmer.
- Creating *named constants* and *macros* with `#define`.
- Using `#include` to make common declarations available to multiple programs.
- Conditionally executing program segments with `#ifdef` and `#if`.
- Setting and clearing individual bits in an integer with the *bitwise* operators.
- Executing a function by passing its pointer as an argument to another function.
- Designing functions that accept a variable number of arguments.
- Organizing a program across multiple files.

### 17.1 The Preprocessor

The preprocessor is a separate program that is invoked at the beginning of the compilation process. Using special instructions, called *directives*, the preprocessor modifies a source program before it is seen by the compiler. A directive begins with the # symbol followed by a keyword and other text. For instance, the preprocessor acts on the directive `#define SIZE 20` by replacing SIZE with 20 wherever it occurs in the program. All directives are eventually removed from the source code so the compiler never gets to see them.

The preprocessor helps create code that is easy to read, maintain and port to multiple machines. Initially, it was not considered to be a part of the C language (even though the directives are included in a C program) until ANSI included it in the C standard (C89 onwards). Preprocessor directives can be categorized into three types (keywords shown in parentheses):

- *Macros* (`#define`) with and without function-like parameters.
- *File inclusion* (`#include`) that enables the contents of a file to be included in a program.
- *Conditional compilation* (`#if`, `#else`, `#endif`, etc.) that enables or disables compilation of certain sections of program code.

The `#define` or macro feature enables the use of an alias to replace a constant or a program segment that is used repeatedly. `#define` can also be used to replace simple functions. We haven't used the latter feature yet, but we have used the other feature in this text:

```c
#define SIZE 40                        Replaces a constant
#define FLUSH_BUFFER while (getchar() != '\n');    Replaces a statement
```

The `#include` feature places the contents of an external file at the point where the directive occurs. Every program in this text contains the following directive that places the contents of the file `stdio.h` in the program:

```c
#include <stdio.h>
```

The conditional compilation feature uses a set of directives that begin with `#if` or `#ifdef` and end with `#endif`. Their "control expression" determines whether or not to include a program segment in the compilation process.

The preprocessor is usually a separate program which is automatically invoked by the compiling software. In Linux systems, this program is represented by the program `cpp` (in `/usr/bin`). In Visual Studio, the executable `cpp.exe` performs the same job. This is how you can generate only the preprocessed output without invoking the compiler:

```
gcc -E foo.c                         Displays preprocessed output on screen
cpp foo.c foo.out                    Saves preprocessed output in foo.out
```

The preprocessor looks for syntax errors in directives, i.e., lines that begin with a `#`. The compiler checks statements that end with a semicolon. Note the following attributes of preprocessor directives:

- The `#` prefix may or may not be followed by whitespace. For instance, both `#define` and `# define` are valid directives. Also, since C89, it is not necessary for the `#` to be located at column 1.
- Unlike C statements, preprocessor directives don't end with a semicolon. If the preprocessor finds one, it either ignores it or treats it as part of the replaced text (for a `#define`). For the latter case, the compiler may output an error.
- Comments can be used in preprocessor directives in the same way (with `/*` and `*/`) they are used in program statements. Like the compiler, the preprocessor simply removes them.
- Most directives use a single line of text. In case a directive needs multiple lines, precede the Enter key for every line (except the last) by a `\`. For instance, the following `#define` directive prints the entire string on a single line:

```c
#define STRING "This is a multi-line \
        text."
```

Spaces before text preserved

So far, we have used the bare essentials of `#define` and `#include`. After these features are examined in detail, you should be able to use a `#define` to replace a function with a macro, or place `#define` and function declarations in a separate file and "include" them in a program. You should also be able to exclude certain parts of a program from the compilation process.
