
```
for(i=0; i<cX; i++) {
    for (j=0; j<cY; j++) {
        for (k=0; k<cZ; k++) {
            val = A[i][j][k];
            ...
        }
    }
}
```

```
for(m=0; m<C(*Y**2); m++) {
    i = m / (Y**2) + j;
    j = m % (Y**2) / i+1;
    k = m % i;
    val = A[i][j][k];
}
```

Unlike many loop transformations, loop coalescing does not require loops to be perfectly nested. For imperfectly nested loops, additional code needs to be included to ensure the right execution.

A special case of loop coalescing is loop collapsing [2], which can be applied when loop iteration bounds match array bounds, and arrays are accessed once per element. This is the case of the previous example. The following codes show the result after applying loop collapsing.

```
int *p = &A[0][0];
for(t=0; t<N*N; t++) {
    sum += *p;
}
}
```

```
int *p = &A[0][0];
for(t=0; t<N*N; t++) {
    sum += p[t];
}
}
```

As with loop alignment, loop coalescing and loop collapsing are always legal since they preserve the execution order of the original loop.

## 5.6.3 LOOP FLATTENING

Loop flattening [3] consists of replacing two or more nested loops in a single loop. Some authors refer to loop coalescing as loop flattening. However, we prefer to use the term loop flattening to refer to a more generic scheme to transform nested loops and sequenced loops in a single loop. In this categorization, loop coalescing and loop collapsing can be seen as special cases of loop flattening.

The following example is based on [3] and presents the result of applying loop flattening on a matrix-vector multiplication code for compressed sparse row (CSR).

```
for (i=0; i<N; i++) {
    y[i] = 0.0f;
    for (k=pntr[i]; k<pntr[i+1]; k++) {
        y[i] = y[i] + val[k]*vec[indx[k]];
    }
}
```

```
k=pntr[0]; i=1;
for (j=0; j<flatLength; j++) {
    if(t==pntr[i+1]-1) {
        y[i] = 0.0;
        i = pntr[i];
    }
    y[i] = y[i] + val[k]*vec[indx[k]];
    k++;
}
```

Generally, loop flattening can be based on the code template presented below. The idea is to ensure that the innermost loop bodies execute in all iterations of the new flattened loop and to limit the execution of the blocks at the level of the outermost loop according to the original loop definition. Also, loop flattening is always a legal loop transformation since the original execution order is not modified.

```
LOOP Outer
Body_1;
LOOP Inner
Body_2;
End Inner;
End Outer;

Loop Flatten: FlatIndex = Outer x max(Inner)
If(Last iteration of Inner (FlatIndex))
Body_1;
Body_2;
If(Last iteration of Inner (FlatIndex))
Body_3;
End FlatLoop
```

## 5.6.4 LOOP FUSION AND LOOP FISSION

Loop fusion (also known as loop merge) and loop fission (also known as loop distribution) merge a sequence of loops into one loop and split one loop into a sequence of loops, respectively.

Unlike other loop transformations previously mentioned, these two loop transformations change the order in which operations are executed, and therefore are only legal if the original data dependencies are preserved. With respect to data dependencies, loop fusion is legal if it does not introduce antidependences. Flow dependences are supported if they exist between the original loops before performing loop fusion. If the trip count of the loops being merged is not the same, the fusion of the loops needs additional code to enable the execution of the original iteration space for each loop’s block of code. With respect to data dependences, loop fission is illegal when there are lexically backward loop-carried data dependences.

Despite these restrictions, both transformations present various potential benefits (see, e.g., [4]). Loop fusion may increase the level of parallelism, data locality, and decrease the loop control overhead (by reducing the number of loops), but may also increase the pressure on register allocation. Loop fission, on the other hand, might be used to distribute computations and memory accesses in a way that may increase the potential for loop pipelining and loop vectorization, may reduce cache misses, and may decrease the pressure on register allocation. There are also cases where loop fusion allows the use of scalar replacement to array variables (also known as array contraction), as data may not need to be fully stored and can be communicated using scalars. Conversely, the use of loop fission may require that some scalars be stored in arrays (known as scalar expansion) to be available to other loops. Loop fission can also enable other transformations such as loop interchange.

## 5.6.5 LOOP INTERCHANGE AND LOOP PERMUTATION (LOOP REORDERING)

