# 13.5.3 Conditionally Compiling Debugging Code

Conditional compilation is sometimes used as a debugging aid. Debuggers provide much more powerful features than conditional compilation, but if a debugger is not available, printf statements can be used to print variable values and to confirm the flow of control. These printf statements can be enclosed in conditional preprocessor directives so the statements are compiled only while the debugging process is not completed. For example,

```
```c
#ifdef DEBUG
    printf("Variable x = %d\n", x);
#endif
```
```

compiles the printf statement if the symbolic constant DEBUG is defined (#define DEBUG) before the #ifdef DEBUG. When debugging is completed, you remove or comment out the #define directive from the source file and the printf statements inserted for debugging purposes are ignored during compilation. In larger programs, it may be desirable to define several symbolic constants that control the conditional compilation in separate sections of the source file. Many compilers allow you to define and undefine symbolic constants like DEBUG with a compiler flag that you supply each time you compile the code so that you do not need to change the code.

# Error-Prevention Tip 13.3

> When inserting conditionally compiled printf statements in locations where C expects a single statement (e.g., the body of a control statement), ensure that the conditionally compiled statements are enclosed in blocks.

# 13.6 #error and #pragma Preprocessor Directives

The #error directive

```
```c
#error tokens
```
```

prints an implementation-dependent message including the tokens specified in the directive. The tokens are sequences of characters separated by spaces. For example,

```
```c
#error 1 - Out of range error
```
```

contains 6 tokens. When a #error directive is processed on some systems, the tokens in the directive are displayed as an error message, preprocessing stops and the program does not compile.

The #pragma directive

```
```c
#pragma tokens
```
```

causes an implementation-defined action. A pragma not recognized by the implementation is ignored. For more information on #error and #pragma, see the documentation for your C implementation.

# 13.7 # and ## Operators

The # operator causes a replacement-text token to be converted to a string surrounded by quotes. Consider the following macro definition:

```
```c
#define HELLO(x) puts("Hello, " #x);
```
```