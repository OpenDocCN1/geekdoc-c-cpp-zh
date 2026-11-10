
## 11.10 LOCALITY OPTIMIZATIONS

### Reuse in Innermost Blocks

We adopt the simple model that data can be found in the cache if it is reused within a small number of iterations. If the innermost loop has a large or unknown bound, only reuse across iterations of the innermost loop translates into a locality benefit. Blocking creates inner loops with small known bounds, allowing reuse within and across entire blocks of computation to be exploited. Thus, blocking has the effect of capitalizing on more dimensions of reuse.

**Example 11.69:** Consider the matrix-multiply code shown in Fig. 11.5 and its blocked version in Fig. 11.7. Matrix multiplication has reuse along every dimension of its three-dimensional iteration space. In the original code, the innermost loop has *n* iterations, where *n* is unknown and can be large. Our simple model assumes that only the data reused across iterations in the innermost loop is found in the cache.

In the blocked version, the three innermost loops execute a three-dimensional block of computation, with *B* iterations on each side. The block size *B* is chosen by the compiler to be small enough so that all the cache lines read and written within the block of computation fit into the cache. Thus reused data across iterations in the third outermost loop can be found in the cache.

We refer to the innermost set of loops with small known bounds as the *innermost block*. It is desirable that the innermost block include all the dimensions of the iteration space that carry reuse, if possible. Maximizing the lengths of each side of the block is not as important. For the matrix-multiply example, 3-dimensional blocking reduces the amount of data accessed for each matrix by a factor of *B²*. If reuse is present, it is better to accommodate higher-dimensional blocks with shorter sides than lower-dimensional blocks with longer sides.

We can optimize locality of the innermost fully permutable loop nest by blocking the subset of loops that share reuse. We can generalize the notion of blocking to exploit reuses found among iterations of outer parallel loops, also. Observe that blocking primarily interleaves the execution of a small number of instances of the innermost loop. In matrix multiplication, each instance of the innermost loop computes one element of the array answer; there are *n²* of them. Blocking interleaves the execution of a block of instances, computing *B* iterations from each instance at a time. Similarly, we can interleave iterations in parallel loops to take advantage of reuses between them.

We define two primitives below that can reduce the distance between reuses across different iterations. We apply these primitives repeatedly, starting from the outermost loop until all the reuses are moved adjacent to each other in the innermost block.

### Interleaving Inner Loops in a Parallel Loop

Consider the case where an outer parallel loop contains an inner loop. To exploit reuse across iterations of the outer loop, we interleave the executions of a fixed number of instances of the inner loop, as shown in Fig. 11.63. Creating two-dimensional inner blocks, this transformation reduces the distance between reuse of consecutive iterations of the outer loop.

```text
for (i=0; i<n; i++)            for (ii=0; ii<n; ii+=4)
  for (j=0; j<n; j++)             for (j=0; j<n; j++)
    <S>                              for (i=ii; i<min(n, ii+4); i++)
                                        <S>
```

(a) Source program.                                      (b) Transformed code.

Figure 11.63: Interleaving 4 instances of the inner loop

### The step that turns a loop

```text
for (i=0; i<n; i++)
  <S>
```

into

```text
for (ii=0; ii<n; ii+=4)
  for (i=ii; i<min(n, ii+4); i++)
    <S>
```

is known as *stripmining*. In the case where the outer loop in Fig. 11.63 has a small known bound, we need not stripmine it, but can simply permute the two loops in the original program.

### Interleaving Statements in a Parallel Loop

Consider the case where a parallelizable loop contains a sequence of statements s₁, s₂, …, sₘ. If some of these statements are loops themselves, statements from consecutive iterations may still be separated by many operations. We can exploit reuse between iterations by again interleaving their executions, as shown in Fig. 11.64.

```text
for (i=0; i<n; i++) {
    <S1>
    <S2>
    ...
}
```

```text
for (i=0; i<n; i+=4) {
    for (j=i; j<min(n,i+4); j++)
        <S1>
    for (j=i; j<min(n,i+4); j++)
        <S2>
    ...
}
```

(a) Source program.

(b) Transformed code.

Figure 11.64: The statement-interleaving transformation

This transformation *distributes* a stripmined loop across the statements. Again, if the outer loop has a small fixed number of iterations, we need not stripmine the loop but simply distribute the original loop over all the statements.

