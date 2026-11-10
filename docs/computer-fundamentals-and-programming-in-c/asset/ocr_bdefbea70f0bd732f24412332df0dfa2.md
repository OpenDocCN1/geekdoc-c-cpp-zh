```
```c
#else
#define INT_SIZE 32
#endif
```
```

Another example of the use of `#ifdef` is given as follows.

# EXAMPLE

```
```c
18. #include <stdio.h>
#define VAX 1
#define SUN 0
int main()
{
    #ifdef VAX
        printf("This is a VAX\n");
    #endif
    #ifdef SUN
        printf("This is a SUN\n");
    #endif
    return 0;
}
```
```

```
```text
Output
    This is a VAX
```
```

+   **Note**
+   
+   - C89 states that `#ifs` and `#elif`s may be nested at least eight levels. C99 states that at least 63 levels of nesting be allowed.

The logical operators such as `&&` or `||` can be used to test if multiple identifiers have been defined.

# #error

The directive `#error` is used for reporting errors by the preprocessor. The general form is

```
```c
#error error_message
```
```

When the preprocessor encounters this, it outputs the `error_message` and causes the compilation to be aborted. Therefore, it should be only used for reporting errors that make further compilation pointless or impossible. It is used primarily for debugging. For example,

```
```c
#ifdef LINUX
#error This software requires the LINUX OS.
#endif
```
```

Another example of the use of `#error` is as follows:

```
```c
#if A_SIZE < B_SIZE
#error "Incompatible sizes"
#endif
```
```

Here, the `#error` macro is used to enforce the consistency of two symbolic constants.

# #line

The `#line` directive is used to change the value of the `__LINE__` and `__FILE__` variables. The filename is optional. The `__FILE__` and `__LINE__` variables represent the current file and the line that is being read. The general form of this directive is

```
```c
#line line_number <file_name>
```
```

```
```c
#line 20 "program1.c"
```
```

changes the current line number to 20, and the current file to `program1.c`.

# #pragma

The `#pragma` directive allows the programmer the ability to convey to the compiler to do certain tasks. Since the `#pragma` directive is implementation-specific, uses vary from compiler to compiler. One option might be to trace program execution. Three forms of this directive (commonly known as pragmas) are specified by the 1999 C standard. A C compiler is free to attach any meaning it likes to other pragmas.

# 16.4.2 Predefined Macros

The preprocessor furnishes a small set of predefined macros that denote useful information. The standard macros are summarized in Table 16.4. Most implementations augment this list with many non-standard predefined identifiers.

Table 16.4 Standard predefined identifiers

| Identifier | Denotes |
|---|---|
| `__FILE__` | Name of the file being processed |
| `__LINE__` | Current line number of the file being processed |
| `__DATE__` | Current date as a string (e.g., “16 Dec 2005”) |
| `__TIME__` | Current time as a string (e.g., “10:15:30”) |

The predefined macros, also known as macros, can be used in programs just like program constants. All predefined macros have two underscore characters more at the beginning and the other at the end. A demonstration of predefined identifiers is illustrated below:

```
```c
#include <stdio.h>
int main()
{
    printf("__DATE__ == %s\n", __DATE__);
    printf("__FILE__ == %s\n", __FILE__);
    printf("__LINE__ == %d\n", __LINE__);
    printf("__TIME__ == %s\n", __TIME__);
    printf("__STDC__ == %d\n", __STDC__);
    return 0;
}
```
```

```
```text
Output
__DATE__ == Dec 18 2010
__FILE__ == pred.c
```
```