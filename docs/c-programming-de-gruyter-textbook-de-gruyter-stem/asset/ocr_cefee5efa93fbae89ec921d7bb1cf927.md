# 5.6 Multifile Structure and Compilation Preprocessing Directives 185

+   - Storage management class
- Algorithm
- Error handling
- Run-environment supporting

The declaration of predefined elements in the library is stored in different header files. To use these predefined elements, we should include the corresponding header files in our source files. The library and header files are a bit different in different compiling systems. For example, to use an I/O stream class in the VC++6.0 environment, the program should include the header file iostream.

To the readers who use a C++ environment, in the early versions before C++4.1, the library was called named *.h. The standard C++ library came into since C++4.2, and it meets the ANSI standard, enabling your program to be portable between different compiling systems and platforms. New header files do not have "h" as their name suffix, while the C++ standard library still retains 18 C header files with .h-suffixed names.

You can use header files of the old version ("*.h") or the new standard C++ library files (no filename suffix). The compiling system will determine which library to link automatically to the name of the header file. But you must pay attention that the two kinds of header files are not mixed in use. For example, if we have already included the header file iostream, then we cannot include math.h, and we should use the new header file cmath.

You can use predefined elements after including the corresponding header files. However, it is different when using standard C++ library, where you need to add the following statement to add the specified namespace to the current namespace:

```
using namespace std;
```

If we do not use the statement above, then we should use the namespace name "std::" to qualify the identifiers that belong to std namespace in use. We will introduce the concept of namespace in Chapter 10.

# 5.6.4 Compilation Preprocessing

The compiler will first use the preprocessing program to preprocess the program text before compiling the source program. A preprocessing program provides a group of compilation directives and preprocessing operators. Actually, preprocessing directives are not a part of C++; they are only used to extend the environment of C++ program design. Each preprocessing directive in a program occupies one separate line beginning with "#" and without a semicolon as the ending tag. Preprocessing directives can appear wherever they are needed.