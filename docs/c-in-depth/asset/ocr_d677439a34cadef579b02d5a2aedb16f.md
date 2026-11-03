```
```c
#error Timer not available for Windows
#endif
```
```

Suppose a program has been written using ANSI C standard, then this line can be inserted at the beginning of the code.

```
```c
#ifndef __STDC__
#error This program should be run using ANSI C
#endif
```
```

Suppose there are two files and both of them can't be included at a time, then we can use #error directive to stop inclusion of both files at a time. For example suppose the files stdarg.h and varargs.h can't be included at a time, then we can insert #error directive inside the files like this-

```
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
```

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
```

# 12.15 Null Directive

A preprocessor directive consisting only of the symbol # is known as the null directive and it has effect.

# 12.16 #pragma

This is an implementation defined directive that allows various instructions to be given to the comp

Syntax:

```
```c
#pragma name
```
```

Here name is the name of the pragma we want. The pragmas may be different for different compi You should check your compiler's manual for the pragmas available and their details. Any unrecogn pragma directive is just ignored, without showing any error or warning. Some #pragma statements avai in Turbo C are as-

# #pragma startup

It allows the programmer to specify the function that should be called upon program startup i.e. b