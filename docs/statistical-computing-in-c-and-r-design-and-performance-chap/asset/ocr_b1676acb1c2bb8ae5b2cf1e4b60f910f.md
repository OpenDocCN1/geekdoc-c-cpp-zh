# 188 PROGRAMMING IN R

d for an integer variable,

e for a floating-point variable in scientific notation,

f for a floating-point variable and

s for printing a character string.

Carriage returns are created by placing a \n inside the character string argument.
The initial argument to R printf in our program is "Hello y'all %d times!\n". The %d informs the compiler that the next argument is an integer variable and the printing
format is to be tailored to a variable of that type. The \n character at the end of the
character string produces a new line after printing the message.

To compile the C code we enter

```
$ R CMD SHLIB hello.c
```

On the shell command line. This creates a shared library hello.so that can now be
imported into R using the dyn.load utility. Specifically, this is accomplished inside R with

```
> dyn.load("hello.so")
> is.loaded("hello")
[1] TRUE
```

The is.loaded function checks that the shared library has been successfully loaded.
Once a shared C/C++ library has been imported, the underlying program can be executed
using the .C function. For our example the result might appear something like

```
> .C("hello", as.integer(3))
Hi ya'all 0 times!
Hi ya'all 1 times!
Hi ya'all 2 times!
[[1]]n[1] 4
```

The list information provided at the end of this output is what has been returned by the
.C function. It represents the values of the arguments (i.e., the values stored in the memory
locations for the pointers that were passed in the function call) that were returned from the
hello program. In particular the output shows that last line of the C program had the
effect of advancing the value of n (from the initial value assigned in R) by one unit. Also,
note that the use of as.integer for passing the integer 3 into the C program
is necessary.

A similar program can be developed in C++ as we now demonstrate. First, we will be
a class with a header file X.hh (the hh file extension is necessary) that contains the code

```
//X.hh
#ifndef X_HH
#define X_HH
class X {
int n;
public:
X(int N);
X();
};
#endif
```

The class constructor and destructor are defined in X.cc (again, the cc file extension is
necessary) as