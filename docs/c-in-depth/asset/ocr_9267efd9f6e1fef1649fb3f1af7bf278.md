.. #endif directives. For example if we open stdio.h file

```
#ifndef __STDIO_H
#define __STDIO_H
....contents of stdio.h file.....
#endif
```

This sort of coding ensures that the contents of this file will be included only once. The first time when the file stdio.h is included, the preprocessor finds that macro __STDIO_H is not defined, and hence it defines this macro and includes the contents of the file. After this whenever stdio.h is included in our program, the preprocessor finds that the macro __STDIO_H is defined and hence it skips all the statements between #ifndef and #endif.

We can use a similar strategy to avoid multiple definitions in our program. For example the definition of constant NULL may be needed by many files such as stdio.h, stdlib.h, string.h, alloc.h etc. This constant can be defined in all these files but if we include more than one files which have definition of NULL, then our program will have multiple definitions of NULL. So definition of NULL is put in a separate file _null.h and this file is included in all other files.

These files don't include the _null.h file directly, but enclose the include directive inside #ifndef and #endif like this-

```
#ifndef NULL
#include<_null.h>
#endif
```

Now this file will be included only when NULL has not been defined.

# 12.12 Predefined Macro Names

There are certain predefined macro names which can't be undefined or redefined by #undef or #define.

| Macro | Description |
|---|---|
| __DATE__ | String constant that represents the date of compilation in the format "mm dd yyyy" |
| __TIME__ | String constant that represents the time of compilation in the format "hh:mm:ss" |
| __FILE__ | String constant that represents the name of the file being compiled. |
| __LINE__ | Decimal constant that represents the line number being compiled. |
| __STDC__ | Decimal constant, which is 1 if compiled with ANSI standard |

```
/*P12.20 Program to display the values of predefined constants*/
#include<stdio.h>
main( )
{
    printf("%s\n", __DATE__);
    printf("%s\n", __TIME__);
    printf("%s\n", __FILE__);
    printf("%d\n", __LINE__);
}
```

Output:
Sep 24 2003
10:24:42