# Chapter 2 Setting Out C++

these definitions to use the cout facility to display a message. The #include directive causes the contents of the iostream file to be sent along with the contents of your file to the compiler. In essence, the contents of the iostream file replace the #include <iostream> line in the program. Your original file is not altered, but a composite file formed from your file and iostream goes on the next stage of compilation.

> Note
Programs that use cin and cout for input and output must include the iostream.

# Header Filenames

Files as iostream are called include files (because they are included in other files) or header files (because they are included at the beginning of a file). C++ compilers use many header files, each supporting a particular family of facilities. The C tradition has been used to the h extension with header files as a simple way to identify the type of file by its name. The C .h file supports various C functions. Initially, C++ did the same. For instance, the header file supporting input and output was named iostream.h. But C++ usage has changed. Now the h extension is reserved for the C old header files (where C+ programs can still use), whereas C++ header files have no extension. There are also C header files that have been converted to C++ header files. These files have been renamed by dropping the h extension (making it a C++-style name) and prefixing the filename with a c (indicating that it is C+). For example, the C++ version of math.h is the cm header file. Sometimes the C and C++ versions of files are identical, in other cases the new version might have a few changes. For purely C++ header files such as iostream, dropping the h is more than a cosmetic change, for the h-free header files also incorporate namespaces, the next topic in this chapter. Table 2.1 summarizes the naming conventions for header files.

Table 2.1 Header File Naming Conventions
| Kind of Header | Convention | Example | Comments |
| --- | --- | --- | --- |
| C++ old style | Ends in .h | iostream.h | Usable by C++ programs |
| C old style | Ends in .h | math.h | Usable by C and C++ programs |
| C++ new style | No extension | iostream | Usable by C++ programs, uses namespace std |
| Converted C | c prefix, no extension | cm | Usable by C++ programs, might use non-C features, as namespace std |

In the C tradition of using different filename extensions to indicate different file types, it appears reasonable to have some special extension, such as .hpp or .hxx, to indicate C++ header files. The ANSI/ISO committee felt so, the problem was agreed on which extension to use, so eventually they agreed on nothing.