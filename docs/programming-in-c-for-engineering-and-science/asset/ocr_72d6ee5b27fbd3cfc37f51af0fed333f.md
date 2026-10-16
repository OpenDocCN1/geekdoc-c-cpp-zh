and the definition of celsiusToFahrenheit() is no longer present. The prototype and the definition of celsiusToFahrenheit() are not given in this file, because the prototype is in the header file of library Heat and the definition is in the library's implementation file.

It is important to note and understand the difference between the #include directive for one of the C++ standard libraries such as

```
#include <iostream>
```

and that used to include a programmer-defined library such as

```
#include "Heat.h"
```

In the first case where the name of the library is surrounded by angle brackets (< and >), the C++ compiler will search for it in the special system include directories. By contrast, if the name of a library's header file is enclosed in double quotes, the C++ compiler will search for it in the directory that contains the source file being compiled.⁹

# 6.4.3 Translating a Library

Translation of a program consists of two separate steps:

+   1. **Compilation:** translating a source program into an equivalent machine-language program called an *object program* that is stored in an *object file*. If the program uses a programmer-defined library, it too must be compiled and stored in a separate object file.
+   2. **Linking:** calls to library functions from a program are linked to the function definitions in the library, creating an *executable program*.

The following diagram illustrates this process:

![](bbox=[0.11, 0.76, 0.92, 0.9])

⁹ C++ also permits the programmer to store a library in a different directory (e.g., a library directory) and then instruct the compiler to search that directory when looking for files named by #include directives. The details of how to do this vary from one system to another.