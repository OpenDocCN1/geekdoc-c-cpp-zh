# Introduction

The stdarg.h header defines a variable type **va_list** and three macros which can be used to get the arguments in a function when the number of arguments are not known i.e. variable number of arguments.

A function of variable arguments is defined with the ellipsis (...) at the end of the parameter list.

# Library Variables

Following is the variable type defined in the header stdarg.h:

| S.N. | Variable & Description |
|------|------------------------|
| 1 | **va_list**
This is a type suitable for holding information needed by the three macros **va_start()**, **va_arg()** and **va_end()**. |

# Library Macros

Following are the macros defined in the header stdarg.h:

| S.N. | Macro & Description |
|------|---------------------|
| 1 | `void va_start(va_list ap, last_arg)`
This macro initializes **ap** variable to be used with the **va_arg** and **va_end** macros. The **last_arg** is the last known fixed argument being passed to the function i.e. the argument before the ellipsis. |
| 2 | `type va_arg(va_list ap, type)`
This macro retrieves the next argument in the parameter list of the function with type **type**. |
| 3 | `void va_end(va_list ap)`
This macro allows a function with variable arguments which used |