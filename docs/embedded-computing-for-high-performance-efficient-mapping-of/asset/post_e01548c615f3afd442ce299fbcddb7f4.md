
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

```
for(i=0; i<N*4; i++) {
 Sum += A[4*i];
}
```

```
int j = 0;
for(i=0; i<N*4; i++) {
 Sum += A[i];
 j = j + 4;
}
```

```
int j = 0;
for(j=0; j<N; j+=4) {
 Sum += A[j];
}
```

FIG. 5.1 Strength reduction in the context of loops: (A) original loop; (B) applying strength reduction to 4*i; (C) moving the strength reduction to the loop control (a transformation also known as induction variable elimination).

Another important transformation is scalar replacement where references to array elements are replaced by references to scalar variables. Typically, a computation such as an accumulation of values is first performed on a scalar variable (possibly even mapped to a hardware register by the compiler). When the accumulation is completed, the value of the scalar variable is then transferred to the array location thus resulting in substantial savings in terms of array address calculation and load/store operations. In addition, scalar replacement can achieve data reuse when applied in the context of the reuse of subscripted variables. In this case, redundant array accesses can be eliminated and replaced by scalar accesses.

The use of scalar variables to replace accesses to arrays can be done for some of the elements of the array or for the entire array. A special case of scalar replacement, and usually enabled by loop unrolling, is register blocking. By unrolling loops, it is common to expose blocks of subscripted variables (registering array accesses) and to increase the opportunity to apply scalar replacement.

The following example presents an example of scalar replacement (sometimes known as loop scalar replacement). In this case accesses to array y over i are replaced with accesses to scalar y_aux and only one access to y for each i is required. This example shows the elimination of redundant array accesses using scalar replacement.

```
for (i=0;i<64;i++) {
 y[i] = 0;
 for (j=0;j<8;j++) {
 y[i] += x[i*64+j];
 }
}
```

```
for (i=0;i<64;i++) {
 y_aux = 0;
 for (j=0;j<8;j++) {
 y_aux += x[i*64+j];
 }
 y[i] = y_aux;
}
```

It is also possible to use scalar replacement on more sophisticated examples, in particular those that result from the application of loop unrolling as depicted in the following example. Here the value written to y[i] is stored in scalar variable yi and is subsequently used to compute y[i+1].

```
for (i=1;i<N;i++) {
 y[i] = x[i]*y[i-1];
}
```

```
for (i=1;i<N;i++) {
 y[i] = x[i]*y[i-1];
 y[i+1] = x[i]*y[i];
}
```

```
for (i=1;i<N;i+=2) {
 yi = x[i]*y[i-1];
 y[i] = yi;
 y[i+1] = x[i+1]*yi;
}
```

## 5.3 DATA TYPE CONVERSIONS

Data types impact memory usage and execution time. Depending on the data type, operations may require more or less clock cycles and the number of values that can be simultaneously loaded may also vary, e.g., affecting vectorization. It is common to convert floating-point data from double to single precision (if the resultant accuracy stays at acceptable levels). There are also cases of conversions from floating-point to integers and to fixed-point data types. While the effect of data type conversions may not be noticeable in most CPUs and GPUs, the impact can be very significant when using field-programmable gate array (FPGA)-based accelerators. Hence, an analysis of the impact of data conversions must include not only the resultant accuracy, but also the overhead associated with these conversions and the efficiency of the target architecture to compute operations with these transformed data types.

## 5.4 CODE REORDERING

In many cases, code reordering may significantly impact performance/energy/power. One example is the reordering of loops in nested loops (described in the section about loop transformations). In terms of instructions, it is common to rely on the reordering performed by the compiler based on data dependences, e.g., when scheduling instructions. There are cases, however, where developers may need to reorder instructions manually. One example is the reordering of cases in switch statements. The most frequent case (the common case) can be moved to the top as the top case needs less test and jump operations.

## 5.5 DATA REUSE

There are code transformations with the aim of maximizing data reuse. Data reuse is very important as it reduces the number of accesses to slow memory by using instead faster storage. Data reuse techniques eliminate repeated accesses to the same data, saving such data in internal registers and/or in faster access memories than where the data is originally stored. Frequently accessed data is saved in registers when it is first used and then reused in subsequent accesses. This increases data availability and avoids accesses to main memories. However, in the case of microprocessors, data reuse techniques may increase register pressure (as we may add additional scalar variables to the code), and it is not easy to apply them automatically due to compiler difficulties to identify data reuse opportunities for some data access patterns. There are cases of data reuse where the optimization benefits from hardware support, such as rotating registers.

Consider the code example in Fig. 5.2. For each iteration of the loop, we load one new position of x and two x positions already loaded in previous iterations (as shown in Fig. 5.3). We can transform the loop to store in scalar variables data that is reused
