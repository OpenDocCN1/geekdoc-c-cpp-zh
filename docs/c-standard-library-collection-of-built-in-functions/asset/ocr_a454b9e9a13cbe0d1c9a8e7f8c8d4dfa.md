# Introduction

The setjmp.h header defines the macro **setjmp()**, one function **longjmp()**, and one variable type **jmp_buf**, for bypassing the normal function call and return discipline.

# Library Variables

Following is the variable type defined in the header setjmp.h:

| S.N. | Variable & Description |
|------|------------------------|
| 1    | **jmp_buf**<br>This is an array type used for holding information for macro **setjmp()** and function **longjmp()**. |

# Library Macros

There is only one macro defined in this library:

| S.N. | Macro & Description |
|------|---------------------|
| 1    | **int setjmp(jmp_buf environment)**<br>This macro saves the current *environment* into the variable **environment** for later use by the function **longjmp()**. If this macro returns directly from the macro invocation, it returns zero but if it returns from a **longjmp()** function call, then a non-zero value is returned. |

# int setjmp(jmp_buf environment)

# Description

The C library macro **int setjmp(jmp_buf environment)**, saves the current **environment** into the variable environment for later use by the function **longjmp()**. If this macro returns directly from the macro invocation, it