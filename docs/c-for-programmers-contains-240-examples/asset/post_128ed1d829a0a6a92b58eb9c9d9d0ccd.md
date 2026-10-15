
The #include directive is used to include standard header files such as <iostream> and <iomanip>. The #include directive is also used with programs consisting of several source files that are to be compiled together. A header file containing declarations and definitions common to the separate program files is often created and included in the file. Examples of such declarations and definitions are classes, structures, unions, enumerations and function prototypes, constants and stream objects (e.g., cin).

## D.3 The #define Preprocessor Directive: Symbolic Constants

The #define preprocessor directive creates symbolic constants—constants represented as symbols—and macros—operations defined as symbols. The #define preprocessor directive format is

```
#define identifier replacement-text
```

When this line appears in a file, all subsequent occurrences (except those inside a string) of identifier in that file will be replaced by replacement-text before the program is compiled. For example,

```
#define PI 3.14159
```

replaces all subsequent occurrences of the symbolic constant PI with the numeric constant 3.14159. Symbolic constants enable you to create a name for a constant and use the name throughout the program. Later, if the constant needs to be modified throughout the program, it can be modified once in the #define preprocessor directive—and when the program is recompiled, all occurrences of the constant in the program will be modified. [Note: Everything to the right of the symbolic constant name replaces the symbolic constant. For example, #define PI = 3.14159 causes the preprocessor to replace every occurrence of PI with = 3.14159. Such replacement is the cause of many subtle logic and syntax errors.] Redefining a symbolic constant with a new value without first undefining it is also an error. Note that const variables in C++ are preferred over symbolic constants. Constant variables have a specific data type and are visible by name to a debugger. Once a symbolic constant is replaced with its replacement text, only the replacement text is visible to a debugger. A disadvantage of const variables is that they might require a memory location of their data type size—symbolic constants do not require any additional memory.

### Common Programming Error D.2

> Using symbolic constants in a file other than the file in which the symbolic constants are defined is a compilation error (unless they are #included from a header file).

### Good Programming Practice D.1

> Using meaningful names for symbolic constants makes programs more self-documenting.

## D.4 The #define Preprocessor Directive: Macros

[Note: This section is included for the benefit of C++ programmers who will need to work with C legacy code. In C++, macros can often be replaced by templates and inline functions.] A macro is an operation defined in a #define preprocessor directive. As with symbolic constants, the *macro-identifier* is replaced with the *replacement-text* before the program is compiled. Macros may be defined with or without *arguments*. A macro without arguments is processed like a symbolic constant. In a macro with arguments, the arguments are substituted in the *replacement-text*, then the macro is expanded—i.e., the *replacement-text* replaces the macro-identifier and argument list in the program. There is no data type checking for macro arguments. A macro is used simply for text substitution.

Consider the following macro definition with one argument for the area of a circle:

```
#define CIRCLE_AREA( x ) ( PI * ( x ) * ( x ) )
```

Wherever CIRCLE_AREA( y ) appears in the file, the value of y is substituted for x in the replacement text, the symbolic constant PI is replaced by its value (defined previously) and the macro is expanded in the program. For example, the statement

```
area = CIRCLE_AREA( 4 );
```

is expanded to

```
area = ( 3.14159 * ( 4 ) * ( 4 ) );
```

Because the expression consists only of constants, at compile time the value of the expression can be evaluated, and the result is assigned to area at runtime. The parentheses around each x in the replacement text and around the entire expression force the proper order of evaluation when the macro argument is an expression. For example, the statement

```
area = CIRCLE_AREA( c + 2 );
```

is expanded to

```
area = ( 3.14159 * ( c + 2 ) * ( c + 2 ) );
```

which evaluates correctly, because the parentheses force the proper order of evaluation. If the parentheses are omitted, the macro expansion is

```
area = 3.14159 * c + 2 * c + 2;
```

which evaluates incorrectly as

```
area = ( 3.14159 * c ) + ( 2 * c ) + 2;
```

because of the rules of operator precedence.

### Common Programming Error D.3

> Forgetting to enclose macro arguments in parentheses in the replacement text is an error.

Macro CIRCLE_AREA could be defined as a function. Function circleArea, as in

```
double circleArea( double x ) { return 3.14159 * x * x; }
```

performs the same calculation as CIRCLE_AREA, but the overhead of a function call is associated with function circleArea. The advantages of CIRCLE_AREA are that macros insert code directly in the program—avoiding function overhead—and the program remains readable because CIRCLE_AREA is defined separately and named meaningfully. A disadvantage is that its argument is evaluated twice. Also, every time a macro appears in a program, the macro is expanded. If the macro is large, this produces an increase in program size. Thus, there is a trade-off between execution speed and program size (if disk space is low).

Note that inline functions (see Chapter 6) are preferred to obtain the performance of macros and the software engineering benefits of functions.

### Performance Tip D.1

Macros can sometimes be used to replace a function call with inline code prior to execution time. This eliminates the overhead of a function call. Inline functions are preferable to macros because they offer the type-checking services of functions.

The following is a macro definition with two arguments for the area of a rectangle:

```
#define RECTANGLE_AREA( x, y ) ( ( x ) * ( y ) )
```

Wherever RECTANGLE_AREA( a, b ) appears in the program, the values of a and b are substituted in the macro replacement text, and the macro is expanded in place of the macro name. For example, the statement

```
rectArea = RECTANGLE_AREA( a + 4, b + 7 );
```

is expanded to

```
rectArea = ( ( a + 4 ) * ( b + 7 ) );
```

The value of the expression is evaluated and assigned to variable rectArea.

The replacement text for a macro or symbolic constant is normally any text on the line after the identifier in the #define directive. If the replacement text for a macro or symbolic constant is longer than the remainder of the line, a backslash (\ ) must be placed at the end of each line of the macro (except the last line), indicating that the replacement text continues on the next line.

Symbolic constants and macros can be discarded using the #undef preprocessor directive. Directive #undef “undefines” a symbolic constant or macro name. The scope of a symbolic constant or macro is from its definition until it is either undefined with #undef or the end of the file is reached. Once undefined, a name can be redefined with #define.

Note that expressions with side effects (e.g., variable values are modified) should not be passed to a macro, because macro arguments may be evaluated more than once.

### Common Programming Error D.4

Macros often replace a name that wasn’t intended to be a use of the macro but just happened to be spelled the same. This can lead to exceptionally mysterious compilation and syntax errors.

## D.5 Conditional Compilation

Conditional compilation enables you to control the execution of preprocessor directives and the compilation of program code. Each of the conditional preprocessor directives evaluates a constant integer expression that will determine whether the code will be compiled. Cast expressions, sizeof expressions and enumeration constants cannot be evaluated in preprocessor directives because these are all determined by the compiler and preprocessing happens before compilation.

The conditional preprocessor construct is much like the if selection structure. Consider the following preprocessor code:

```
#ifndef NULL
#define NULL 0
#endif
```
