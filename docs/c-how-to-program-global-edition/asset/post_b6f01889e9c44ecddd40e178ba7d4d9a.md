
the call to the macro CIRCLE_AREA is expanded to:

```c
    result = ((3.14159) * (++radius) * (++radius));
```

which increments radius *twice* in the statement. In addition, the result of the preceding statement is *undefined* because C allows a variable to be modified *only once* in a statement. In a function call, the argument is evaluated *only once before* it's passed to the function. So, functions are always preferred to unsafe macros.

## Summary

### Section 13.1 Introduction
- The preprocessor (p. 551) executes before a program is compiled.
- All preprocessor directives (p. 551) begin with #.
- Only whitespace characters and comments may appear before a preprocessor directive on a line.

### Section 13.2 #include Preprocessor Directive
- The #include directive (p. 551) includes a copy of the specified file. If the filename is enclosed in quotes, the preprocessor begins searching in the same directory as the file being compiled for the file to be included. If the filename is enclosed in angle brackets (< and >), as is the case for C standard library headers, the search is performed in an implementation-defined manner.

### Section 13.3 #define Preprocessor Directive: Symbolic Constants
- The #define preprocessor directive (p. 552) is used to create symbolic constants and macros.
- A symbolic constant (p. 552) is a name for a constant.

### Section 13.4 #define Preprocessor Directive: Macros
- A macro is an operation defined in a #define preprocessor directive. Macros may be defined with or without arguments (p. 553).
- Replacement-text (p. 552) is specified after a symbolic constant's identifier or after the closing right parenthesis of a macro's argument list. If the replacement-text for a macro or symbolic constant is longer than the remainder of the line, a backslash (\) is placed at the end of the line, indicating that the replacement-text continues on the next line.
- Symbolic constants and macros can be discarded by using the #undef preprocessor directive (p. 554). Directive #undef "undefines" the symbolic constant or macro name.
- The scope (p. 554) of a symbolic constant or macro is from its definition until it's undefined with #undef or until the end of the file.

### Section 13.5 Conditional Compilation
- Conditional compilation (p. 555) enables you to control the execution of preprocessor directives and the compilation of program code.
- The conditional preprocessor directives evaluate constant integer expressions. Cast expressions, sizeof expressions and enumeration constants cannot be evaluated in preprocessor directives.
- Every #if construct ends with #endif (p. 555).
- Directives #ifdef and #ifndef (p. 555) are provided as shorthand for #if defined(name) and #if !defined(name).
- Multiple-part conditional preprocessor constructs may be tested with directives #elif and #else (p. 555).

13.2 Write a program to print the values of the predefined symbolic constants listed in Fig. 13.1.

13.3 Write a preprocessor directive to accomplish each of the following:
- a) Define symbolic constant YES to have the value 1.
- b) Define symbolic constant NO to have the value 0.
- c) Include the header common.h. The header is found in the same directory as the file being compiled.
- d) Renumber the remaining lines in the file beginning with line number 3000.
- e) If symbolic constant TRUE is defined, undefine it and redefine it as 1. Do not use #ifdef.
- f) If symbolic constant TRUE is defined, undefine it and redefine it as 1. Use the #ifdef preprocessor directive.
- g) If symbolic constant TRUE is not equal to 0, define symbolic constant FALSE as 0. Otherwise define FALSE as 1.
- h) Define macro CUBE_VOLUME that computes the volume of a cube. The macro takes one argument.

## Answers to Self-Review Exercises

13.1 a) #. b) #elif. c) #define. d) whitespace. e) #undef. f) #ifdef, #ifndef. g) Conditional compilation. h) assert. i) #include. j) #. k) #. l) `\`.

13.2 See below. [Note: `__STDC__` works in Visual C++ only with the /Za compiler flag.]

```c
1  // Print the values of the predefined macros
2  #include <stdio.h>
3  int main(void)
4  {
5     printf("__LINE__ = %d\n", __LINE__);
6     printf("__FILE__ = %s\n", __FILE__);
7     printf("__DATE__ = %s\n", __DATE__);
8     printf("__TIME__ = %s\n", __TIME__);
9     printf("__STDC__ = %s\n", __STDC__);
10 }
```

```
__LINE__ = 5
__FILE__ = ex13_02.c
__DATE__ = Jan 5 2012
__TIME__ = 09:38:58
__STDC__ = 1
```

- a) `#define YES 1`
- b) `#define NO 0`
- c) `#include "common.h"`
- d) `#line 3000`
- e) `#if defined(TRUE)`
   `#undef TRUE`
   `#define TRUE 1`
   `#endif`
- f) `#ifdef TRUE`
   `#undef TRUE`
   `#define TRUE 1`
   `#endif`

## Other C Topics

## 14

## Objectives

In this chapter, you'll:
- Redirect program input to come from a file.
- Redirect program output to be placed in a file.
- Write functions that use variable-length argument lists.
- Process command-line arguments.
- Compile multiple-source-file programs.
- Assign specific types to numeric constants.
- Terminate programs with exit and atexit.
- Process external asynchronous events in a program.
- Dynamically allocate arrays and resize memory that was dynamically allocated previously.

## Outline
- 14.1 Introduction
- 14.2 Redirecting I/O
- 14.2.1 Redirecting Input with <
- 14.2.2 Redirecting Input with |
- 14.2.3 Redirecting Output
- 14.3 Variable-Length Argument Lists
- 14.4 Using Command-Line Arguments
- 14.5 Compiling Multiple-Source-File Programs
  - 14.5.1 `extern` Declarations for Global Variables in Other Files
  - 14.5.2 Function Prototypes
- 14.5.3 Restricting Scope with `static`
- 14.5.4 Makefiles
- 14.6 Program Termination with `exit` and `atexit`
- 14.7 Suffixes for Integer and Floating-Point Literals
- 14.8 Signal Handling
- 14.9 Dynamic Memory Allocation: Functions `calloc` and `realloc`
- 14.10 Unconditional Branching with `goto`

*Summary* | *Self-Review Exercise* | *Answers to Self-Review Exercise* | *Exercises*

## 14.1 Introduction

This chapter presents additional topics not ordinarily covered in introductory courses. Many of the capabilities discussed here are specific to particular operating systems, especially Linux/UNIX and Windows.

## 14.2 Redirecting I/O

In command-line applications, normally the input is received from the *keyboard* (standard input), and the output is displayed on the *screen* (standard output). On most computer systems—Linux/UNIX, Mac OS X and Windows systems in particular—it is possible to redirect inputs to come from a *file* rather than the keyboard and redirect outputs to be placed in a *file* rather than on the screen. Both forms of redirection can be accomplished without using the file-processing capabilities of the standard library (e.g., by changing your code to use `fprintf` rather than `printf`, etc.). Students often find it difficult to understand that redirection is an operating-system function, not another C feature.

### 14.2.1 Redirecting Input with <

There are several ways to redirect input and output from the command line—that is, a Command Prompt window in Windows, a shell in Linux or a Terminal window in Mac OS X. Consider the executable file `sum` (on Linux/UNIX systems) that inputs integers one at a time and keeps a running total of the values until the end-of-file indicator is set, then prints the result. Normally the user inputs integers from the keyboard and enters the end-of-file key combination to indicate that no further values will be input. With input redirection, the input can be read from a file. For example, if the data is stored in file `input`, the command line

```
    $ sum < input
```

executes the program `sum`; the redirect input symbol (<) indicates that the data in file `input` is to be used as the program's input. Redirecting input on a Windows system or a Terminal window on OS X is performed identically. The character `$` shown in the line above is a typical Linux/UNIX command-line prompt (some systems use a `%` prompt or other symbol).
