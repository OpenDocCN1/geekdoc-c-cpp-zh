# Using Command-Line Arguments

31:
32: printf("Program %s: (%d) Error opening file ", __FILE__, __LINE__);
n33:

If these lines were part of a program called myprog.c, they would print
Program myprog.c: (32) Error opening file

This might not seem important at this point, but as your programs grow and spread
across multiple source files, finding errors becomes more difficult. Using __LINE__ and
__FILE__ makes debugging much easier.

| DO | DON'T |
|---|---|
| DO use __LINE__ and __FILE__ macros to make your error messages more helpful. | DON'T forget the #endif when using the #if statement. |
| DO put parentheses around the value to be passed to a macro. This prevents errors. For example, use this: | |
#define CUBE(x) (x)*(x)*(x) | |
instead of this: | |
#define CUBE(x) x*x*x |

Your C program can access arguments passed to the program on the command line. This
refers to information entered after the program name when you start the program. If you
start a program progname from the C:> prompt, for example, you could enter
C:>progname jones

The two command-line arguments smith and jones can be retrieved by the program\during execution. You can think of this as information passed to the program's
main() function. Such command-line arguments permit information to be passed to
tprogram startup rather than execution, which can be convenient at times.
You can pass as many command-line arguments as you like. Note that command-line
arguments can be retrieved only within main(). To do so, declare main() as follows:

```
main(int argc, char *argv[])
{
    /* Statements go here */
}
```