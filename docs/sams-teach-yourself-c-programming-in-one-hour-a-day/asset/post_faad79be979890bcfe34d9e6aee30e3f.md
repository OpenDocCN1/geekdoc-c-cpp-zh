
preceded by # in the substitution string, the argument is converted into a quoted string when the macro is expanded. Thus, if you define a macro as

```
#define OUT(x) printf ("#x")
```

and you invoke it with the statement

```
OUT(Hello Mom);
```

it expands to this statement:

```
printf("Hello Mom\"");
```

The conversion performed by the stringizing operator takes special characters into account. Thus, if a character in the argument normally requires an escape character, the # operator inserts a backslash before the character. Continuing with the example, the invocation

```
OUT("Hello Mom\"");
```

expands to

```
printf("\\Hello Mom\\\"");
```

The # operator is demonstrated in Listing 22.4. First, you need to look at one other operator used in macros, the concatenation operator (##). This operator concatenates and joins two strings in the macro expansion. It doesn't include quotation marks or special treatment of escape characters. Its main use is to create sequences of C source code. For example, if you define and invoke a macro as

```c
#define CONCAT(a, b) a ## b
#define CALL(n) func##n)
```

the macro invoked in the second line is expanded to

```c
salad = func3(q, w);
```

You can see that, by using the ## operator, you determine which function is called. You have actually modified the C source code.

Listing 22.4 shows an example of one way to use the # operator.

## The C Preprocessor

### Input

### LISTING 22.4 macroreplc.c--Demonstrates the # Operator in Macro Expansion

```c
1: // macroreplc.c--Demonstrates the # operator in macro expansion
2:
3: #include <stdio.h>
4:
5: #define OUT(x) printf("#x is equal to %d.\n", x)
6:
7:     int main(void )
8:     {
9:         int value = 123;
10:        OUT(value);
11:        return(0);
12: }
```

**Output**
value is equal to 123.

**Analysis**
By using the # operator on line 5, the call to the macro expands the variable name value as a quoted string to the printf() function. After expansion on line 9, the macro OUT looks like this:

`printf("value" " is equal to %d.", value);`

### Macros Versus Functions

You have seen that function macros can be used in place of real functions, at least in situations where the resulting code is relatively short. Function macros can extend beyond one line, but they usually become impractical beyond a few lines. When you can use either function or a macro, which should you use? It's a trade-off between program speed and program size.

A macro's definition is expanded into the code each time the macro is encountered in the source code. If your program invokes a macro 100 times, copies of the expanded macro code are in the final program. In contrast, a function's code exists only as a single copy. In terms of program size, the best choice is a true function.

When a program calls a function, a certain amount of processing overhead is required to pass execution to the function code and return execution to the calling program. There is no processing overhead in “calling” a macro because the code is right there in the program. In terms of speed, a function macro has the advantage.

The few size/speed considerations aren’t usually of much concern to the beginning programmer. Only with large, time-critical applications do they become important.

| DO | DON'T |
|---|---|
| use #defines, especially for symbolic constants. Symbolic constants make your code much easier to read. Examples of things to put into defined constants are true, false, yes/no, the keyboard keys, and maximum values. Symbolic constants are used throughout this book. | over-use macro functions. Use them where needed, but be sure that they are a better choice than a normal function. |

## Using the #include Directive

You have already learned how to use the #include preprocessor directive to include header files in your program. When it encounters an #include directive, the preprocessor reads the file and inserts it at the location of the directive. You can't use the * or wildcards in a group of files with one #include directive. You can, however, nest #include directives. In other words, an included file can contain #include directives, which can contain #include directives and so on. Compilers limit the number of levels deep that you can nest, but if the compiler supports the ANSI Standard, then you already learned how to use the #include preprocessor directive to include header files that can nest up to 15 levels.

There are two ways to specify the filename for an #include directive. If the filename is enclosed in angle brackets, as <stdio.h> (as you have seen throughout this book), the preprocessor first looks for the file in the standard directory. If the file isn't found, or no standard directory is specified, the preprocessor looks for the file in the current directory.

The second method of specifying the file to be included is enclosing the filename in double quotation marks: #include "myfile.h". In this case, the preprocessor doesn't search the standard directory; instead, it looks in the directory containing the sourcecode file being compiled. Generally speaking, header files that you should be kept in the same directory as the C source-code files, they are included by using double quotation marks. The standard directory is reserved for header files supplied with your compiler.

## Using #if, #elif, #else, and #endif

These #if, #elif, #else, and #endif directives are used for conditional compilation. The #if, #elif, #else, and #endif directives allow you to control which parts of the code are compiled based on certain conditions.

By using #if, #elif, #else, and #endif, you can control compilation based on previous definitions, without regard to the specific value of a name. The structure of an #if block is:

```c
#if condition_1
    statement_1
#elif condition_2
    statement_2
...
#elif condition_n
    statement_n
#else
    default_statement
#endif
```

The #if, #elif, #else, and #endif directives are useful when you use conditional compilation directives. This operator tests to see whether a particular name is defined. Then, the expression defined( NAME ) evaluates to TRUE or FALSE depending on whether NAME is defined. By using defined(), you can control compilation, based on previous definitions, without regard to the specific value of a name. Referring to the previous debugging code example, you could rewrite the #if...#endif section as follows:

```c
#if defined( DEBUG )
debugging code here
#endif
```

You can also use defined() to assign a definition to a name only if it hasn’t been previously used. Using the NOT operator (! ) as follows:

```c
#if !defined( TRUE )   /* if TRUE is not defined. */
#define TRUE 1
#endif
```

The possible uses of these conditional directives are limited only by your imagination. Here's one example: Suppose you're writing a program that uses a great deal of country-specific information. This information is contained in a header file for each country. When you compile the program for different countries, you can use an #if...#endif construction as:

```c
#if ENGLAND == 1
#include "england.h"
#elif FRANCE == 1
#include "france.h"
#elif ITALY == 1
#include "italy.h"
#else
#include "usa.h"
#endif
```

Then, by using #define to define the appropriate symbolic constant, you can control which header is included during compilation.

### Using #if...#endif to Help Debug

Another common of #if...#endif is to include conditional debugging code in the program. You could define a DEBUG symbolic constant set to either 1 or 0. Throughout the program, you can insert debugging code as follows:

```c
#if DEBUG == 1
debugging code here
#endif
```

During program development, if you define DEBUG as 1, the debugging code is included to help track any bugs. After the program works properly, you can redefine DEBUG as 0 and recompile the program without the debugging code.

The defined() operator is useful when you use conditional compilation directives. This operator tests to see whether a particular name is defined. Then, the expression

defined( NAME ) evaluates to TRUE or FALSE depending on whether NAME is defined. By using defined(), you can control compilation, based on previous definitions, without regard to the specific value of a name. Referring to the previous debugging code example, you could rewrite the #if...#endif section as follows:

```c
#if defined( DEBUG )
debugging code here
#endif
```
