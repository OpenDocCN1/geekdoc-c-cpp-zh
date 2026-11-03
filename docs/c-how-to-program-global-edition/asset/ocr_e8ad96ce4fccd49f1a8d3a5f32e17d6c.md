# ### Better to Use a Function

Macro CIRCLE_AREA could be defined more safely as a function. Function circleArea

```
    double circleArea(double x)
    {
        return 3.14159 * x * x;
    }
```

performs the same calculation as macro CIRCLE_AREA, but the function's argument is evaluated only once when the function is called. Also, the compiler performs type checking on functions—the preprocessor does not support type checking.

> > **Performance Tip 13.1**
> >
> > In the past, macros were often used to replace function calls with inline code to eliminate the function-call overhead. Today's optimizing compilers often inline function calls for you, so many programmers no longer use macros for this purpose. You can also use the C standard's inline keyword (see Appendix E).

# ### 13.4.2 Macro with Two Arguments

The following two-argument macro calculates the area of a rectangle:

```
    #define RECTANGLE_AREA(x, y)  ((x) * (y))
```

Wherever RECTANGLE_AREA(x, y) appears in the program, the values of x and y are substituted in the macro replacement-text and the macro is expanded in place of the macro name. For example, the statement

```
    rectArea = RECTANGLE_AREA(a + 4, b + 7);
```

is expanded to

```
    rectArea = ((a + 4) * (b + 7));
```

The value of the expression is evaluated at runtime and assigned to variable rectArea.

# ### 13.4.3 Macro Continuation Character

The replacement-text for a macro or symbolic constant is normally any text on the line after the identifier in the #define directive. If the replacement-text for a macro or symbolic constant is longer than the remainder of the line, a backslash (\) continuation character must be placed at the end of the line, indicating that the replacement-text continues on the next line.

# ### 13.4.4 #undef Preprocessor Directive

Symbolic constants and macros can be discarded by using the #undef preprocessor directive. Directive #undef “undefines” a symbolic constant or macro name. The scope of a symbolic constant or macro is from its definition until it’s undefined with #undef, or until the end of the file. Once undefined, a name can be redefined with #define.

# ### 13.4.5 Standard Library Functions and Macros

Functions in the standard library sometimes are defined as macros based on other library functions. A macro commonly defined in the <stdio.h> header is

```
    #define getchar() getc(stdin)
```