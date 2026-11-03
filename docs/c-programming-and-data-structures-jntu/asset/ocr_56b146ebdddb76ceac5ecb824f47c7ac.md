# Decision Making and Looping 7.21

The use of structured programming techniques helps ensure well-designed programs that are easier to write, read, debug and maintain compared to those that are unstructured. Structured programming discourages the implementation of unconditional branching using jump statements such as goto, break and continue. In its purest form, structured programming is synonymous with "goto less programming". Do not go to goto statement!

# CASE STUDIES

# 1. Table of Binomial Coefficients

Problem: Binomial coefficients are used in the study of binomial distributions and reliability of multicomponent redundant systems. It is given by B(m, x) = (m choose x) = m! / (x! (m-x)!) , m >= x

A table of binomial coefficients is required to determine the binomial coefficient for any set of m and x.

Problem Analysis: The binomial coefficient can be recursively calculated as follows: B(m, x) = B(m, x - 1) * [(m - x + 1) / x] , x = 1, 2, 3, ..., m

Further, B(m, 0) = 1 B(0, x) = 1

That is, the binomial coefficient is one when either x is zero or m is zero. The program in Fig. 7.12 prints the table of binomial coefficients for m = 10. The program employs one do loop and one while loop.

```
#include <stdio.h>
/* EVALUATION OF BINOMIAL COEFFICIENTS */
#define MAX 10
{
int m, x, binom;
printf("m x\n");
for (m=0; m<=10; ++m)
printf("%4d", m);
printf("\n");
m=0;
do {
printf("%4d ", m);
x=0; binom=1;
while (x <= m) {
printf("%4d", binom);
binom = binom * (m - x +1) / x;
x++;
}
printf("\n");
m++;
} while (m <=10);
}
```