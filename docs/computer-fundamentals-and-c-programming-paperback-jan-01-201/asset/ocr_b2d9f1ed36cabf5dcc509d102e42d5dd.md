```
/* variable_arguments.c: Uses a variable of type va_list and 3 macros. */

#include <stdio.h>
#include <stdarg.h>          /* Defines 3 macros -- va_start, va_args, va_end */
int sum(int argc, ...);      /* ... indicates variable number of arguments */
int main(void) {
    printf("10 + 20 + 40 = %d\n", sum(3, 10, 20, 40));
    printf("1 + 2 + 3 + 5 + 10 = %d\n", sum(5, 1, 2, 3, 5, 10));

    return 0;
}

int sum(int argc, ...)        /* Function definition */
{
    int i, total = 0;

    /* First define a variable arglist of type va_list */
    va_list arglist;
    /* Initialize arglist */
    va_start(arglist, argc);
    /* Retrieve all arguments from arglist */
    for (i = 0; i < argc; i++)
        total += va_arg(arglist, int);

    /* Clean up arglist */
    va_end(arglist);
    return total;
}
```

PROGRAM 17.6: **variable_arguments.c**

```
10 + 20 + 40 = 70
1 + 2 + 3 + 5 + 10 = 21
```

PROGRAM OUTPUT: **variable_arguments.c**

# 17.13 MULTI-SOURCE PROGRAM FILES

The most trivial application uses a single source file. A typical commercial application is spread across multiple .c (source), .h (include) and .o (object) files, along with one or more executables. The standard technique of using `gcc foo.c` or `cl foo.c` doesn’t work in this situation. When code is distributed across multiple files, all .c files must be included for compilation. This is how GCC and Visual Studio compile multi-file programs:

| Command | Description |
|---|---|
| `gcc a.c b.c c.c` | Creates a.out; no .o files |
| `cl a.c b.c c.c` | Creates a.exe and three .obj files |