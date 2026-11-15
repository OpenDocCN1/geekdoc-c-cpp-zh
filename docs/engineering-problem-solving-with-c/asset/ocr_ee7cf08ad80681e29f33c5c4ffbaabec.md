# # APPENDIX C Using MATLAB to Plot Data from ASCII Files

To understand engineering problems and engineering solutions to problems, it is important to be able to visualize the numerical information that is involved. Therefore, the ability to easily obtain simple x-y plots from data files is an important capability in solving engineering problems.

In this appendix, we present a simple C++ program that generates a data file, and we then show how to use MATLAB to obtain a plot of the data. We chose MATLAB (MATrix LABoratory) to generate the plots in this appendix and also in the text chapters because it is an extremely powerful software environment for interactive numeric computations, data analysis, and graphics. An extensive discussion on generating different types of plots and on additional options that can be specified within the plots is included in Chapter 7 of _Engineering Problem Solving with MATLAB_, by D. M. Etter, Prentice Hall, 1993.

In the following example, we use a C++ program to generate an ASCII (American Standard Code for Information Interchange) data file, and we then plot the information using MATLAB. An ASCII data file can also be generated using a word processor, and then the same steps can be used to plot the information using MATLAB. If the data file is generated with a word processor, it is important to select the options for saving the file such that it is saved as a text file instead of as a word processor file.

The program that follows generates a data file containing 100 lines of information. Each line contains the corresponding time and function value from the equation for a damped sine function, namely,

$f(t) = e^{-t} \sin(2\pi t)$,

where $t = 0.0, 0.1, 0.2, \dots, 9.9$ seconds.

# ## C++ Program to Generate a Data File

```
/* -------------------------------------------------- */
/* Program app_c                                      */
/*                                                    */
/* This program generates a data file of values       */
/* from a damped sine function.                       */
/* -------------------------------------------------- */

#include<iostream>
#include <fstream>
#include <cmath>
using namespace std;
const double PI = 3.141593;
```