
## 2.3.8 C Libraries and Functions

C has a rich collection of libraries. These libraries contain predefined functions that programmers can use. The code has already been written and tested for correctness and accuracy. The C library functions are grouped according to their functionality and use. Function prototypes for each of the groups is stored in a separate file called a header file. To access the groups of functions contained in these libraries the programmer must include the header files in the program by using the #include statement. The #include statement is a preprocessor directive. There are header files for input and output functions, character manipulation functions, mathematical functions, memory allocation functions, and other miscellaneous functions. As with all function declarations the header files must precede the main function. The linker/loader then knows what function implementations to load.

The header files, the detailed descriptions of the preprocessor directives, and most of the common functions are presented in Appendix B.

## 2.3.9 Review Questions

- 1. Indicate the following statements are true (T) or false (F).
    a. The order of precedence of arithmetic operators is important in the evaluation of a C expression.
    b. Parentheses have the lowest order of precedence in evaluating a C expression.
    c. The order of evaluation of the arithmetic operators is that division and/or multiplication is performed before addition and/or subtraction.
    d. The order of evaluation of an expression with parentheses is the same as the order of evaluation of a nonparenthesized expression.
    e. When an algebraic expression is divided by another algebraic expression you must enclose each of the expressions with parentheses.
    f. When an arithmetic operation involves a mixed data type, the data type is converted to the more complex data type, the arithmetic is carried out, and the result has the more complex data type.
    g. C has a large collection of library functions.

- 2. Write the equivalent C expression for each of the following algebraic expressions:
    a. x+y/z+wp
    b. (x+y) ÷ w+r-s
    c. 8(a+b) ÷ 6f-kn
    d. -a+bc -(-d)*g
    e. (1/3) bh+(1/4) kn

- 3. Given the values of the int variables: x=4, y=5, z=6, and w=2, compute the value of each of the following expressions:
    a. x+y*/z/w
    b. (x+y)/z+w
    c. (x+y*)z/w
    d. (x+y)/(z+w)
    e. (x+y)*z/w

- 4. Given the values of the following float variables: a=4.5, b=5.0, c=6.5, and d=2.5, compute the value of each of the following expressions:
    a. (a+b)/c*d
    b. (a+b)/c+d
    c. (a+b*c)/d
    d. (a+c)/(b+d)
    e. (a+b)+c/d

- 5. Given the following algebraic expressions, write the equivalent C expressions:
    a. (w+x)/(y+2)+xt
    b. ax+bx-cx+d
    c. (a+b+c)÷(d+e-(f+g))÷(1+j)
    d. volume=length·width·height
    e. force=mass·acceleration

- 6. Given the values of the int variables a=10, b=6 and float variables x=10.5, y=12.0, and w=8.5, determine the value computed and the value stored in each of the following assignment statements. The variables $s, t,$ and $r$ are type $int$, and $l$ and $m$ are type float.
    a. $s = a - b * 5 - x / 2 + y$;
    b. $t = a * x + b - y / 2$;
    c. $r = a / 2 + x + y$;
    d. $l = a * 5 + b / 2 - x - y + w$;
    e. $m = x + a / 2 + b - y * 5$;

- 7. Write the C assignment statements for each of the following equations used in engineering applications, where $p$ is pressure, $v$ is volume, $m$ is mass, $R$ is the universal constant, and $t$ is temperature:
    a. $p = (mRt)/v$
    b. $p1 = (p2v2)/v1$;
    c. From the equation $pv = mRt$, write a C statement to calculate the mass, given $p, v, R,$ and $t$.
    d. Given the formula $a = 4\pi r^2$ for the surface area of a sphere, write a C statement to calculate the radius of the sphere given the surface area.
    e. The moment of inertia of a disk about its fixed axis of rotation is given by $a = 0.5mr^2$. Write a C statement to calculate the mass given $a$ and $r$.
    f. The state equation for an ideal gas is given by the formula $p = \rho Rt$, where $p$ is absolute pressure, $\rho$ is mass density, $t$ is absolute temperature, and $R$ is the universal gas constant. Write a C statement to find the pressure for gases at $100^\circ$ Celsius.
    g. The pressure in a pipe carrying water is given by:
    $h = \frac{flv}{d^{2}g}$
    Where $f$ is the friction coefficient, $l$ is length, $v$ is velocity, $d$ is diameter, and $g$ is gravitational acceleration. Write a C statement to calculate $h$.
    h. The discharge over a rectangular weir is given by:
    $q = k\sqrt{2glh^{3/2}}$
    Write a C statement to calculate $q$.
    i. The effective resistance of a parallel circuit with five parallel resistances is given by:
    $r = \frac{1}{R1} + \frac{1}{R2} + \frac{1}{R3} + \frac{1}{R4} + \frac{1}{R5}$
    Write this as a C statement to calculate the effective resistance.

