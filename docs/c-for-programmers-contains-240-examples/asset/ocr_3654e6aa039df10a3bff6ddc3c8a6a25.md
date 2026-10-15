The #include directive is used to include standard header files such as <iostream> and <iomanip>. The #include directive is also used with programs consisting of several source files that are to be compiled together. A header file containing declarations and definitions common to the separate program files is often created and included in the file. Examples of such declarations and definitions are classes, structures, unions, enumerations and function prototypes, constants and stream objects (e.g., cin).

# D.3 The #define Preprocessor Directive: Symbolic Constants

The #define preprocessor directive creates symbolic constants—constants represented as symbols—and macros—operations defined as symbols. The #define preprocessor directive format is

```
#define identifier replacement-text
```

When this line appears in a file, all subsequent occurrences (except those inside a string) of identifier in that file will be replaced by replacement-text before the program is compiled. For example,

```
#define PI 3.14159
```

replaces all subsequent occurrences of the symbolic constant PI with the numeric constant 3.14159. Symbolic constants enable you to create a name for a constant and use the name throughout the program. Later, if the constant needs to be modified throughout the program, it can be modified once in the #define preprocessor directive—and when the program is recompiled, all occurrences of the constant in the program will be modified. [Note: Everything to the right of the symbolic constant name replaces the symbolic constant. For example, #define PI = 3.14159 causes the preprocessor to replace every occurrence of PI with = 3.14159. Such replacement is the cause of many subtle logic and syntax errors.] Redefining a symbolic constant with a new value without first undefining it is also an error. Note that const variables in C++ are preferred over symbolic constants. Constant variables have a specific data type and are visible by name to a debugger. Once a symbolic constant is replaced with its replacement text, only the replacement text is visible to a debugger. A disadvantage of const variables is that they might require a memory location of their data type size—symbolic constants do not require any additional memory.

# Common Programming Error D.2

> Using symbolic constants in a file other than the file in which the symbolic constants are defined is a compilation error (unless they are #included from a header file).

# Good Programming Practice D.1

> Using meaningful names for symbolic constants makes programs more self-documenting.

# D.4 The #define Preprocessor Directive: Macros

[Note: This section is included for the benefit of C++ programmers who will need to work with C legacy code. In C++, macros can often be replaced by templates and inline functions.] A macro is an operation defined in a #define preprocessor directive. As with sym-