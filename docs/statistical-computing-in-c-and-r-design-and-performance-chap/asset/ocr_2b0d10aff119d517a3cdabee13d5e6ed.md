# 6

# INTRODUCTION

> X

| [1,] 1 2823297 2828507 |
| [2,] 1 2820724 2823269 |
| [3,] 1 2824568 2809724 |

Now, this X matrix is nonsingular and the coefficients can be determined directly using its inverse. The computational scheme evolves through updating (Xt)⁻¹ which requires it to be computed at this initial phase of the algorithm. An attempt to invert Xt R produces the response

> solve(t(X)%%*X)
Error in solve.default(t(X) %* X) :
system is computationally singular:
iprocal condition number = 1.33467e-22

But, X is nonsingular which means the thing is true for Xt. The problem is one of numerical singularity as indicated by the R message. This can be viewed as meaning that in terms of the precision the machine can maintain for the size of numbers exceeded one is singular. Another interpretation is that the numbers in the calculations have exceeded the ability of the computer to represent them in any meaningful sense.

The problem is actually quite easy to diagnose by the disparity between the size of values in the first column of X and the two columns that contains. We will see in Chapter 2, manipulation, particularly addition, numbers of very different magnitudes causes problems for computer arithmetic. The solution is to take a standard piece of advice from courses on linear regression: standardize values by, e.g., subtracting the means and dividing by their standard deviations. This transformation is performed the computations using the data in Figure 1.1 proceed without difficulty. Although the solution is not unique, this example does illustrate that a little of a computer's limitations can remove the memory from computational outcomes that might seem puzzling.

Chapter 2 is where some of the elements of C++ will be introduced. A detailed exploration of the language then begins in Chapter 3 with discussions of the C/C++ concept concept and execution control using if/else blocks and for/while loops. With this background, the next step is into the OOP aspects of the language that allow for creation of new data types with classes and their object instances. We also introduce the C++ approach to generic programming using template and functions.

One of the powers of C++ is the ability for dynamic memory allocation. Although one may delay the specification of the size of objects, as arrays, run-time. In particular, this makes possible for the memory of a program to be determined by input. Dynamic memory management is accomplished through a special type of variable pointer whose location is a location in the computer's physical memory. The use of pointers to create array structures is a key effective use of C/C++ in scientific computing. We spend some time in Chapter 3 on developing this idea and illustrate its usage via the construction of C classes that can represent matrices and vectors.

Although statistics is a mathematical science, it has a commonality with the lab sciences as well. In respect this the computer represents the statistician's and she/he uses, like a scientist, to experiment with new ideas related to statistical methodology. These experiments are usually of the Monte Carlo variety that rely on artificial data to assess the performance of new (and old) procedures. This makes random number generation an