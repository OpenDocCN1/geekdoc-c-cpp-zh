For the Watcom C/C++, IBM VisualAge C/C++, and Microsoft Visual C/C++ compilers, the function main can also be declared to return void. The compilers MetaWare High C/C++ and EMX C/C++ do not allow main to have a return type void. For these compilers, the return type of main has to be declared as int. Borland C/C++, Comeau C/C++, and Digital Mars C/C++ compilers do not explicitly list void main() as a legal definition of main, but somewhat ironically there are example codes using this non-conforming definition on main.

```
```
{
```
```

This is a brace. As the name implies, braces come in packs of two, i.e., for every open brace there must be a matching close. Braces allow to lump pieces of program together. Such a lump of program is often called a block. A block can contain the declaration of variable used within it, followed by a sequence of program statements which are executed in order. In this case, the braces enclose the working parts of the function main. When the compiler sees the matching close brace at the end, it knows that it has reached the end of the function and can look for another (if any).

By enclosing the program instructions, printf() and return 0 within the opening brace ‘{’ and the closing brace ‘}’, a block of program instructions is formed. Such a block of program instructions, within these braces, form the body of the function main().

```
```
printf("C is Sea\n");
```
```

printf() is a ‘library function’.

The \n (pronounced backslash n) in the string argument of the function printf()

```
```
"C is Sea\n"
```
```

is an example of an escape sequence. It is used to print the new line character. If the program is executed, the \n does not appear in the output. Each \n in the string argument of a printf() causes the cursor to be placed at the beginning of the next line of output. Think of an escape sequence as a ‘substitute character’ for outputting special characters or some positional action on the printing point, known as cursor, when the output device is a visual display unit.

All escape sequences available in C are given in Table 8.1. Placing any of these within a string causes either the indicated action or the related character to be output.

```
```
return 0;
```
```

This statement indicates that the value returned by the function main(), after the program instructions in its body are executed, to the operating system is 0. Though the value, recognized by the OS as status, is returned using the return 0 statement, the OS may not always use it.

The return statement is not mandatory; if it is missing, the program will still terminate. In C89, the value returned to the operating system is undefined. In C99, if main() is declared to return an int, the program returns 0 (zero) to the operating

system or operating environment; otherwise the program returns an unspecified value.

Throughout this book, at the end of every function definition for main(), the return 0 instruction must be written. Function definition means the sequence of instructions that form the body of the function which performs the desired task. Similarly, main() should always be written as int main(void) in every program given in this book.

The above discussion is summarized in Fig. 8.3.

**Table 8.1 Backslash codes**

| Code | Meaning |
|---|---|
| `\a` | Ring terminal bell (a is for alert) [ANSI extension] |
| `\?` | Question mark [ANSI extension] |
| `\b` | Backspace |
| `\r` | Carriage return |
| `\f` | Form feed |
| `\t` | Horizontal tab |
| `\v` | Vertical tab |
| `\0` | ASCII null character |
| `\\` | Backslash |
| `\"` | Double quote |
| `\'` | Single quote |
| `\n` | New line |
| `\o` | Octal constant |
| `\x` | Hexadecimal constant |

+   **Note**
+   
+   - C uses a semicolon as a statement terminator; the semicolon is required as a signal to the compiler to indicate that a statement is complete.
+   - All program instructions, which are also called statements, have to be written in lower-case characters.

# ## 8.5 PARTS OF C PROGRAM REVISITED

# ### Header files

A header file is a file containing C declarations and macro definitions to be shared among the source files, compiler, preprocessor, C library, and other header files.

In C, the usual convention is to give header files names that end with .h. Functions in the ANSI C library are declared in a set of standard headers. This set is self-consistent and is free of name space pollution, when compiling in the pure ANSI mode. The ISO C standard library consists of 24 header files which can be included into a programmer’s project with a single directive. Each header file contains one or more function declarations, data type definitions, and macros. Later revisions of the C standard have added several new required header files to the library: