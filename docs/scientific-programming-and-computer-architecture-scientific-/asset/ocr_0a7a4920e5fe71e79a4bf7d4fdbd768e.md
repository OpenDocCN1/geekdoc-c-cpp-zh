# Cache flush

When programs are timed, one may inadvertently ignore the effects of caching and come up with unrealistically good numbers. Suppose we initialize three matrices to time algorithms for matrix-matrix multiplication.

```
for(int i=0; i < dim; i++) //initialize a, b and c
for(int j=0; j < dim; j++){
    a[i*j] = (1.0*rand()/RAND_MAX-0.5)*2;
    b[i*j] = (1.0*rand()/RAND_MAX-0.5)*2;
    c[i*j] = (1.0*rand()/RAND_MAX-0.5)*2;
}
```

The C library function rand() generates a pseudorandom integer between zero and RAND_MAX. It is for timing and testing but may not be a well-tested random generator.¹⁰ When pseudorandom numbers with specific properties, such as uniformity and independence, are needed, a good library of statistical functions must be used. For our purposes rand() is adequate, but in the manner which the matrices a, b, and c are initialized that they will all be in cache if dim is small. If dim=100, for example, the matrices will remain in the L2 cache of any of the processors table A.1, which are not more than 0.2 MB. In a realistic program, small matrices are unlikely to be in cache when they are needed because the program may touch a lot of data before initialization can starts operating on the small matrices. Thus, timing immediately after evict from cache as follows:

```
//clear a, b, c from cache
for(int i=0; i < dim; i++)
for(int j=0; j < dim; j++){
    mm_clflush(a+i*j);
    mm_clflush(b+i*j);
    mm_clflush(c+i*j);
}
```

The function mm_clflush() is an *intrinsic*. It corresponds directly to the instruction CLFLUSH. The effect of cache flush is to evict the entire cache line that corresponds to

> ¹⁰The general opinion that rand() is of poor quality appears to be from decades before. Whether that really applies to gcc and icpc runtime libraries is uncertain and possibly untrue.