## 2.4 Overview of Implementation

Since C is a procedural language, the basic units of the program are the program. The code has already been written and tested for correctness and accuracy. The C library functions are grouped according to their functionality and use. Function prototypes for each of the groups is stored in a separate file called a header file. To access the groups of functions contained in these libraries the programmer must include the header files in the program by using the #include statement. The #include statement is a preprocessor directive. There are header files for input and output functions, character manipulation functions, mathematical functions, memory allocation functions, and other miscellaneous functions. As with all function declarations the header files must precede the main function. The linker/loader then knows what function implementations to load.

The header files, the detailed descriptions of the preprocessor directives, and most of the common functions are presented in Appendix B.

Since C is a procedural language, the basic units of the program are the program. The code has already been written and tested for correctness and accuracy. The C library functions are grouped according to their functionality and use. Function prototypes for each of the groups is stored in a separate file called a header file. To access the groups of functions contained in these libraries the programmer must include the header files in the program by using the #include statement. The #include statement is a preprocessor directive. There are header files for input and output functions, character manipulation functions, mathematical functions, memory allocation functions, and other miscellaneous functions. As with all function declarations the header files must precede the main function. The linker/loader then knows what function implementations to load.

The header files, the detailed descriptions of the preprocessor directives, and most of the common functions are presented in Appendix B.

Since C is a procedural language, the basic units of the program are the program. The code has already been written and tested for correctness and accuracy. The C library functions are grouped according to their functionality and use. Function prototypes for each of the groups is stored in a separate file called a header file. To access the groups of functions contained in these libraries the programmer must include the header files in the program by using the #include statement. The #include statement is a preprocessor directive. There are header files for input and output functions, character manipulation functions, mathematical functions, memory allocation functions, and other miscellaneous functions. As with all function declarations the header files must precede the main function. The linker/loader then knows what function implementations to load.

The header files, the detailed descriptions of the preprocessor directives, and most of the common functions are presented in Appendix B.

Since C is a procedural language, the basic units of the program are the program. The code has already been written and tested for correctness and accuracy. The C library functions are grouped according to their functionality and use. Function prototypes for each of the groups is stored in a separate file called a header file. To access the groups of functions contained in these libraries the programmer must include the header files in the program by using the #include statement. The #include statement is a preprocessor directive. There are header files for input and output functions, character manipulation functions, mathematical functions, memory allocation functions, and other miscellaneous functions. As with all function declarations the header files must precede the main function. The linker/loader then knows what function implementations to load.

The header files, the detailed descriptions of the preprocessor directives, and most of the common functions are presented in Appendix B.

Since C is a procedural language, the basic units of the program are the program. The code has already been written and tested for correctness and accuracy. The C library functions are grouped according to their functionality and use. Function prototypes for each of the groups is stored in a separate file called a header file. To access the groups of functions contained in these libraries the programmer must include the header files in the program by using the #include statement. The #include statement is a preprocessor directive. There are header files for input and output functions, character manipulation functions, mathematical functions, memory allocation functions, and other miscellaneous functions. As with all function declarations the header files must precede the main function. The linker/loader then knows what function implementations to load.

The header files, the detailed descriptions of the preprocessor directives, and most of the common functions are presented in Appendix B.

