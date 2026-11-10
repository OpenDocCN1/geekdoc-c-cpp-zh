and

```
~~~c
#include "file_name"
~~~
```

The first form is used for referring to the standard system header files. It searches for a file named `file_name` in a standard header file library and inserts it at the current location. Header files contain details of functions and types used within the library. They must be included before the program can make use of the library functions. The angle brackets, `< >`, indicates the preprocessor to search for the header file in the standard location for library definitions.

The second form searches for a file in the current directory. This is used where multi-file programs are being written. Certain information is required at the beginning of each program file. This code in the `file_name` can be put into the current directory and included in each program file. Local header file names are usually enclosed by double quotes, "". It is conventional to give header files a name that ends in '.h' to distinguish them from other types of files. Examples of both forms of `#include` have been given in earlier chapters.

In addition, each preprocessing directive must be on its own line. For example, the following will not work:

```
~~~c
#include <stdio.h> #include <stdlib.h>
~~~
```

Include files can have `#include` directives in them. This is referred to as nested includes. The number of levels of nesting allowed varies between compilers. However, C89 stipulates that at least eight nested inclusions will be available. C99 specifies that at least 15 levels of nesting be supported.

# ## #if, #else, #elif, and #endif

Here, `#if` is a conditional directive of the preprocessor. It has an expression that evaluates to an integer. The `#else` is also used with this directive if required. The `#if` and `#else` pair operates in a way similar to the if-else construct of C. The `#endif` is used to delimit the end of statement following the statement sequence.

The general form of `#if` with `#endif` and `#else` is

```
~~~c
#if< constant_expression>
    <statement_sequence1>
#endif

or

#if< constant_expression>
    <statement_sequence1>
#else<statement_sequence2>
#endif
~~~
```

As an example, if a program has to run on an MSDOS machine and it is required to include file `MSDOS.h`, otherwise a `default.h` file, then the following code using `#if` can be used.

```
~~~c
#if SYSTEM == MSDOS
    #include <msdos.h>
~~~
```

```
~~~c
#else
    #include "default.h"
#endif
~~~
```

The general form for using `#if` with `#elif`, which is else-if, and `#endif` is

```
~~~c
#if<constant_expression1>
    <statement_sequence1>
#elif<constant_expression2>
    <statement_sequence2>
.
.
#elif<constant_expressionN>
    <statement_sequenceN>
#endif
~~~
```

Sometimes, it may be necessary to choose one of the different header files to be included into a program. For example, preprocessors might specify configuration parameters to be used on different types of operating systems. The programmer can do this using a series of conditional directives as shown in the following illustration.

```
~~~c
#if SYSTEM1
    #include "SYSTEM_1.h"
#elif SYSTEM2
    #include "system_2.h"
#elif SYSTEM3
    ...
#endif
~~~
```

# ## #ifdef and #ifndef

The `#ifdef` directive executes a statement sequence if the `macro_name` is defined. If the `macro_name` is not defined, the `#ifndef` directive executes a statement sequence. For both the directives, the end of statements is delimited by `#endif`. The general form of `#ifdef` is

```
~~~c
#ifdef macro_name
    <statement_sequence>
#endif
~~~
```

and the general form of `#ifndef` is

```
~~~c
#ifndef macro_name
    <statement_sequence>
#endif
~~~
```

These conditional directives are useful for checking if macros are defined or set, perhaps from different header files and program modules. For instance, to set integer size for a portable C program between Turbo C (on MSDOS) and LINUX (or other) operating systems, these directives can be used.

As an example, assume that if Turbo C is running, a macro `TURBOC` will be defined. So, the programmer just needs to check for this. Thus, the following code may be written.

```
~~~c
#ifdef TURBOC
    #define INT_SIZE 16
~~~
```