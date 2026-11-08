# 4.2.12 Details on the Include Directive

Includes always begin with a hash sign #. Such a character at the beginning of a line stands for an instruction to the preprocessor. If you remember Chapter 2, Figure 2.1, you are already familiar with this phase of the translation.

The file that is included here with #include is inserted into your program by the preprocessor almost as if by copy and paste. The effect is that all declarations from that file are now part of your program.

There are other preprocessor directives, but #include is the most important one for you. The others can be found in Chapter 21.

Includes always belong at the top of your source files. In Listing 4.2, I have used two of them.

```
```cpp
#include <iostream>  // cin, cout
#include <string>    // stoi
```
```

Both <iostream> and <string> are part of the C++ standard library. They therefore contain things that are not part of the core language. Something like int is always present on all systems without the need for an include. The standard library will usually be present—and we assume that it will be in this book—but not always.

As you introduce many identifiers into the current source code with #include, it is helpful to add a comment to indicate which of them you are using in this translation unit. This allows readers to find out where an unknown identifier comes from by simply searching the file. Some module names are self-explanatory. For example, #include <vector> imports vector; there is no need to explain this.

You can recognize the includes of the standard library by the fact that the name does not have an extension such as .h or similar. The convention is that only header files of the standard library without an extension are used. If you create your own, then append an .h, .hpp, .H, .hh, or .hxx. In practice, .h is the most common, even if some programmers do not like this, as the header does not differ from C headers from the outside. The .hpp file extension is often chosen as an alternative. Regardless of which extension you use, you name it in the #include directive:

```
```cpp
#include <iostream>          // Module of the standard library
#include <asteroids.h>       // Module of a third-party provider
#include "myModule.hpp"      // Module of the current project
#include "algo/myModule.h"   // in a subdirectory
```
```

Write the name of the header file in angle brackets if the file is installed on your system; the compiler should search for it. Use the quotation marks "..." if the header file is part