# ### 4.4.1 Program Comments

Like every language, C supports comments in the source code. Comments help in making program maintenance easier, so a sensible programmer provides them at key points in a program. They are enclosed by the character sequence `/*` on the left and `*/` on the right. Comments can be single- or multi-line and they can also be placed after program statements. This program shows all of these instances.

Comments in no way affect the size or efficiency of the executable because they are removed by the compiler. While excessive use of comments is discouraged, complex logic must be properly documented in the program itself. Judicious use of comments will help you understand your own program when you look at it months or even years later.

# ### 4.4.2 Preprocessor Section

The preprocessor section that follows the initial comment lines contains two lines that begin with a `#` but don't end with a semicolon. They are not C statements because all C statements are terminated with a semicolon. (For confirmation, look at the lines that follow.) These lines, called *preprocessor directives*, generally appear before the occurrence of the word **main**. When the program is compiled, the preprocessor acts on these lines before the compiler sees them.

The first directive (`#include <stdio.h>`) tells the preprocessor to replace the line with the contents of the file `stdio.h`. This *header file*, which contains information required by the `printf` function, is shipped with every C distribution.

The next directive (`#define PI 3.142`) instructs the preprocessor to globally replace all occurrences of PI in the program with 3.142. The compiler thus doesn't see PI but only 3.142. Unlike radius and area which are variables, **PI** is a *symbolic constant*. It occurs once in the body—in the expression that calculates the area of a circle. We will have to understand why PI was not declared as a variable.

> > **Note:** Preprocessor directives don't end with a semicolon because technically they are not C statements. In fact, the compiler, which acts after the preprocessor has completed its job, doesn't see any comment lines, `#define` or `#include` directives.

# ### 4.4.3 Variables and Computation

The preprocessor section is followed by the program body, which begins with the word **main**. The body represents the meat of a C program where all work is actually done—assigning variables, making decisions, running loops and invoking function calls. The body contains *statements* that end with a semicolon. Here, it begins with two variable declarations:

```
```c
int radius = 5;          /* Integer type */
float area;              /* Floating point type */
```
```

C is a *typed* language, which means all data have types assigned to them. The first statement declares a variable named `radius` having the type `int` (integer). The assignment symbol, `=`, is an *operator* which assigns the value 5 to `radius`. The next statement declares another variable named