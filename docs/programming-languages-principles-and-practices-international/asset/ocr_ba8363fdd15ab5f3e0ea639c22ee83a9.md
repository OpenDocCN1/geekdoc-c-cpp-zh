In particular, Section 13.3 will discuss **threads**, especially the Java thread implementation. Sections 13.4 and 13.5 will discuss **semaphores** and **monitors**, two approaches to the shared-memory model. Section 13.6 will study **message passing**, a mechanism that follows the distributed model, with examples from Ada. That section will also briefly mention a few of the issues surrounding the network model (which is a kind of distributed model).

We will also need a number of standard problems in parallel processing to demonstrate the use of particular mechanisms. We will use the following two problems throughout the remainder of this chapter (other problems are discussed in the exercises):

+   1. *The bounded buffer problem.* This problem assumes that two or more processes are cooperating in a computational or input-output situation. One (or more) process produces values that are consumed by another process (or processes). An intermediate buffer, or buffer process, stores produced values until they are consumed. A solution to this problem must ensure that no value is produced until there is room to store it and that a value is consumed only after it has been produced. This involves both communication and synchronization. When the emphasis is not on the buffer, this problem is called the *producer-consumer problem.*

+   2. *Parallel matrix multiplication.* This problem is different from the previous one in that it is an example of an algorithmic application in which the use of parallelism can cause significant speedups. Matrices are essentially two-dimensional arrays, as in the following declaration of integer matrices (we consider only the case where the size of both dimensions is the same, given by the positive integer constant N):

```
typedef int Matrix [N][N];
Matrix a,b,c;
```

The standard way of multiplying two matrices a and b to form a third matrix c is given by the following nested loops:

```
for (i = 0; i < N; i++)
    for (j = 0; j < N; j++)
        c[i][j] = 0;
        for (k = 0; k < N; k++)
            c[i][j] = c[i][j] + a[i][k] * b[k][j];
```

This computation, if performed sequentially, takes N³ steps. If, however, we assign a process to compute each c[i][j], and if each process executes on a separate processor, then the computation can be performed in the equivalent of N steps. Algorithms such as this are studied extensively in courses on parallel algorithms. In fact, this is the simplest form of such an algorithm, since there are no write conflicts caused by the computation of the c[i][j] by separate processes. Thus, there is no need to enforce mutual exclusion in accessing the matrices as shared memory. There is, however,