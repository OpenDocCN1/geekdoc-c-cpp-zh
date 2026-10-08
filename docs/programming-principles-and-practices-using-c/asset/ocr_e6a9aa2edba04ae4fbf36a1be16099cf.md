For these, there are often C libraries based on arrays, pointers, and functions to help compensate. The main parts of the C standard library are

+   - **< stdlib.h>**: general utilities (e.g., **malloc()**) and **free()**; see \$27.4
- **< stdio.h>**: standard I/O; see \$27.6
- **< string.h>**: C-style string manipulation and memory manipulation; see \$27.5
- **< math.h>**: standard floating-point mathematical functions; see \$24.8
- **< errno.h>**: error codes for **< math.h>**; see \$24.8
- **< limits.h>**: sizes of integer types; see \$24.2
- **< time.h>**: date and time; see \$26.6.1
- **< assert.h>**: debug assertions; see \$27.9
- **< ctype.h>**: character classification; see \$11.6
- **< stdbool.h>**: Boolean macros

For a complete description, see a good C textbook, such as K&R. All of these libraries (and header files) are also available in C++.

# ## 27.2 Functions

In C:

+   - There can be only one function of a given name.
- Function argument type checking is optional.
- There are no references (and therefore no pass-by-reference).
- There are no member functions.
- There are no inline functions (except in C99).
- There is an alternative function definition syntax.

Apart from that, things are much as you are used to in C++. Let us explore what that means.

# ### 27.2.1 No function name overloading

Consider:

```
```C
void print(int);             /* print an int */
void print(const char*);     /* print a string */ /* error! */
```
```

The second declaration is an error because there cannot be two functions with the same name. So you'll have to invent a suitable pair of names: