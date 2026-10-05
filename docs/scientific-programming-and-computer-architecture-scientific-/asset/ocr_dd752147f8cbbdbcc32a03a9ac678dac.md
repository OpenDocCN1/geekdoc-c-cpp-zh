# Chapter 1. C/C++: Review

| C programming | B.W. Kernighan and D.M. Ritchie, The C programming language, 2nd ed. |
| C++ programming | B. Stroustrup, The C++ programming language, 3rd ed. |

Table 1.3: Books on C and C++ written by their inventors.

# 1.2.1 Header files

A header file in C is an interface to one or more source files, with each source file a collection of function definitions. As an example of a simple header file, we look at aitken.h. This header file is an interface to the functions defined in aitken.c.

```
#ifndef aitkenJuly09DVsfe
#define double aitkenJuly09DVsfe
# void aitken(double *seq2, int len);
# double aitkenExtrapolate(double *seq1, double* seq2,
      int len);
#endif
```

The two symbolic names aitken and aitkenExtrapolate are introduced in this header file. These are the names of two functions that are defined in aitken.c. For the two functions, the declarations in the header file specify the type of the arguments as well as the type of value that is returned. This header file is saying that aitken() is a function that takes three arguments—the first two of type pointer to double and the last of type int—and returns nothing (void). The function aitkenExtrapolate() is stated to take three arguments of the same types, and returns double.

Both of these are examples of function declarations. The declarations specify the arguments the functions take in as well as the types of what they return. When a declaration is made, the function is stated to exist somewhere. However, a sequence of statements defining the functions is lacking.

The source files aitken.c, leibnitz.c, and logseries.c include aitken.h within their text using the line #include "aitken.h". The include statement has the effect of splitting all of aitken.h into those source files. The source aitken.c includes the header aitken.h and goes on to define the functions declared in the header.