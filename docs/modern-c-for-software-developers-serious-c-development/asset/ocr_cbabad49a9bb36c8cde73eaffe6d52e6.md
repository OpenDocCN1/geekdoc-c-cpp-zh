```
#include <stdio.h>

#define ABS(a) (a)<0 ? -(a) : (a)

int main(void) {
    printf("abs of -1 and 1: %d %d", -1, ABS(1));
    return 0;
}
```

When this program is compiled, a in the macro definition will be substituted with the values -1 and 1. The parentheses enclose ensures proper substitution in all cases.

The use of function macros is strongly discouraged since it can produce strange results.
Look at the following program fragment:

```
// call f with the maximum of a and b
#define CALL_WITH_MAX(a, b) f((a) > (b) : (b))

int a = 5, b = 0;
CALL_WITH_MAX(++a, b);      // a is incremented twice
CALL_WITH_MAX(++a, b+10);   // a is incremented once
```

The number of times that a is incremented before calling f depends on what it is being compared.

The use of a function-like macro in real functions has one major benefit: It increases the execution speed of the code because there is no function call overhead. However, if the size of the function-like macro is very large, then this increased speed may be paid for with an increase in the size of the program because of duplicate code.

# The NULL Macro

In the C language, NULL is defined as follows: