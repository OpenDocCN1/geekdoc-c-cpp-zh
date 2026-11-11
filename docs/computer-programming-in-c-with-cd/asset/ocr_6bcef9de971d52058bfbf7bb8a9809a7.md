```
```cpp
#ifdef _cplusplus
cout << "This is a C++ program." << endl;
#endif
```
```

Some of the predefined tokens you can use in your code are as follows:

+   - `_cplusplus`: Defined if the current program is in C++
+   - `_STDC_`: Defined if the current program is in standard C
+   - `__LINE__`: Holds the current line number
+   - `__FILE__`: Holds the current file name
+   - `__DATE__`: Holds the date of compilation of a program
+   - `__TIME__`: Holds the time of compilation of a program

Preprocessor directives also support *macros*, which are sections of predefined code. These macros are replaced by the preprocessor along with the values stored in the macros. All preprocessor directives are discussed in detail under following sections:

+   - The #define directive
+   - The #undef directive
+   - The #include directive
+   - Directives used in conditional compilation

# The #define Directive

The #define directive is a preprocessor directive used to give a meaningful name to a constant in a C++ program and the constant is then used as a macro in the program. The #define directive is used in the following two ways:

+   - To define a variable holding a constant value
+   - To define a function constant

The two syntaxes to use the # define directive are:

```
```cpp
#define <macro/constant name> < value> // defining constant variable/macro
#define < func_name () > < func_val> // function constant/macro
```
```

In the first syntax, macro/constant name can be any logical variable name to be used as a constant or macro, and value can be any logical value assigned to the variable. An example of this can be #define PI 3.14. In this case, all occurrences of PI in the program are replaced with the value 3.14.

In the second syntax, func_name() is the function name whose macro has to be created, and func_val is the value to be assigned to the parameters passed in the function. For example, in #define radius (a) (PI *a*a), a will be replaced with the parameter passed in the function radius from a C++ program. Now, consider the following code snippet to understand the concept of function macro better:

```
```cpp
result = radius (a);
```
```