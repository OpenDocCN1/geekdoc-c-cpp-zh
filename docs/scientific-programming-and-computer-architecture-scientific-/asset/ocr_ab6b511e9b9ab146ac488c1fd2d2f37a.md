# Chapter 1. C/C++: Review

| x | Partial Sum | Extrapolate |
|---|---|--|
| 0.00 | 0.0000000000 | 0.0000000000 |
| 0.20 | 0.1823215568 | 0.1823215568 |
| 0.40 | 0.3364723763 | 0.3364722366 |
| 0.60 | 0.4700395318 | 0.4700036292 |
| 0.80 | 0.5895867562 | 0.5877866649 |
| 1.00 | 0.7301337551 | 0.6931471806 |
| 1.25 | 0.8615505069 | 0.8109302162 |

Table 1.2: The partial sum column is the sum of the first 13 terms of the Taylor series of log(1 + x). Each number in the last column is produced by applying the Aitken transformation 6 times to the first 13 partial sums, which leaves us with just one number. The last column shows that number, which gives log(1+x), with all the digits shown being correct.

partial sums recover the value of log(1 + x) for x = 1.25. If x were larger, just the first 13 partial sums would not be enough to produce 10 digits of accuracy after the decimal point.

Here we have our first programming problem. There is a simple iteration (1.1) to begin with. The problem is to code it in C/C++ and apply it to the Leibniz series and the logarithmic series.

# 1.1.2 Modular organization of sources

Before we delve into the syntax of C/C++, let us look at how to structure a program for the Aitken iteration. In particular, we look at how to split the program between source files.

It is not uncommon to introduce computer programming using programs that reside in a single source file. A computer program as a single source file is a bad idea to allow into one's head. It is a bad idea that can grow and grow. This author has heard of Fortran programs longer than 100,000 lines in a single file. Even the simple Aitken example shows why a single monolithic source is a bad idea.

> ⁶Events limited to a single source file rely on the runtime library. Strictly speaking, there is no such thing as a program that entirely resides in a single source file.