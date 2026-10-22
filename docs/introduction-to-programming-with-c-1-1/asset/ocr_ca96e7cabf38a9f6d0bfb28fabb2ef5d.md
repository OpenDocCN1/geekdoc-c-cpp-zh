executing program.
used in array.
executing program.
used in linked list.

Now let's have a quick look at the methods used for dynamic memory allocation.

**malloc()** allocates single block of requested memory.
**calloc()** allocates multiple block of requested memory.
**realloc()** reallocates the memory occupied by malloc() or calloc() functions.
**free()** frees the dynamically allocated memory.

For complete tutorial of dynamic memory allocation refer to the link below:

https://www.youtube.com/watch?v=xDVC3wKjS64

# 5.3 C - Preprocessors

The **C Preprocessor** is not a part of the compiler, but is a separate step in the compilation process. In simple terms, a C Preprocessor is just a text substitution tool and it instructs the compiler to do required pre-processing before the actual compilation. We'll refer to the C Preprocessor as CPP.

All preprocessor commands begin with a hash symbol (#). It must be the first nonblank character, and for readability, a preprocessor directive should begin in the first column. The following section lists down all the important preprocessor directives –

**Sr.No.**        **Directive & Description**

1        **#define**
Substitutes a preprocessor macro.

2        **#include**
Inserts a particular header from another file.

3        **#undef**
Undefines a preprocessor macro.