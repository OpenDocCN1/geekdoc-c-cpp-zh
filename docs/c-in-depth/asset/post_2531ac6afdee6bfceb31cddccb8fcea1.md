
Similarly if we have some code in the program that is different for different machines, we can use the above structure.

## 12.11.6 Debugging

The compiler can detect syntax errors but it is unable to detect run time errors, which result in incorrect output. To trace these types of errors in the program the debugging has to be done by the programmer. In a large program where many functions and variables are involved this can be a difficult task. For this debugging purpose we can insert some printf statements inside the code that tell us about the intermediate results. After the debugging is complete we don't need these statements and we can delete them. But suppose after few days we again need to debug the program, then we'll have to insert all those statements once again. We have another better alternative if we use preprocessor directives. Using these directives we can make these debugging statements active or inactive depending on our needs. The following program shows this-

```c
#include<stdio.h>
#define DEBUG
main()
{
    int x;
    #ifdef DEBUG
        printf("Starting main()\n");
    #endif
    ............
    func();
    ............
    #ifdef DEBUG
        printf("Now value of x = %d and y = %d \n",x,y);
    #endif
    ........
}
func(){
    #ifdef DEBUG
        printf("Inside func()\n");
    #endif
    ..........
}
```

When the debugging is complete we can just undefine or delete the macro DEBUG. This will make the #ifdef condition false and all the debugging statements will not be compiled. So in this way we can switch between the debugging and normal mode by defining or deleting the macro DEBUG without having to delete all the debugging statements.

Including #ifdef and #endif for every debugging statement makes things look more lengthy and confusing. To make it more concise we can define another macro SHOW. The macro SHOW is defined in such a way that if macro DEBUG is defined, then SHOW will be replaced by a printf statement, and if DEBUG is not defined then SHOW won't be replaced by anything.

```c
#include<stdio.h>
#define DEBUG
#ifdef DEBUG
#define SHOW(message)    printf message
#else
    #define SHOW(message)
#endif
main()
{
    int x, y;
    SHOW("*Starting main()\n");
    func();
    SHOW("*Now value of x = %d and y = %d \n",x,y);
}
func()
{
    SHOW("*Inside func()\n");
}
```

Here the argument message sent to the macro SHOW consists of the control string and all arguments which we want to send to printf(), and these are to be enclosed in parentheses. This is why we have used two pairs of parentheses while calling SHOW.

## 12.11.7 Commenting A Part Of Code

Suppose while testing or for some other reason, we want to comment some part of our source code that contains many comments. This can't be done using our usual technique (/*.... */) since comments can't be nested in C. So here we can use our conditional compilation directives to comment out parts of our source code

```c
#include<stdio.h>
#define COMMENT
main()
{
    .........
    .........
    #ifndef COMMENT
        statement...     /* ...comment ....*/
        statement...     /* ...comment.....*/      Code to be commented
    #endif
    .......
    .......
}
```

If the macro COMMENT is defined, then the code will be commented (not compiled) and if this macro is not defined then it will be treated as usual code and will be compiled.

## 12.11.8 Other Uses of conditional compilation

If you open any header file, you will see that whole contents of the file are enclosed inside #ifndef ... #endif directives. For example if we open stdio.h file

```c
#ifndef __STDIO_H
#define __STDIO_H
....contents of stdio.h file.....
#endif
```

This sort of coding ensures that the contents of this file will be included only once. The first time when the file stdio.h is included, the preprocessor finds that macro __STDIO_H is not defined, and hence it defines this macro and includes the contents of the file. After this whenever stdio.h is included in our program, the preprocessor finds that the macro __STDIO_H is defined and hence it skips all the statements between #ifndef and #endif.

We can use a similar strategy to avoid multiple definitions in our program. For example the definition of constant NULL may be needed by many files such as stdio.h, stdlib.h, string.h, alloc.h etc. This constant can be defined in all these files but if we include more than one files which have definition of NULL, then our program will have multiple definitions of NULL. So definition of NULL is put in a separate file _null.h and this file is included in all other files.

These files don't include the _null.h file directly, but enclose the include directive inside #ifndef and #endif like this-

```c
#ifndef NULL
#include<_null.h>
#endif
```

Now this file will be included only when NULL has not been defined.

## 12.12 Predefined Macro Names

There are certain predefined macro names which can't be undefined or redefined by #undef or #define.

| Macro | Description |
|---|---|
| __DATE__ | String constant that represents the date of compilation in the format "mm dd yyyy" |
| __TIME__ | String constant that represents the time of compilation in the format "hh:mm:ss" |
| __FILE__ | String constant that represents the name of the file being compiled. |
| __LINE__ | Decimal constant that represents the line number being compiled. |
| __STDC__ | Decimal constant, which is 1 if compiled with ANSI standard |

```c
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

The macros __FILE__ and __LINE__ can be used to write error messages in the program, that can indicate the line number and file name where the error occurred.

## 12.13 #line

This directive is used for debugging purposes.

Syntax:

```c
#line dec_const string_const
```

Here dec_const is any decimal constant and string_const is any string constant. This directive assigns dec_const and string_const to the macros __LINE__ and __FILE__ respectively. If the string_const is not specified then the macro __FILE__ remains unchanged.

```c
/* P12.21 Program to understand the use of #line, name of this file is prog.c */
#include<stdio.h>
main()
{
    printf("C in depth\n");
    printf("%d %s\n",__LINE__,__FILE__);
    #line 25 "myprog.c"
    printf("%d %s\n",__LINE__,__FILE__);
}
```

Output:

C in depth
6 C:\prog.c
25 myprog.c

## 12.14 #error

This preprocessor directive is used for debugging purpose. #error directive stops compilation and displays a fatal error message attached with it.

Syntax:

```c
#error message
```

```c
#error Timer not available for Windows
#endif
```

Suppose a program has been written using ANSI C standard, then this line can be inserted at the beginning of the code.

```c
#ifndef __STDC__
#error This program should be run using ANSI C
#endif
```

Suppose there are two files and both of them can't be included at a time, then we can use #error directive to stop inclusion of both files at a time. For example suppose the files stdarg.h and varargs.h can't be included at a time, then we can insert #error directive inside the files like this-

```c
/*Structure of file stdarg.h*/
#ifndef __STDARG_H
#define __STDARG_H

#ifdef __VARARGS_H
#error Can't include both stdarg.h and varargs.h
#endif
...contents of file.......
#endif
```

```c
/*Structure of file varargs.h*/
#ifndef __VARARGS_H
#define __VARARGS_H

#ifdef __STDARG_H
#error Can't include both stdarg.h and varargs.h
#endif
...contents of file.......
#endif
```

## 12.15 Null Directive

A preprocessor directive consisting only of the symbol # is known as the null directive and it has no effect.

## 12.16 #pragma

This is an implementation defined directive that allows various instructions to be given to the compiler

Syntax:

```c
#pragma name
```

Here name is the name of the pragma we want. The pragmas may be different for different compiler. You should check your compiler's manual for the pragmas available and their details. Any unrecognized pragma directive is just ignored, without showing any error or warning. Some #pragma statements available in Turbo C are as-

# #pragma startup

It allows the programmer to specify the function that should be called upon program startup i.e. before main