Loop interchange (also known as iteration interleaving) changes the order of execution between two loops in a loop nest (see, e.g., [5]). The technique is useful to improve the data memory access patterns and thus increase the overall code spatial locality. Also, it can enable other important code transformations. Loop permutation (or loop reordering) is a generalization of this loop interchange transformation when more than two loops are reordered.

The following code shows a simple example of applying loop interchange. In this case, this transformation provides stride 1 accesses to array A (code on the right) instead of stride M accesses (code on the left). Note, however, that the changes in the stride accesses are dependent on the programming language. For instance, the memory layout in C/C++ is different from Fortran/MATLAB. In particular, in Fortran/MATLAB, the corresponding codes on the left would yield stride 1 accesses to array A.

| for(j=0; j<M; j++) | for(i=0; i<N; i++) |
| :--- | :--- |
| for(i=0; i<N; i++) | for(j=0; j<M; j++) |
| A[i][j] += C; | A[i][j] += C; |

The legality of loop interchange depends on the type of dependences of the nested loops. When the direction of the dependences of the two loops to interchange are positive and negative, the interchange results in an illegal distance vector. The following code shows an example of an illegal distance vector. Consider the code on the left. The distance vector for i is -1, while the distance vector for j is +1, resulting in <-1, +1>. If we apply loop interchange (code on the right) the distance vector changes to <+1, -1> producing illegal code as antidependences change to true dependences (as shown with the following arrows).

| for(i=0; i<N; i++) | for(i=1; i<N; i++) |
| :--- | :--- |
| for(j=1; j<N; j++) | for(j=0; j<N-1; j++) |
| A[i][j] = A[i+1][j-1] + C; | A[i][j] = A[i+1][j+1] + C; |
| A[0][1] = A[1][0] + C | A[0][1] = A[1][0] + C |
| A[0][2] = A[1][1] + C | ... |
| ... | A[M-2][1] = A[M-1][0] + C |
| A[0][N-1] = A[1][N-2] + C | A[0][2] = A[1][1] + C |
| A[1][1] = A[2][0] + C | ... |
| ... | A[M-2][2] = A[M-1][1] + C |
| A[1][N-2] = A[2][N-3] + C | |
| A[1][N-1] = A[2][N-2] + C | |

## 5.6.6 LOOP PEELING

Loop peeling consists on separating (or peeling off ) iterations from the beginning and/or the end of the loop (see a simple example below). Loop peeling is always legal and can be used as the basis for better code generation in the context of scalar replacement and software pipelining. It is sometimes required to generate vector code with aligned vector loads/stores and to peel off some loop iterations to prologue and/or epilogue in loop unrolling and/or software pipelining.

```
for(i=0; i<n; i++) 
    sum += A[i];
```

```
sum += A[0];
for(i=1; i<n; i++) 
    sum += A[i];
```

## 5.6.7 LOOP SHIFTING

Loop shifting (see, e.g., [6]) consists of moving some of the statements from their original iteration to another loop iteration. This technique can be used to enable loop fusion and to identify when to move a loop inside a loop nest. In the following example, the original loop (left) is transformed to a loop (right) where in the first iteration only S2 is executed and in the last iteration only S1 is executed, i.e., as if one of these statements was shifted one iteration to the left or one iteration to the right.

```
for(i=1; i<n; i++) {
S1[i]=b[i]; //S1
d[i]=a[i-1]; //S2
}
```

```
for(i=0; i<n-1; i++) {
if(i>0) a[i]=b[i];
if(i<n-1) d[i+1]=a[i];
}
```

## 5.6.8 LOOP SKEWING

Loop skewing [7] is a transformation that changes the indexing and the corresponding loop control. For instance, in the following example the column accesses to array A are now given by a substitution between the two induction variables i and j.

```
for(j=0; j<n; j++)
for(i=0; i<n; i++)
sum += A[i][j-i];
```

```
for(j=0; j<n; j++)
for(i=j; i<n+j; i++)
sum += A[i][i-j];
```

## 5.6.9 LOOP SPLITTING

Loop splitting partitions a loop or loop nest in various loops, each one traversing a different iteration space (see a simple example below). This technique can be performed when considering data parallelism where the iteration space of the loop is split and each section is now executed as a thread, for example.

```
for(i = 0; i < N; i++)
A[i] = B[i] + C;
```

```
for(i = 0; i < M/2; i++)
A[i] = B[i] + C;
for(i = M/2; i < N; i++)
A[i] = B[i] + C;
```

Loop splitting can be also used to create prologues and epilogues of a loop (in this case it is similar to loop peeling) as in the case of loop vectorization when the
