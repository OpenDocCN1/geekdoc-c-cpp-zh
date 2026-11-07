+   - **E.1** Introduction
+   - **E.2** `#include` Preprocessing Directive
+   - **E.3** `#define` Preprocessing Directive: Symbolic Constants
+   - **E.4** `#define` Preprocessing Directive: Macros
+   - **E.5** Conditional Compilation
+   - **E.6** `#error` and `#pragma` Preprocessing Directives
+   - **E.7** Operators `#` and `##`
+   - **E.8** Predefined Symbolic Constants
+   - **E.9** Assertions
+   - **E.10** Wrap-Up
+   
+   **Summary** | **Self-Review Exercises** | **Answers to Self-Review Exercises** | **Exercises**

# ## E.1 Introduction

This chapter introduces the preprocessor. Preprocessing occurs before a program is compiled. Some possible actions are inclusion of other files in the file being compiled, definition of symbolic constants and macros, conditional compilation of program code and conditional execution of preprocessing directives. All preprocessing directives begin with `#`, and only whitespace characters may appear before a preprocessing directive on a line. Preprocessing directives are not C++ statements, so they do not end in a semicolon (`;`). Preprocessing directives are processed fully before compilation begins.

> **Common Programming Error E.1**
> 
> Placing a semicolon at the end of a preprocessing directive can lead to a variety of errors, depending on the type of preprocessing directive.

![](bbox=[0.129, 0.485, 0.192, 0.526])

> **Software Engineering Observation E.1**
> 
> Many preprocessor features (especially macros) are more appropriate for C programmers than for C++ programmers. C++ programmers should familiarize themselves with the preprocessor, because they might need to work with C legacy code.

![](bbox=[0.129, 0.558, 0.192, 0.605])

# ## E.2 `#include` Preprocessing Directive

The `#include` preprocessing directive has been used throughout this text. The `#include` directive causes a copy of a specified file to be included in place of the directive. The two forms of the `#include` directive are

```
```cpp
#include <filename>
#include "filename"
```
```

The difference between these is the location the preprocessor searches for the file to be included. If the filename is enclosed in angle brackets (`<` and `>`)—used for standard library header files—the preprocessor searches for the specified file in an implementation-dependent manner, normally through predesignated directories. If the file name is enclosed in quotes, the preprocessor searches first in the same directory as the file being compiled, then in the same implementation-dependent manner as for a file name enclosed in angle brackets. This method is normally used to include program-defined header files.

The `#include` directive is used to include standard header files such as `<iostream>` and `<iomanip>`. The `#include` directive is also used with programs consisting of several