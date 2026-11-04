
For example, if the user enters 2 and 5, the program displays:

i+j = 7
i*j+i*j = 20

The ## operator is used to merge identifiers together. It is not allowed to appear in the beginning or at the end of the sequence. If the identifier is a macro parameter, the preprocessor first replaces it with the value of the argument and then pasting occurs. For example:

```
#include <stdio.h>

#define f(a) s##u##m##a

int sum1(int a, int b);

int main(void)
{
    int i, j;

    printf("Enter numbers: ");
    scanf("%d%d", &i, &j);
    printf("%d\n", f(1)(i, j));
    return 0;
}

int sum1(int a, int b)
{
    return a+b;
}
```

When the preprocessor expands the f macro, because the character a has the same name as the argument, the preprocessor replaces a with the value of the argument, that is, 1, and then merges that value with the s, u, and m characters. Therefore, f(1)(i, j) is expanded to sum1(i, j) and the program calls sum1() to display the sum of the two input numbers.

## Preprocessor Directives and Conditional Compilation

This section discusses the preprocessor directives that allow the conditional compilation of a part of the program. The conditional compilation can be very useful in many situations, for example, to debug the program, to monitor the program execution, or to maintain multiple versions of the same program.

### The #if, #else, #elif, and #endif Directives

The #if and #endif directives are used to define which parts of a program will be compiled, depending on the value of an expression. The general syntax is:

```
#if expression
... /* block of statements */
#endif
```

The expression is a constant integer expression which is not allowed to include sizeof, casts or enum constants. If its value is true, the preprocessor keeps the block of statements to be compiled. If not, the block will be removed and the compiler won't see it. Notice that if the expression is an undefined identifier, the #if directive evaluates to false. For example:

```
#if NUM
```

If NUM is not defined the outcome is false, while the value of #if !NUM is true. If NUM is defined with value 0, #if NUM evaluates to false and #if !NUM to true.

The #else directive is used in conjunction with the #if directive to define a block of statements that will be compiled if the value of the expression is false.

```
#if expression
... /* block of statements A */
#else
... /* block of statements B */
#endif
```

For example, in the following program, the #else part will be compiled because NUM is greater than 0:

```
#include <stdio.h>

#define NUM 10

int main(void)
{
    #if NUM < 0
        printf("Seg_1\n");
    #else
        printf("Seg_2\n");
    #endif
    return 0;
}
```

Therefore, the program displays Seg_2. Notice that if the definition of NUM was missing, the program would display Seg_2, too.

Since nested comments are not allowed, it is not possible to put in comments a part of the program that contains comments. Instead, we can use the #if directive. For example:

```
#if 0
    /* Comment. */
    ...    /* Code. */
    /* Another comment. */
#endif
```

The #elif directive can be used together with #if, #ifdef, and #ifndef directives to define multiple compilation paths. For example:

```c
#if expression_A
    ... /* block of statements A */
#elif expression_B
    ... /* block of statements B */
.
.
#else
    ... /* block of statements N */
#endif
```

The second block of statements will be compiled only if the value of expression_A is false and the value of expression_B is true. Once an #if or #elif expression is found true, next #elif and #else directives are discarded. The last #else is optional and its block of statements will be compiled only if the previous expressions are all false. In practice, we've often used this syntax to support multiple versions of the same program. For example:

```c
#include <stdio.h>

#define VER_2 1

int main(void)
{
    int cnt = 0;

    #if VER_1
        cnt = 1;
        printf("Version_1\n");
    #elif VER_2
        cnt = 2;
        printf("Version_2\n");
    #else
        cnt = 3;
        printf("Version_3\n");
    #endif

    printf("Cnt = %d\n", cnt);
    return 0;
}
```

Since VER_1 is not defined and the value of VER_2 is true, the preprocessor keeps those lines and discards the rest, cnt becomes 2 and the program displays:

```text
Version_2
Cnt = 2
```

If we change the value of VER_2 to 0, the #elif expression becomes false and the preprocessor keeps the lines of the #else directive. Therefore, the program displays:

```
Version_3
Cnt = 3
```

If the #else directive was missing, the program would display: Cnt = 0

### The #ifdef, #ifndef, and #undef Directives

