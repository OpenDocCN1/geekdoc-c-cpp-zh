learn in this chapter will also be useful when working with modules.

# 11.1 Program, Library, Object File

When the compiler (or linker) assembles the executable program, it usually takes your translated source code and combines it with other libraries available in the system.

Each *.obj file represents a *.cpp file translated by the compiler that you have written. The *.dll files are libraries present on your system that your program is aware of but does not need to fully integrate (hence the dashed line in [Figure 11.1](Figure 11.1)). The [Figure 11.1] *.lib files are also libraries, but ones that your program integrates fully—or at least parts of them. For example, libraries of the C and C++ compilers as well as a game library are shown here. You may have acquired the latter from a third-party vendor so that you don't have to develop essential parts of the program yourself.

As a Unix user, you are more familiar with the extensions *.o, *.so, and *.a instead of *.obj, *.dll, and