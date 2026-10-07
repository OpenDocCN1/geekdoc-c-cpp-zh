# COMPUTER REPRESENTATION OF NUMBERS

quantities that correspond to command line input. In particular, one can use of char argv[] as an array of character strings (actually, a pointer to memory that holds arrays of char variables) with each string being a non-space component of the white-space delimited text that was entered on the shell command line. The first element argv[] contains the (/prefixed) name of the executable while strings held in argv. Another new twist is the use of the function atoi that is made available with the cstdlib header. The argument to atoi in this case is assumed to represent a sequence of digits that may be preceded by a sign. If the string cannot be interpreted as an integer, atoi returns 0. This is a method of dealing with the fact that command line input comes as character strings but will be used to represent numeric (in this integer) values. The function atof performs the same type of operation except that the transformation is to a floating-point representation.

To compute sums in Listing 2.3 we need to calculate reciprocals of the exponent j*k for a variable j int with multiplication. Unless precautions are taken to prevent the counter, such ratios will be evaluated using integer arithmetic with the consequence that a value of 0 is returned for 1/(j*j) for every j that exists. The circumvent this behavior is through the use of another cast. Here takes the form (float)(j*j) which computes the product and converts the output to type float.

Our program sums the series in direct and reverse order to produce the two sums: sumL and sumR. The values will necessarily agree if they be evaluated without error. This is not the case for finite precision arithmetic as indicated by the results from running the program (compiled with the names).

```
$.series5000
Direct and reverse sums are 1.6447253 1.6447344
```

As noted above, by type float one might expect for accuracy is seven decimal digits. But, the two computing of the sum have differences that appear in the first decimal place where n=5000 terms in the sum. To determine which answer is closer to the actual, the sums can be redone in double precision: i.e., every float designation in series.cpp is replaced with double. This altered set of code (compiled as deries) produced the result

```
$.series5000
Direct and reverse sums are 1.6447341 1.6447341
```

As expected, computing the sum in reverse order where smaller values are added in first provides the most accuracy. The approximate sums can be compared to $\sum_{j=1}^{\infty} j^{-2}=\pi^{2}/6=1.644934$.

# 2.6 Computing a sample variance

One of the earliest calculations carried out in an elementary methods course is computing a sample mean and standard deviation from a set of data values $x_{1},\dots,x_{n}$. The sample deviation is defined to be

```
$S=\sqrt{RSS/(n-1)}$
```

with RSS is the residual sum-of-squares

```
$RSS=\sum_{j=1}^{n}(x_{j}-\bar{x})^{2}$
```

with $\bar{x}=n^{-1}\sum_{j=1}^{n}x_{j}$ the sample mean.