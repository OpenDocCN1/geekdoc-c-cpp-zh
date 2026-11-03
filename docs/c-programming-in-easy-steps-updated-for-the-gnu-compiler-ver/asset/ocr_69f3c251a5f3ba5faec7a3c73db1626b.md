# # Understanding compilation

In producing an executable file from an original C source code file, the compilation process actually undergoes four separate stages, which each generate a new file:

![](bbox=[0.07, 0.15, 0.33, 0.87])

+   - **Preprocessing** – The preprocessor substitutes all preprocessor directives in the original source code `.c` file with actual library code that implements those directives. For instance, library code is substituted for `#include` directives. The generated file containing the substitutions is in text format and typically has a `.i` file extension.
+   - **Translating** – The compiler translates the high-level instructions in the `.i` file into low-level Assembly language instructions. The generated file containing the translation is in text format and typically has a `.s` file extension.
+   - **Assembling** – The assembler converts the Assembly language text instructions in the `.s` file into machine code. The generated object file containing the conversion is in binary format and typically has a `.o` file extension.
+   - **Linking** – The linker combines one or more binary object `.o` files into a single executable file. The generated file is in binary format and typically has a `.exe` file extension.

Strictly speaking, “compilation” describes the first three stages above, which operate on a single source code text file and ultimately generate a single binary object file. Where the program source code contains syntax errors, such as a missing semi-colon statement terminator or a missing parenthesis, they will be reported by the compiler and compilation will fail.

The linker, on the other hand, can operate on multiple object files and ultimately generates a single executable file. This allows the creation of large programs from modular object files that may each contain reusable functions. Where the linker finds a function of the same name defined in multiple object files it will report an error and the executable file will not be created.