
The process of developing a problem solution is often one of “divide and conquer,” as was discussed in Chapter 3 when we first discussed the decomposition outline. The decomposition outline is a set of sequentially executed steps that solves the problem, so it provides a good starting point for selecting potential functions. In fact, it is not uncommon for each step in the decomposition outline to correspond to one or more function references in the main function.

### Reusability

Breaking a problem solution into a set of modules has many advantages. Because a module has a specific purpose, it can be written and tested separately from the rest of the problem solution. An individual module is smaller than the complete solution, so testing it is easier. Also, once a module has been carefully tested, it can be used in new problem solutions without being retested. For example, suppose that a module is developed to find the average of a group of values. Once this module is written and tested, it can be used in other programs that need to compute an average. This reusability is a very important issue in the development of large software systems, because it can save development time. In fact, libraries of commonly used modules (such as Standard C library) are often available on computer systems.

### Modularity

The use of modules (called modularity) often reduces the overall length of a program because many problem solutions include steps that are repeated several places in the program. By incorporating these steps that are repeated in a function, the steps can be referenced with a single statement each time that they are needed.

Several programmers can work on the same project if it is separated into modules, because the individual modules can be developed and tested independently of each other. This allows the development schedule to be accelerated, because some of the work can be done in parallel.

### Abstraction

The use of modules that have been written to accomplish specific tasks supports the concept of abstraction. The modules contain the details of the tasks, and we can reference the modules without worrying about these details. The I/O diagrams that we use in developing a problem solution are an example of abstraction—we specify the input information and the output information without giving the details of how the output information is determined. In a similar way, we can think of modules as “black boxes” that have a specified input and that compute specified information; we can use these modules to help develop a solution. Thus, we are able to operate at a higher level of abstraction to solve problems. For example, the Standard C library contains functions that compute the logarithms of values. We can reference these functions without being concerned about the specific details, such as whether the functions are using infinite series approximations or lookup tables to compute the specified logarithms. By using abstraction, we can reduce the software development time while we increase its quality.

To summarize, there are several advantages to using modules in a problem solution:

- A module can be written and tested separately from other parts of the solution, and thus module development can be done in parallel for large projects.
- A module is a small part of the solution, and thus testing it separately is easier.
- Once a module is tested carefully, it does not need to be retested before it can be used in new problem solutions.
- The use of modules usually reduces the length of a program, making it more readable.
- The use of modules promotes the concept of abstraction, which allows us to “hide” the details in modules; this allows us to use modules in a functional sense without being concerned about the specific details.

Additional benefits of modules will be pointed out as we progress through this chapter.

Structure charts, or module charts, show the module structure of a program. The main function references additional functions, which may also reference other functions themselves. Figure 4.1 contains some of the structure charts for the programs developed in the Problem Solving Applied sections in this chapter and the next chapter. Note that a structure chart does not indicate the sequence of steps that are contained in the decomposition outline. The structure chart shows the separation of the program tasks into modules and indicates which modules reference other modules. Therefore, both the decomposition outline and the structure chart provide different but useful views of a problem solution. Also, note that the structure chart does not contain the modules referenced from the Standard C library because they are used so frequently and because they are an integral part of the C environment.

![](img/02c4582f051c5b51776411c92b079035_173_0.png)

Figure 4.1 Examples of structure charts.

As we begin to develop solutions to more complicated problems, the programs become longer. Therefore, three steps will help us debug longer programs. First, it may be helpful to run a program using a different compiler because different compilers have different error messages; in fact, some compilers have extensive error messages, whereas others give very little information about some errors. Another useful step in debugging a long program is to add comment indicators (/* and */) around some sections of the code so that you can focus on other parts of the program. Of course, you must be careful; do not comment out statements that affect variables needed for the parts of the program that you want to test. Finally, test complicated functions by themselves. This is usually done with a special program called a driver, whose purpose is to provide a simple interface between you and the function that you are testing. Typically, this program asks you to enter the parameters that you want passed to the function, and then it prints the value returned by the function. The usefulness of a driver program will become more apparent as we cover the next few sections.

![](img/02c4582f051c5b51776411c92b079035_174_0.png)

- Driver program

## 4.2 Programmer-Defined Functions

The execution of a program always begins with the main function. Additional functions are called, or invoked, when the program encounters function names. These additional functions must be defined in the file containing the main function or in another available file or library of files. (If the function is included in a system library file, such as the sort function, it is often called a library function; other functions are usually called programmer-written or programmer-defined functions.) After executing the statements in a function, the program continues with the statement that called the function.

- Invoked
- Library function
- Programmer-defined functions

### Function Example

The sinc(x) function, plotted in Figure 4.2, is commonly used in many engineering applications. The most common definition for sinc(x) is the following:

```
f(x) = sinc(x)
= \frac{\sin(\pi x)}{\pi x}
```

(The sinc(x) function is also occasionally defined to be sin(x)/x. The values of this function can be easily computed, except for sinc(0), which gives an indeterminate form of 0/0. In this case, l'Hôpital's theorem from calculus can be used to prove that sinc(0) = 1.

Assume that we want to develop a program that allows the user to enter interval limits, a and b. The program should then compute and print 21 values of sinc(x) for values of x evenly spaced between a and b, inclusive. Thus, the first value of x should be a. An increment should then be added to obtain the next value of x, and so on, until the twenty-first value, which should be b. Therefore, the increment in x is

```
x\_increment = \frac{\text{interval width}}{20} = \frac{b - a}{20}
```

![](img/02c4582f051c5b51776411c92b079035_175_0.png)

Figure 4.2 Sinc function in [-20, 20].

Select values for a and b, and convince yourself that, with this increment and with a as the first value, the twenty-first value will be b.
Because sinc(x) is not part of the mathematical functions provided by the Standard C library, we implement this problem solution in two ways. In one solution, we include the statements to perform the computations of sinc(x) in the main function; in the other solution, we write a programmer-defined function to compute sinc(x), and then reference the programmer-defined function each time that the computations are needed. Both solutions are now presented so that you can compare them.

### Solution 1

```
/*
 * ----------------------------------------------------------- */
/*
 * Program chapter4_1                                                */
/*
 * This program prints 21 values of the sinc                         */
/* function in the interval [a,b] using                              */
/* computations within the main function.                            */
/*
#include <stdio.h>
#include <math.h>
#define PI 3.141593

int main(void)
{
    /* Declare variables. */
    int k;
    double a, b, x_incr, new_x, sinc_x;

    /* Get interval endpoints from the user. */
    printf("Enter endpoints a and b (a<b): \n");
    scanf("%lf %lf", &a, &b);
    x_incr = (b - a)/20;

    /* Compute and print table of sinc(x) values. */
    printf("x and sinc(x) \n");
