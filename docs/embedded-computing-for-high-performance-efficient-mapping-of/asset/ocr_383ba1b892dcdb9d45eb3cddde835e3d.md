large number of such expressions at the intermediate level representation of the code, which can then be simplified in later phases of the compiler optimization passes.

There are cases where one can substitute expressions by approximate ones. One example related to strength reduction is the use of (x>>1)+(x>>3) – (x>>6) – (x>>9) to substitute x*0.607259. This is a topic that we focus in more detail and in the context of function approximation.

When considering floating-point numbers, there are also opportunities to apply strength reduction. For example, the multiplication of a floating-point value by 2 can be done by adding one to the exponent of the representation. The following code shows how this can be done in the C programming language. We note however that C is not a particularly good example to perform this transformation, as it requires many operations in order to capture the right bits of the exponent, adding one, and placing the new exponent in the right place. In general, any multiplication of a floating-point number by an integer power of two can be substituted by adding a constant to the exponent of the floating-point representation.

```
// get the bit representation of the floating-point as an uint
unsigned int p1 = * (unsigned int *) &a;
// get the exponent
unsigned char exp = (p1 & (0xFF<<23))>>23;
// equivalent to multiply by 2
exp = exp + 1;
// add the new exponent to the representation of the floating-point value
p1 = (p1 & (~(0xFF<<23))) | (exp<<23);
// the resultant floating-point value: 2*a
float ax2 = * (float *) &p1;
```

Another example regarding floating-point values is when we need to negate a value, e.g., as in -1*a. This can be done by modifying the bit signal of the floating-point representation as it is shown in the following C code (for illustrative purposes as an implementation of this in a microprocessor is not profitable).

```
unsigned int p2 = * (unsigned int *) &a;
p2 ^= 1 << 31;
float neg_a = * (float *) &p2;
```

Strength reduction can be also applied in the context of loops as is illustrated in Fig. 5.1. In this case, the multiplication in Fig. 5.1A can be substituted by an addition (see Fig. 5.1B). Note that we can even go further if we change the loop control to reflect the index computations (see Fig. 5.1C).

This form of strength reduction can be typically applied to induction variables (i.e., to variables whose values are functions of the loop iteration values), and in some cases can lead to the elimination of the induction variable (induction variable elimination) altogether as shown in the example code in Fig. 5.1C.