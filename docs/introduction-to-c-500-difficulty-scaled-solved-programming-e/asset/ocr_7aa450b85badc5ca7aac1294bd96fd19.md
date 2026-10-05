# 456 Introduction to C++

C++ provides several predefined preprocessing macros. The following table presents some of them. Their names are enclosed in double underscores. Their main purpose is to provide special information about the current implementation.

| NAME | DESCRIPTION |
| --- | --- |
| DATE | It is replaced with the compilation date. |
| FILE | It is replaced with the name of the compiled file. |
| LINE | It is replaced with the line number of the compiled file. |
| TIME | It is replaced with the time of the compilation. |
| func | It is replaced with some text which is defined by the implementation and name of the function. |

For example, consider the following program:

```
#include <iostream> // Example 15.5
int main() {
    std::cout << "Line " << LINE_ << " of file " << FILE_ << " in " 
function " << func_ << " is compiled on " << DATE_ << " at " << 
TIME_ << '\\n';
    return 0;
}
```

When I run the program, the output was:
Line 4 of file in function main is compiled on Feb 2019 at 17:32:52

This output is shown to that the program runs. If we recompile and run the new compile date and time will be displayed. In case of various versions of the same program, information might be macros to distinguish the running version. Furthermore, we can use the LINE_ and FILE_ macros to locate errors. For example:

```
if(error)
    cout << "Error in line " << LINE_ << " of file " << FILE_ << '\\n';
```

# THE assert( ) MACRO

For diagnostic purposes, C++ provides the assert( ) macro. It is declared in the cassert file, as follows:

```
void assert(exp);
```

If exp is true, nothing is displayed. Otherwise, assert( ) outputs an error message to cerr and calls the std::abort( ) function. This terminates the program immediately. The produced message depends on the implementation, but it contains the file name and the name of assert( ). For example:

assert( ); if conditions and directives that we'll see later (e.g., #ifdef) can be used for the same reason, that is, to detect potential bugs in the development phase. Once the program is tested, those checks