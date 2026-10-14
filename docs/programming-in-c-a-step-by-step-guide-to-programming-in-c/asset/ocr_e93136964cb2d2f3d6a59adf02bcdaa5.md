# 2.6 Library functions

The C language is accompanied by a number of *library functions* or *built in functions* that carry out various commonly used operations or calculations. There are library functions that carry out standard input/output operations, functions that perform operations on characters, functions that perform operations on strings and functions that carry out various mathematical calculations.

Functionally similar library functions are usually grouped together as object programs in separate library files. A library function is accessed simply by writing the function name, followed by a list of arguments that represent information being passed to the function. A function that returns a data item can appear anywhere within an expression in place of a constant or an identifier. A function that carries out operations on data items but does not return anything can be accessed simply by writing the function name. A typical set of library functions will include a large number of functions that are common to most C compilers, such as those shown in table 2.1.

| Function |
|---|
| abs(i) |
| ceil(d) |
| cos(d) exp(d) fabs(d) floor(d) |
| getchar() |
| log(d) |
| pow(d1,d2) putchar(c) rand() |
| sin(d) |
| sqrt(d) |