We use sᵢ(j) to denote the execution of statement sᵢ in iteration j. Instead of the original sequential execution order shown in Fig. 11.65(a), the code executes in the order shown in Fig. 11.65(b).

![](img/2a44b9071782fade81f3050c3b718341_895_0.png)

Figure 11.65: Distributing a stripped loop

**Example 11.70:** We now return to the multigrid example and show how we exploit reuse between iterations of outer parallel loops. We observe that references *DW*[1, k, j, i], *DW*[1, k−1, j, i], and *DW*[1, k+1, j, i] in the innermost loops of the Fig. 11.62 have rather poor spatial locality. From reuse analysis, as discussed in Section 11.5, the loop with index *i* carries spatial locality and the loop with index *k* carries group reuse. The loop with index *k* is already the innermost loop, so we are interested in interleaving operations on *DW* from a block of iterations with consecutive *i* values.

We apply the transform to interleave statements in the loop to obtain the code in Fig. 11.66, then apply the transform to interleave inner loops to obtain the code in Fig. 11.67. Notice that as we interleave *B* iterations from loop with index *i*, we next expand variables *AP, AM, T* into arrays that hold *B* results at a time.

```text
for (j = 2; j <= jl; j++)
    for (ii = 2; ii <= il; ii+=b) {
        for (i = ii; i <= min(ii+b-1,il); i++) {
            ib          = i-ii+1;
            AP[ib]      = ...;
            T           = 1.0/(1.0 + AP[ib]);
            D[2,ib]     = T*AP[ib];
            DW[1,2,j,i] = T*DW[1,2,j,i];
        }
        for (i = ii; i <= min(ii+b-1,il); i++) {
            for (k=3; k <= kl-1; k++) {
                ib          = i-ii+1;
                AM          = AP[ib];
                AP[ib]      = ...;
                T           = ...AP[ib]-AM*D[ib,k-1]...;
                D[ib,k]     = T*AP;
                DW[1,k,j,i] = T*(DW[1,k,j,i]+DW[1,k-1,j,i])...;
            }
            ...
            for (i = ii; i <= min(ii+b-1,il); i++)
                for (k=kl-1; k>=2; k--) {
                    DW[1,k,j,i] = DW[1,k,j,i] + [D?][1,k+1,j,i];
                    /* Ends code to be executed by processor (j, i) */
                }
        }
    }
```

Figure 11.66: Excerpt of Fig. 11.23 after partitioning, array contraction, and blocking

### 11.10.4 Putting it All Together

Algorithm 11.71 optimizes locality for a uniprocessor, and Algorithm 11.72 optimizes both parallelism and locality for a multiprocessor.

### Algorithm 11.71: Optimize data locality on a uniprocessor.

**INPUT:** A program with affine array accesses.

**OUTPUT:** An equivalent program that maximizes data locality.

**METHOD:** Do the following steps:

- 1. Apply Algorithm 11.64 to optimize the temporal locality of computed results.
- 2. Apply Algorithm 11.68 to contract arrays where possible.
- 3. Determine the iteration subspace that may share the same data or cache lines using the technique described in Section 11.5. For each statement, identify those outer parallel loop dimensions that have data reuse.
- 4. For each outer parallel loop carrying reuse, move a block of the iterations into the innermost block by applying the interleaving primitives repeatedly.
- 5. Apply blocking to the subset of dimensions in the innermost fully permutable loop nest that carries reuse.
- 6. Block outer fully permutable loop nest for higher levels of memory hierarchies, such as the third-level cache or the physical memory.
- 7. Expand scalars and arrays where necessary by the lengths of the blocks.

### Algorithm 11.72: Optimize parallelism and data locality for multiprocessors.

**INPUT:** A program with affine array accesses.

**OUTPUT:** An equivalent program that maximizes parallelism and data locality.

**METHOD:** Do the following:

- 1. Use the Algorithm 11.64 to parallelize the program and create an SPMD program.
- 2. Apply Algorithm 11.71 to the SPMD program produced in Step 1 to optimize its locality.

### 11.10.5 Exercises for Section 11.10

**Exercise 11.10.1:** Perform array contraction on the following vector operations:

```text
for (i=0; i<n; i++) T[i] = A[i] * B[i];
for (i=0; i<n; i++) D[i] = T[i] + C[i];
```

**Exercise 11.10.2:** Perform array contraction on the following vector operations:
