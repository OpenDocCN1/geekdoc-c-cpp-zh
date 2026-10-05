# C Language: Storage Class Specifiers

Storage Class specifiers tell the compiler how to store a variable. C has four storage class specifiers:

+   * extern
* static
* register
* auto

Variables with storage class specifiers are declared as follows:

```
storage_class_specifier type variable_name;
```

# extern

C and C++ allow a large program to be broken up into files and for these files to be compiled separately and then linked together. Because of this, there must be some way of telling a file about variables that are declared in some other file.

A variable declaration declares the name and type of a variable. A variable definition causes storage to be allocated for the variable. In most cases, variable declarations and definitions are combined together (e.g. int x = 5). However when we precede a variable declaration with the *extern* specifier, we inform the compiler that the variable is declared in some other file.

One prominent use of *extern* is to declare all of the global variables in one file and use *extern* declarations in other files to access these variables.

Example:

File 1

File 2