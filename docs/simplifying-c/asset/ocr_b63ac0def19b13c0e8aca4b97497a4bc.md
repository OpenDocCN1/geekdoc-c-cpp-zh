calculating value of x raised to a given power, and function sqrt is used to find square root of a given number. We can use these functions in our program if needed. To use these functions in a program, we need to include files that hold information about these functions. In C, these files are known as header files and usually have a file extension .h. The syntax to include header files in our program is `#include <filename.h>`. The list of header files available in C and their use is given in Appendix I of this book.

# ■ Global Variable Declaration Section

The use of C variables is governed by the place of their declaration. The function in which the variables are declared becomes the scope of the variable, which is decided by using opening and closing curly braces { }. The variables defined within curly braces are known as local variables. For example, the variables f_radius and f_crf used in Program 2 are local variables of the function main. These variables cannot be used outside the scope. At times we need to use a variable in all the functions, such a variable is known as global variable. This variable is defined before defining all the functions. The detailed discussion of global variables will be done in chapter dealing with functions in C language.

# ■ Main Function

All C programs contain one function with the name main( ). This is the function from where the execution of any C program starts. The control is first transferred to this function, and from here, the rest of the operations are carried out. In Programs 1 and 2, the core logic of solving the problem is part of the function main. It is possible that the core logic may be defined as a separate function and the function main uses it for solving the problem.

# ■ User-Defined Function

C program provides us a facility of splitting a single program into set of small functions. These functions can then be used independently in a program. In this subsection, we will see how two functions can be used in a single program.

The structure of the C program shown in Figure 2 is not a standard, although used by almost all programmers. It is also possible to interchange the place of sections within a C program. For example, user-defined function section can be interchanged with the main program section, and vice versa. Programs 3 and 4 give an example of such changes:

# ▶ Program 3

```
/* Program to multiply two numbers */

#include <stdio.h>

/* Prototype of a function multiply */
int multiply(int, int);

/* Beginning of main function */
main ( )
{
 int i_first, i_second, i_multiple;
 printf("Enter the value of first number: ");
 scanf("%d", &i_first);
```