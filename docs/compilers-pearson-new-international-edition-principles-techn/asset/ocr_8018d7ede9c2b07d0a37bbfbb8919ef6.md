# 11.7. *FINDING SYNCHRONIZATION-FREE PARALLELISM*

**Example 11.40:** As discussed above, the code of Fig. 11.24 has two degrees of parallelism. We view the processor array as a 2-dimensional space. Let $(p_1,p_2)$ be the ID of a processor in the array. The parallelization scheme discussed in Section 11.7.1 can be described by simple affine partition functions. All the statements in the first loop nest have this same affine partition:

$$\begin{bmatrix}p_1\\p_2\end{bmatrix}=\begin{bmatrix}1&0\\0&1\end{bmatrix}\begin{bmatrix}j\\i\end{bmatrix}+\begin{bmatrix}0\\0\end{bmatrix}$$

All the statements in the second and third loop nests have the following same affine partition:

$$\begin{bmatrix}p_1\\p_2\end{bmatrix}=\begin{bmatrix}0&1&0\\0&0&1\end{bmatrix}\begin{bmatrix}k\\j\\i\end{bmatrix}+\begin{bmatrix}0\\0\end{bmatrix}$$

The algorithm to find synchronization-free parallelism consists of three steps:

+   1. Find, for each statement in the program, an affine partition that maximizes the degree of parallelism. Note that we generally treat the statement, rather than the single access, as the unit of computation. The same affine partition must apply to each access in the statement. This grouping of accesses makes sense, since there is almost always dependence among accesses of the same statement anyway.
+   
+   2. Assign the resulting independent computation units among the processors, and choose an interleaving of the steps on each processor. This assignment is driven by locality considerations.
+   
+   3. Generate an SPMD program to be executed on each processor.

We shall discuss next how to find the affine partition functions, how to generate a sequential program that executes the partitions serially, and how to generate a SPMD program that executes each partition on a different processor. After we discuss how parallelism with synchronization is handled in Sections 11.8 through 11.9.9, we return to Step 2 above in Section 11.10 and discuss the optimization of locality for uniprocessors and multiprocessors.

# 11.7.3  Space-Partition Constraints

To require no communication, each pair of operations that share a data dependence must be assigned to the same processor. We refer to these constraints as “space-partition constraints.” Any mapping that satisfies these constraints creates partitions that are independent of one another. Note that such constraints can be satisfied by putting all the operations in a single partition. Unfortunately, that “solution” does not yield any parallelism. Our goal is to create