# 5.1 Introduction to Modular Programming

three values must be passed to the calling routine. There is only one value to return, so it should be returned to the calling routine through a return statement. However, a function that determines the largest and smallest of a set of three values has to return two. This would be done through two addresses in the argument/parameter list of the calling and the called functions, for example minimax(x, y, z, &max, &min).

A function that returns a single value through its return statement is called a pure function. A function that returns values through its argument/parameter list is sometimes called a procedure or subroutine in other languages, but in C it also called a function.

As another example, consider a function to find, input, and validate a set of data. A set of values cannot be returned through the return statement, so they would be returned through the argument/parameter list, while the return statement would be used to indicate whether the input is successful. The scanf() function and other standard input functions do exactly that. A standard output function as printf() is a pure function in it does not return value through its parameters, but returns a value through its return statement, which indicates whether output has been successful.

In C, pure functions and subroutine-type functions can be written to replace frequently repeated code in a large program, provided that the repeated code meets the requirements of a functional module: entry at the top, exit at the bottom, and carries out a single task.

The advantage of using functions in modular programs is that any change made in a specific function that does not affect the argument/parameter list, is effectively isolated to that function. This prevents unwanted and hard-to-detect side effects. Only the function modified needs to be recompiled. Separately compiled, debugged, and recompiled functions are linked together by the computer to produce an executable program.

# 5.1.3 Review Questions

+   1. Indicate whether the following statements are true or false.
   a. Modular programming is a methodology to understand and implement solutions to complex problems.
   b. In the modular approach a large problem is divided into input, calculation, and output.
   c. A subproblem is simply a specific task performed in a program.