+   - Compiler Generates assembly language code from a preprocessed source file.

+   - Assembler Converts an assembly language file into machine code (an object or .obj file).

+   - Linker Joins object files to create an executable file.

Machine code is simply a sequence of machine language instructions that a CPU can understand without any further translation. In other words a machine language instruction is a sequence of zeros and ones.

# Translation Unit

In C and C++, a translation unit is the final input into a C or C++ compiler. The compiler processes a translation unit and generates an object file from it.

A translation unit consists of a source file after it has been processed by the C or C++ preprocessor, meaning that the header files listed in the #include directives have been literally included, sections of code within #ifdef sections have been included, and macros have been expanded. A single translation unit is compiled by the compiler into a single object file.