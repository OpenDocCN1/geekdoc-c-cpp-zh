The source file contains the realization of all algorithms from which the executable will be generated.6 The header file contains declarations of the functions and classes that are implemented in the other file. Some functions may be used only internally and thus omitted in the header file. For instance, the math functions of our friend Herbert will be split into

```
// File: herberts/math_functions.hpp

#ifndef HERBERTS_MATH_FUNCTIONS_INCLUDE
#define HERBERTS_MATH_FUNCTIONS_INCLUDE

typedef double hreal; // Herbert's real numbers

hreal sine(hreal);
hreal cosine(hreal);
#endif
```

```
// File: herberts/math_functions.cpp

#include <herberts/math_functions.hpp>

hreal divide_by_square(hreal x, hreal y) { ... }

hreal sine(hreal) { ... }
hreal cosine(hreal) { ... }
...
```

We leave it to the reader's fantasy why Herbert introduced his own real number type. To use Herbert's magnificent functions, we need two things:

+   - The declarations by
+     - Including the header file herberts/math_functions.hpp or
+     - Declaring all desired functions ourselves.
+   - The compiled code by
+     - Linking against math_functions.o (.obj under Windows) or
+     - Linking against a library containing math_functions.o.

The declarations tell the compiler that the code for the functions with the given signatures exists somewhere and that they can be called in the current compilation unit.

The linking step then brings together the function calls with their actual code. The simplest way to link the compiled functions to some application is passing the object file or the archive as an argument to the C++ compiler. Alternatively, we could use a standard linker, but then we would need a handful of C++-specific extra flags.

# 7.2.3.2 Linkage Problems

During the linkage, the C++ entities like functions and variables are represented by symbols. C++ uses Name Mangling: decorating the symbol names with type and namespace (§3.2.1) information.