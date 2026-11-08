![](bbox=[0.0, 0.058, 0.292, 0.27])

# ## APPENDIX F
# HEADER FILES

The C++ standard library contains many predefined functions, named constants, and specialized data types. This appendix discusses some of the most widely used library routines (and several named constants). For additional explanation and information on functions, named constants, and so on, check your system documentation. The names of the Standard C++ header files are shown in parentheses.

# ## Header File `cassert` (`assert.h`)

The following table describes the function `assert`. Its specification is contained in the header file `cassert` (`assert.h`).

| Function | Description | Behavior |
|---|---|---|
| `assert(expression)` | `expression` is any int expression; `expression` is usually a logical expression | - If the value of `expression` is nonzero (true), the program continues to execute.\n- If the value of `expression` is 0 (false), execution of the program terminates immediately. The expression, the name of the file containing the source code, and the line number in the source code are displayed. |

> > To disable all of the `assert` statements, place the preprocessor directive `#define NDEBUG` before the directive `#include <cassert>`.