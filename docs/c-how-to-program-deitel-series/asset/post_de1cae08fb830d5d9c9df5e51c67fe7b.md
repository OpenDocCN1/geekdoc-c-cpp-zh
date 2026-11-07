
## Summary

## Section E.2 `#include` Preprocessing Directive

- All preprocessing directives begin with `#` and are processed before the program is compiled.
- Only whitespace characters may appear before a preprocessing directive on a line.
- The `#include` directive includes a copy of the specified file. If the filename is enclosed in quotes, the preprocessor begins searching in the same directory as the file being compiled for the file to be included. If the filename is enclosed in angle brackets (`<` and `>`), the search is performed in an implementation-defined manner.

## Section E.3 `#define` Preprocessing Directive: Symbolic Constants

- The `#define` preprocessing directive is used to create symbolic constants and macros.
- A symbolic constant is a name for a constant.

## Section E.4 `#define` Preprocessing Directive: Macros

- A macro is an operation defined in a `#define` preprocessing directive. Macros may be defined with or without arguments.
- The replacement text for a macro or symbolic constant is any text remaining on the line after the identifier (and, if any, the macro argument list) in the `#define` directive. If the replacement text for a macro or symbolic constant is too long to fit on one line, a backslash (`\`) is placed at the end of the line, indicating that the replacement text continues on the next line.
- Symbolic constants and macros can be discarded using the `#undef` preprocessing directive. Directive `#undef` “undefines” the symbolic constant or macro name.
- The scope of a symbolic constant or macro is from its definition until it is either undefined with `#undef` or the end of the file is reached.

## Section E.5 Conditional Compilation

- Conditional compilation enables you to control the execution of preprocessing directives and the compilation of program code.
- The conditional preprocessing directives evaluate constant integer expressions. Cast expressions, `sizeof` expressions and enumeration constants cannot be evaluated in preprocessing directives.
- Every `#if` construct ends with `#endif`.
- Directives `#ifdef` and `#ifndef` are provided as shorthand for `#if defined(name)` and `#if !defined(name)`.
- A multiple-part conditional preprocessor construct is tested with directives `#elif` and `#else`.

## Section E.6 `#error` and `#pragma` Preprocessing Directives

- The `#error` directive prints an implementation-dependent message that includes the tokens specified in the directive and terminates preprocessing and compiling.
- The `#pragma` directive causes an implementation-defined action. If the pragma is not recognized by the implementation, the pragma is ignored.

## Section E.7 Operators `#` and `##`

- The `#` operator causes the following replacement text token to be converted to a string surrounded by quotes. The `#` operator must be used in a macro with arguments, because the operand of `#` must be an argument of the macro.
- The `##` operator concatenates two tokens. The `##` operator must have two operands.

## Section E.8 Predefined Symbolic Constants

- There are six predefined symbolic constants. Constant `__LINE__` is the line number of the current source-code line (an integer). Constant `__FILE__` is the presumed name of the file (a string). Constant `__DATE__` is the date the source file is compiled (a string). Constant `__TIME__` is the time the source file is compiled (a string). Note that each of the predefined symbolic constants begins (and, with the exception of `__cplusplus`, ends) with two underscores.

## Section E.9 Assertions

- The `assert` macro—defined in the `<cassert>` header file—tests the value of an expression. If the value of the expression is 0 (false), then `assert` prints an error message and calls function `abort` to terminate program execution.

## Self-Review Exercises

- **E.1** Fill in the blanks in each of the following:

  a) Every preprocessing directive must begin with ________.

  b) The conditional compilation construct may be extended to test for multiple cases by using the ________ and the ________ directives.

  c) The ________ directive creates macros and symbolic constants.

  d) Only ________ characters may appear before a preprocessing directive on a line.

  e) The ________ directive discards symbolic constant and macro names.

  f) The ________ and ________ directives are provided as shorthand notation for `#if defined(name)` and `#if !defined(name)`.

  g) ________ enables you to control the execution of preprocessing directives and the compilation of program code.

  h) The ________ macro prints a message and terminates program execution if the value of the expression the macro evaluates is 0.

  i) The ________ directive inserts a file in another file.

  j) The ________ operator concatenates its two arguments.

  k) The ________ operator converts its operand to a string.

  l) The character ________ indicates that the replacement text for a symbolic constant or macro continues on the next line.

- **E.2** Write a program to print the values of the predefined symbolic constants `__LINE__`, `__FILE__`, `__DATE__` and `__TIME__` listed in Fig. E.1.

- **E.3** Write a preprocessing directive to accomplish each of the following:

  a) Define symbolic constant `YES` to have the value 1.

  b) Define symbolic constant `NO` to have the value 0.

  c) Include the header file `common.h`. The header is found in the same directory as the file being compiled.

  d) If symbolic constant `TRUE` is defined, undefine it, and redefine it as 1. Do not use `#ifdef`.

  e) If symbolic constant `TRUE` is defined, undefine it, and redefine it as 1. Use the `#ifdef` preprocessing directive.

  f) If symbolic constant `ACTIVE` is not equal to 0, define symbolic constant `INACTIVE` as 0. Otherwise, define `INACTIVE` as 1.

  g) Define macro `CUBE_VOLUME` that computes the volume of a cube (takes one argument).

## Answers to Self-Review Exercises

- **E.1** a) `#`. b) `#elif`, `#else`. c) `#define`. d) whitespace. e) `#undef`. f) `#ifdef`, `#ifndef`. g) Conditional compilation. h) `assert`. i) `#include`. j) `##`. k) `#`. l) `\`.

The program should define macro `SUM` with two arguments, `x` and `y`, and use `SUM` to produce the output.

- **E.6** Write a program that uses macro `MINIMUM2` to determine the smaller of two numeric values. Input the values from the keyboard.

- **E.7** Write a program that uses macro `MINIMUM3` to determine the smallest of three numerical values. Macro `MINIMUM3` should use macro `MINIMUM2` defined in Exercise E.6 to determine the smallest number. Input the values from the keyboard.

- **E.8** Write a program that uses macro `PRINT` to print a string value.

- **E.9** Write a program that uses macro `PRINTARRAY` to print an array of integers. The macro should receive the array and the number of elements in the array as arguments.

- **E.10** Write a program that uses macro `SUMARRAY` to sum the values in a numeric array. The macro should receive the array and the number of elements in the array as arguments.

- **E.11** Rewrite the solutions to Exercises E.4–E.10 as inline functions.

- **E.12** For each of the following macros, identify the possible problems (if any) when the preprocessor expands the macros:

  a) `#define SQR( x ) x * x`

  b) `#define SQR( x ) ( x * x )`

  c) `#define SQR( x ) ( ( x ) * ( x ) )`

  d) `#define SQR( x ) ( ( x ) * ( x ) )`

![](img/b42ba5cd262b1358d16610173f975e4d_1032_0.png)

## Appendices on the Web

The following appendices are available as PDF documents from this book’s Companion Website, which is accessible from www.pearsonhighered.com/deitel1/:

- Appendix F, C Legacy Code Topics
- Appendix G, UML 2: Additional Diagram Types
- Appendix H, Using the Visual Studio Debugger
- Appendix I, Using the GNU C++ Debugger
- Appendix J, Using the Xcode Debugger
- Appendix K, Test Driving a C++ Program on Mac OS X

These files can be viewed in Adobe® Reader® (get.adobe.com/reader/).

New copies of this book come with a Companion Website access code that is located on the inside of the front cover. If the access code is already visible, you purchased a used book. If there is no access code inside the front cover, you purchased an edition that does not come with an access code. In either case, you can purchase access directly from the Companion Website.
