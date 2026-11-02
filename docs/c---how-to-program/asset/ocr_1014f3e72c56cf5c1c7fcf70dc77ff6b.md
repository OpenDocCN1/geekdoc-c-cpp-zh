| Header | Explanation |
|---|---|
| `<math.h>` | Contains function prototypes for math library functions. |
| `<setjmp.h>` | Contains function prototypes for functions that allow bypassing the usual function call and return sequence. |
| `<signal.h>` | Contains function prototypes and macros to handle various conditions that may arise during program execution. |
| `<stdarg.h>` | Defines macros for dealing with a list of arguments to a function whose number and types are unknown. |
| `<stddef.h>` | Contains common type definitions used by C for performing calculations. |
| `<stdio.h>` | Contains function prototypes for the standard input/output library functions, and information used by them. |
| `<stdlib.h>` | Contains function prototypes for conversions of numbers to text and text to numbers, memory allocation, random numbers and other utility functions. |
| `<string.h>` | Contains function prototypes for string-processing functions. |
| `<time.h>` | Contains function prototypes and types for manipulating the time and date. |

**Fig. 5.10** | Some of the standard library headers. (Part 2 of 2.)

You can create custom headers. Programmer-defined headers should also use the `.h` filename extension. A programmer-defined header can be included by using the `#include` preprocessor directive. For example, if the prototype for our square function was located in the header `square.h`, we'd include that header in our program by using the following directive at the top of the program:

```
#include "square.h"
```

Section 13.2 presents additional information on including headers, such as why programmer-defined headers are enclosed in quotes (`" "`) rather than angle brackets (`<>`).

# 5.9 Passing Arguments By Value and By Reference

In many programming languages, there are two ways to pass arguments—pass-by-value and pass-by-reference. When arguments are *passed by value*, a copy of the argument’s value is made and passed to the called function. Changes to the copy do not affect an original variable’s value in the caller. When an argument is *passed by reference*, the caller allows the called function to *modify* the original variable’s value.

Pass-by-value should be used whenever the called function does not need to modify the value of the caller’s original variable. This prevents the accidental side effects (variable modifications) that so greatly hinder the development of correct and reliable software systems. Pass-by-reference should be used only with *trusted* called functions that need to modify the original variable.

In C, all arguments are passed by value. As we’ll see in Chapter 7, C Pointers, it’s possible to achieve pass-by-reference by using the *address operator* and the *indirection operator*. In Chapter 6, we’ll see that array arguments are automatically passed by reference for performance reasons. We’ll see in Chapter 7 that this is *not* a contradiction. For now, we concentrate on pass-by-value.