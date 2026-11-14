
iteration space is not a multiple of the vector length, or in the case of loop unrolling when the iteration space is not multiple of the unrolling factor. This can be seen in the following loop vectorization example where the remainder N%4 of the iterations of the loop is moved to a second loop.

```c
//float *restrict A, float *restrict B
for(i = 0; i < N; i++)
    A[i] = B[i] + C;
```

```c
//float *restrict A, float *restrict B
// w/o assuming N%4=0
for(i = 0; i < (N-N%4); i+=4)
    A[i:i+3] = B[i:i+3] + C;
for(i = N - N%4; i < N; i++)
    A[i] = B[i] + C; //epilogue
```

### 5.6.10 LOOP STRIPMINING

Loop stripmining (also known as loop sectioning) transforms a loop in a double-nested loop and can be seen as a special case of loop tiling (see next subsection) in which only one of the loops is tiled (blocked). The following is an example of loop stripmining and as we can see, the loop on the left is transformed into two loops on the right: an outer loop responsible to iterate through the blocks and an inner loop to iterate over each block.

```c
for(i=0; i<N; i++) {
    sum += A[i];
}
```

```c
for(is=0; is<N; is+=S) { // S is the size of the 1-dimensional block
    for(js=is; js<min(is+S,N); js++) {
        sum += A[js];
    }
}
```

### 5.6.11 LOOP TILING (LOOP BLOCKING)

Loop tiling, also known as loop blocking, is a loop transformation that exploits spatial and temporal locality of data accesses in loop nests. This transformation allows data to be accessed in blocks (tiles), with the block size defined as a parameter of this transformation. Each loop is transformed in two loops: one iterating in each block (intratile) and the other one iterating over the blocks (intertile). Fig. 5.7 shows a simple example considering the use of loop tiling on two of the three nested “for” loops.

```c
for(i=0; i<N; i++) {
    for(j=0; j<N; j++) {
        for(k=0; k<N; k++)
            C[i][j] = C[i][j] + A[i][k]*B[k][j];
    }
}
```

```c
for(jj=0; jj<N; jj+=B8) {
    for(kk=0; kk<N; kk+=B8) {
        for(i=0; i<N; i++) {
            for(j=jj; j<min(jj+B8,N); j++) {
                for(k=kk; k<min(kk+B8,N); k++)
                    C[i][j] = C[i][j] + A[i][k]*B[k][j];
            }
        }
    }
}
```

(A) (B) FIG. 5.7 Loop tiling example: (A) original code; (B) code after loop tiling to loops j and k.

Loop tiling can target the different levels of memory (including the cache levels) and can be tuned to maximize the reuse of data at a specific level of the memory hierarchy. The transformation involves the use of specific block sizes and they can be fixed at compile time, and are calculated based on data sizes and memory (e.g., cache) size, and/or tuned at runtime.

### 5.6.12 LOOP UNROLLING

Loop unrolling is a well-known loop transformation. When unrolling a loop by a factor of K, the loop body is repeated K number of times and the loop iteration space is reduced (or eliminated when the loop is fully unrolled). Loop unrolling enables other optimizations and/or increases the parallelism degree in the loop body given the increase of its operations. As the number of iterations of a loop is not always known, there is a need to include a “clean-up” code as part of the prologue and/or epilogue of the loop when unrolled. However, when the number of iterations of the loop is known at compile time and it is a multiple of the unrolling factor no prologue or epilogue code is needed.

In the following example, the loop on the left is fully unrolled, which results in the code in the right.

```c
for(i=0; i<4;i++) {
    c[i] = a[i] + b[i];
}
```

```c
c[0] = a[0] + b[0];
c[1] = a[1] + b[1];
c[2] = a[2] + b[2];
c[3] = a[3] + b[3];
```

The following example shows the loop unrolled by a factor of 2. In this case, the loop is not eliminated.

```c
for(i=0; i<4;i+=2) {
    c[i] = a[i] + b[i];
    c[i+1] = a[i+1] + b[i+1];
}
```

When the number of iterations is not known at compile time and the intention is to unroll a loop by a factor, there is the need to include code to test if the number of iterations is greater or equal than the unrolling factor, and to include an epilogue (example on the left) or a prologue (example on the right).

```c
if(N > 2) {
    for(i=0; i<N-2;i+=2) { // K>=2
        c[i] = a[i] + b[i];
        c[i+1] = a[i+1] + b[i+1];
    }
} else i=0;
for(; i<N; i++) { // epilogue
    c[i] = a[i] + b[i];
}
```

```c
for(i=0; i<K; i++) // prologue
    c[i] = a[i] + b[i];
if(N > 2) {
    for(; i<N-2; i+=2) { // K>=2
        c[i] = a[i] + b[i];
        c[i+1] = a[i+1] + b[i+1];
    }
}
for(; i<N; i++) {
    c[i] = a[i] + b[i];
}
```