Since C is a procedural language, the basic units of the program are the program. The code has already been written and tested for correctness and accuracy. The C library functions are grouped according to their functionality and use. Function prototypes for each of the groups is stored in a separate file called a header file. To access the groups of functions contained in these libraries the programmer must include the header files in the program by using the #include statement. The #include statement is a preprocessor directive. There are header files for input and output functions, character manipulation functions, mathematical functions, memory allocation functions, and other miscellaneous functions. As with all function declarations the header files must precede the main function. The linker/loader then knows what function implementations to load.

The header files, the detailed descriptions of the preprocessor directives, and most of the common functions are presented in Appendix B.

Since C is a procedural language, the basic units of the program are the program. The code has already been written and tested for correctness and accuracy. The C library functions are grouped according to their functionality and use. Function prototypes for each of the groups is stored in a separate file called a header file. To access the groups of functions contained in these libraries the programmer must include the header files in the program by using the #include statement. The #include statement is a preprocessor directive. There are header files for input and output functions, character manipulation functions, mathematical functions, memory allocation functions, and other miscellaneous functions. As with all function declarations the header files must precede the main function. The linker/loader then knows what function implementations to load.

The header files, the detailed descriptions of the preprocessor directives, and most of the common functions are presented in Appendix B.

Since C is a procedural language, the basic units of the program are the program. The code has already been written and tested for correctness and accuracy. The C library functions are grouped according to their functionality and use. Function prototypes for each of the groups is stored in a separate file called a header file. To access the groups of functions contained in these libraries the programmer must include the header files in the program by using the #include statement. The #include statement is a preprocessor directive. There are header files for input and output functions, character manipulation functions, mathematical functions, memory allocation functions, and other miscellaneous functions. As with all function declarations the header files must precede the main function. The linker/loader then knows what function implementations to load.

The header files, the detailed descriptions of the preprocessor directives, and most of the common functions are presented in Appendix B.

Since C is a procedural language, the basic units of the program are the program. The code has already been written and tested for correctness and accuracy. The C library functions are grouped according to their functionality and use. Function prototypes for each of the groups is stored in a separate file called a header file. To access the groups of functions contained in these libraries the programmer must include the header files in the program by using the #include statement. The #include statement is a preprocessor directive. There are header files for input and output functions, character manipulation functions, mathematical functions, memory allocation functions, and other miscellaneous functions. As with all function declarations the header files must precede the main function. The linker/loader then knows what function implementations to load.

The header files, the detailed descriptions of the preprocessor directives, and most of the common functions are presented in Appendix B.

Since C is a procedural language, the basic units of the program are the program. The code has already been written and tested for correctness and accuracy. The C library functions are grouped according to their functionality and use. Function prototypes for each of the groups is stored in a separate file called a header file. To access the groups of functions contained in these libraries the programmer must include the header files in the program by using the #include statement. The #include statement is a preprocessor directive. There are header files for input and output functions, character manipulation functions, mathematical functions, memory allocation functions, and other miscellaneous functions. As with all function declarations the header files must precede the main function. The linker/loader then knows what function implementations to load.

The header files, the detailed descriptions of the preprocessor directives, and most of the common functions are presented in Appendix B.

### 2.4.1 Formatting of Statements

In C there are two types of statements: comment statements and program statements.

Comment Statement A comment statement starts with /* and ends with */. A comment statement can also continue into two or lines. Comments are not compiled or executed. They are used for program documentation and program

through this text every program is documented. The following examples show sample documentation.

Single line comment statement: /* This is a C program */

Multiple line comment statement: /* This program computes the average of ten integer numbers and prints the average */

Notice that a multiple line comment statement starts with /* and continues into the next line then ends with (*). Everything between /* and (*/) is part of the comment. ANSI C also supports single-line comments //.

Program Statements Program statements are free format; this means blank spaces can be inserted between variables, operators, reserved words, and parentheses for readability and clarity of the code. Any statement can continue into two or more lines. A program statement can start in any position on a line and end on the same line or on the next line. The following examples show a program statement.

```
a = b + c - d * e / f;
or a = b + c
- d * e / f;
```

Notice that the second statement is split between two lines; this is perfectly valid as long as it ends with a semicolon.

## 2.4.2 Formatting of a Program

A well designed program has separate sections for documentation, declarations, definitions, and program statements. These are stored in the program file. Data is
