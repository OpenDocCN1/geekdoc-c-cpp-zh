# # Exploring compilation

Whenever the C++ compiler runs, it first calls upon its preprocessor to seek any compiler directives that may be included in the source code. Each of these begin with the `#` hash character and will be implemented first to effectively modify the source code before it is assembled and compiled.

![](bbox=[0.118, 0.22, 0.247, 0.485])

The changes made by compiler directives to the preprocessor create new temporary files that are not normally seen. It is these temporary files that are used to create a binary object file:

+   - The first temporary file created during compilation expands the original source code by replacing its compiler directives with library code that implements those directives. This text file is named like the source file, but with a `.ii` file extension.
+   - The second temporary file created during compilation is a translation of the temporary expanded `.ii` file into low-level Assembly language instructions. This text file is named like the source file, but with a `.s` file extension.
+   - The third temporary file created during compilation is a translation of the temporary Assembly language `.s` file into machine code. This binary object file is named like the source file, but with a `.o` file extension.

So, the compilation process employs the Preprocessor to compile source code, an “Assembler” to translate this into machine code, and a Linker to convert one or more binary objects into an executable program.

You can see the temporary files by instructing the compiler to save them using the `-save-temps` compiler option. Both temporary text files can then be examined by opening them in a plain text editor.

Most significantly, you can see that the temporary file with the `.ii` file extension contains the complete function definitions from any included library. For example, it replaces an `#include <iostream>` directive with definitions for the `cin`, `cout`, `cerr` functions, and the `clog` function that can be used to redirect error messages to a file. The end of the `.ii` file shows the defined functions to be part of the “std” namespace – so they can appear without the `std::` prefix.

![](bbox=[0.118, 0.906, 0.18, 0.963])