Loop unrolling is always a legal transformation as the order in which the operations are executed remains unchanged (special care must be taken in the presence of continue instructions). Yet, and as with other transformations that replicate code instructions, the compiler needs to evaluate the impact of code expansion that can result from the use of loop unrolling, in particular when the iteration space or the number of body statements is very large.

### 5.6.13 UNROLL AND JAM

Unroll and jam is a loop transformation that unrolls an outer loop by a factor and then fuse/merge (jam) the inner loops resultant from the outer loop unrolling. The following example shows an unrolling of 2 x and a jam which results in two stores of the y array per iteration of the outermost loop, maintaining a single innermost loop (this one with two loads of array z).

```c
for(i=0;i<4;i++) {
    y_aux = 0.0;
    for(j=0; j<64;j++)
        y_aux += z[i*64+j];
    y[i] = y_aux;
}
```

```c
// unroll 2x outermost loop and jam
for(i=0;i<4; i+=2) {
    y_aux0 = 0.0;
    y_aux1 = 0.0;
    for(j=0; j<64;j++){
        y_aux0 += z[i*64+j];
        y_aux1 += z[(i+1)*64+j];
    }
    y[i] = y_aux0;
    y[i+1] = y_aux1;
}
```

### 5.6.14 LOOP UNSWITCHING

Loop unswitching consists of moving loop invariant conditionals (conditions without side effects and whose logical values are independent of the loop iterations) outward. This transformation involves having as many loops as there are branch conditions, and each loop body executing the corresponding branch statements. The following example shows on the left a loop where there is a condition (op==1) which is not dependent on the loop iterations (i.e., during the execution of the loop it is always true or false). In this case, the condition can be moved to outside the loop and each branch of the if-statement has now a loop responsible for each of the original branch statements (see the following example on the right).

```c
for(i=0;i<m;i++) {
    if(op==1)
        sum += A[i];
    else
        sum *= A[i];
}
```

```c
if(op==1) {
    for(i=0;i<m;i++) {
        sum+=A[i];
    }
} else {
    for(i=0;i<m;i++) {
        sum *= A[i];
    }
}
```

The legality of this transformation hinges on the compiler's ability to determine if a given predicate is a loop invariant, and thus enables the use of this transformation.

### 5.6.15 LOOP VERSIONING

Loop versioning consists of generating multiple versions of a loop, in which each version's execution is predicated and selected at runtime. This transformation is always legal and is commonly used in conjunction with partial loop unrolling to test if the number of iterations of the loop evenly divides the selected unrolling factor.

This transformation can also be used to ensure the legality of other transformations. For example, the following code shows how a compiler can generate transformed code and use a predicate to ensure that a loop can be vectorized. In this case, it emits code that checks at runtime the absence of data dependences between the array variables (i.e., if arrays A and B are not fully or partially overlapped) and thus can be vectorized. If this predicate does not hold at runtime, then the loop is not vectorizable and the code will execute an alternative version of the loop (possibly the original loop version).

| | |
|---|---|
| `//Float *a, float *b`<br>`for(i = 0; i < N; i++)`<br>` A[i] = B[i] + C;` | `//float *a, float *b`<br>`// USE ORIGINAL VERSION:`<br>`if (((B[N-1] >= B[0]) && (B[N-1] >= A[0]))`<br>` for(...) { // N: i++ }`<br>` // USE VECTORIZED VERSION:`<br>` else { // assuming N==4`<br>` for(i = 0; i < N; i+=4)`<br>` A[i:i+3] = B[i:i+3] + C;`<br>` }` |

Typically, multiple versions corresponding to different optimizations of the same loop can coexist at runtime and selected depending on certain runtime properties. This transformation can be even extended when considering the use of hardware accelerators and/or computation offloading. In this case, multiple implementations of the same loop can be provided, and the decision to execute one of them is postponed to runtime.

### 5.6.16 SOFTWARE PIPELINING

Software pipelining [8] (also known as loop pipelining and loop folding) is a technique that overlaps loop iterations (i.e., subsequent iterations start before previous finished). This technique is suitable to increase performance but may also increase register pressure (not a main problem in reconfigurable architectures with pipeline stages). One of the most used software pipelining techniques is the iterative modulo scheduling [9].

All efficient compilers include software pipelining as part of their set of optimizations. This technique is mostly applied at the intermediate representation (IR) level of a program, but can also be applied at the source code level (and in this case, it is considered a code transformation technique, as the following example shows.

Software pipelining requires a prologue, a kernel, and an epilogue (see Fig. 5.8). They can be explicit as shown in the following example (middle) or implicit during execution as can be the case of code on the right. In the latter, predicated execution is used. The kernel is the section of code that iterates capturing all loop instructions. The prologue and the epilogue execute a subset of instructions (ramp-up and ramp-down).
