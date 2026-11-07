The name of the `namespace` in each of these header files is `std`. Therefore, whenever certain features of a header file in ANSI/ISO Standard C++ are discussed, this book will refer to the identifiers without the prefix `std::`. Moreover, to simplify the accessing of identifiers in programs, the statement `using namespace std;` will be included. Also, if a program uses multiple header files, only one `using` statement is needed. This `using` statement typically appears after all the header files.

# ### Using the `string` Data Type in a Program

Recall that the `string` data type is a programmer-defined data type and is not directly available for use in a program. To use the `string` data type, you need to access its definition from the header file `string`. Therefore, to use the `string` data type in a program, you must include the following preprocessor directive:

```
```cpp
#include <string>
```
```

# ## Creating a C++ Program

In previous sections, you learned enough C++ concepts to write meaningful programs. You are now ready to create a complete C++ program.

A C++ program is a collection of functions, one of which is the function `main`. Therefore, if a C++ program consists of only one function, then it must be the function `main`. Moreover, a function is a set of instructions designed to accomplish a specific task. Until Chapter 6, you will deal mainly with the function `main`.

The statements to declare variables, the statements to manipulate data (such as assignments), and the statements to input and output data are placed within the function `main`. The statements to declare named constants are usually placed outside of the function `main`.

The syntax of the function `main` used throughout this book has the following form:

```
```cpp
int main()
{
    statement_1
    .
    .
    statement_n

    return 0;
}
```
```

In the syntax of the function `main`, each statement (`statement_1`, ..., `statement_n`) is usually either a declarative statement or an executable statement. The statement `return 0;` must be included in the function `main` and must be the last statement. If