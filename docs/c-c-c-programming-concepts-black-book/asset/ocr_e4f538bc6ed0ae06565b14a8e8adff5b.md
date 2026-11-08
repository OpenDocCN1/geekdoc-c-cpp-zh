The preprocessor contains the following directives:

+   - [ ] #if
+   - [ ] #ifdef
+   - [ ] #ifndef
+   - [ ] #else
+   - [ ] #elif
+   - [ ] #endif
+   - [ ] #include
+   - [ ] #define
+   - [ ] #undef
+   - [ ] #line
+   - [ ] #error
+   - [ ] #pragma

As we can see, all the preprocessor directives begin with a # sign. In addition, each preprocessor directive extends only across a single line of code. As soon as a newline character is found, the preprocessor directive is considered to end. No semicolon (;) is expected at the end of a preprocessor directive. For example, the following statement would not work:

```
```cpp
#include <iostream>     #include<string>
```
```

In this section, we cover only two of the preprocessor directives (#include and #define), as the other preprocessor directives are already covered in detail in the section on C Programming in this book. Let’s start the discussion on #include.

# # #include

The #include directive instructs the compiler to read another source file in addition to the one that contains the #include directive. The name of the additional source file must be enclosed between double quotes or angle brackets. For example, consider the following two statements:

```
```cpp
#include <iostream>
#include <string>
```
```

Both the preceding statements instruct the compiler to read and compile the header for the file system library functions. These can be both standard C++ input files and custom header files written by users. Both types of header files can also have #include directives in them. Such directives are referred to as nested includes. The number of levels of nesting varies from compiler to compiler. However, the ANSI C standard supports at least eight nested inclusions. Let’s say, that our program takes a header file myFile.hpp as one standard input file, and now when we check inside myFile.hpp, it might contain other include statements, such as #include <iostream>. Therefore, typically, our program, while being compiled, not only includes myFile.hpp, but also includes iostream before compilation.

The proposed ANSI C++ standard recommends that at least 256 levels of nested inclusions should be supported. The filename enclosed within quotes or angle brackets determines how the search for the specific file should be conducted. If the filename is enclosed in angle bracket, the file is searched for in a manner defined by the creator of the compiler. Often, this means searching some special directory set aside for include files. If the filename is enclosed in quotes, the file is looked for in another implementation-defined manner. For many compilers, this means searching the current working directory. If the file is not found, then the search is repeated as if the filename has been enclosed in angle brackets.