The #ifdef directive is used to check if an identifier is defined as a macro. The general syntax is:

```
#ifdef name
... /* block of statements */
#endif
```

The difference with the #if directive is that the #ifdef directive only checks if the identifier is defined as a macro; it does not evaluate its value. For example:

```
#include <stdio.h>

#define VER_1 0

int main(void)
{
    #ifdef VER_1
        printf("Version_1\n");
    #else
        printf("Version_2\n");
    #endif
    return 0;
}
```

Since VER_1 is defined, the program displays Version_1.

The #ifndef directive is used to check whether an identifier is not defined as a macro. A typical use of the #ifndef directive is to prevent multiple inclusions of the same file. It is not only to avoid unnecessary recompilations and save some time, but also for another reason. Suppose that a program consists of several source files and some of them include the same file (e.g., test.h). If test.h contains type definitions (e.g., structures), the compilation will fail because redefinition of the same types is not allowed. To avoid that, we add the following lines at its beginning:

```
#ifndef SOME_TAG /* Use a name not defined somewhere else. */
#define SOME_TAG
/* Contents of test.h */
#endif
```

Once the first file that includes test.h is compiled, the preprocessor will include the contents of the test.h because the SOME_TAG macro is not defined yet. In next inclusions of test.h, the preprocessor skips its content because SOME_TAG has been defined and #ifdef evaluates to false. The common practice is to select a name for the SOME_TAG similar to the name of the header file.

Furthermore, the use of #ifndef prevents endless inclusions. For example, this might happen if one file (e.g., one.h) includes a second one (e.g., sec.h) and that second one includes the first.

The #undef directive cancels the definition of a macro. If the macro has not been defined, #undef has no effect. For example:

```c
#include <stdio.h>

#define NUM 100

int main(void)
{
    int arr[NUM];
#undef NUM

    printf("Array contains %d elements\n", NUM);
    return 0;
}
```

Since the directive #undef NUM cancels the definition of NUM, the compiler will produce an error message in printf().

### The defined Operator

An alternative way to check if an identifier is defined as a macro is to use the defined operator. The defined operator is usually used together with the #if or #elif directives. For example:

```c
#if defined(VER_1) /* Equivalent to #ifdef VER_1 */
...
#endif
```

The parentheses are not necessary; it is a matter of preference. Similarly, the expression #if !defined(VER_1) is equivalent to #ifndef VER_1. The advantage over the #ifdef and #ifndef is that these can be used to check if only one macro is defined or not, while the defined operator and the #if directive can be used to check multiple macros. See how we are using the && operator to check multiple conditions:

```c
#if defined(VER_1) && !defined(VER_2) && defined(VER_3)
...
#endif
```

or use the || operator to check if a macro is defined:

```c
#if defined(VER_1) || defined(VER_2)
...
#endif
```

Here is another common application of the conditional compilation. Suppose that we are writing a program that depends on some external factor, for example, the operating system or the compiler. Instead of writing different versions, we could use conditional compilation. For example:

```c
#if defined(UNIX)
...
#elif defined(LINUX)
...
#elif defined(WINDOWS)
...
#endif
```

At the beginning of the program, the proper macro is defined and the preprocessor keeps the corresponding code.

### Miscellaneous Directives

Before continuing with the exercises, let's discuss briefly the #error, #line, and #pragma directives.

The syntax of the #error directive is #error message and instructs the preprocessor to display an error message that contains the message. The compilation fails. Typically, it is used in the #else part of an #if-#elif-#else series to indicate an undesirable situation. For example:

```c
#if defined(VER_1)
...
#elif defined(VER_2)
...
#else
#error Unspecified version
#endif
```

The #line directive has two forms. The first one is #line n, where n is an integer. It changes the numbering of the next lines in the program to n, n+1, n+2, ... The second form is #line n "file", where the compiler assumes that the lines that follow this directive are coming from file, with line numbering starting from n.

The #pragma directive is used to request special behavior from the compiler. The set of commands that can appear in the #pragma directive is different for each compiler. If the command is not supported, the compiler ignores the directive. For example, if a compiler supports the warning command, the directive #pragma warning(disable: 4244) may be used to disable the appearance of the warning message with code 4244.
