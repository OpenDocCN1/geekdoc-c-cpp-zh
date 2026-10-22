# Functions

You will learn about the following in this chapter:

+   - Keyword:
+     `return`
+   - Operators:
+     `* (unary) & (unary)`
+   - Functions and how to define them
+   - How to use arguments and return values
+   - How to use pointer variables as function arguments
+   - Function types
+   - ANSI C prototypes
+   - Recursion

How do you organize a program? C’s design philosophy is to use functions as building blocks. We’ve already relied on the standard C library for functions such as `printf()`, `scanf()`, `getchar()`, `putchar()`, and `strlen()`. Now we’re ready for a more active role—creating our own functions. You’ve previewed several aspects of that process in earlier chapters, and this chapter consolidates your earlier information and expands on it.

# Reviewing Functions

First, what is a function? A *function* is a self-contained unit of program code designed to accomplish a particular task. Syntax rules define the structure of a function and how it can be used. A function in C plays the same role that functions, subroutines, and procedures play in other languages, although the details might differ. Some functions cause an action to take place. For example, `printf()` causes data to be printed on your screen. Some functions find a value for a program to use. For instance, `strlen()` tells a program how long a certain string is. In general, a function can both produce actions and provide values.