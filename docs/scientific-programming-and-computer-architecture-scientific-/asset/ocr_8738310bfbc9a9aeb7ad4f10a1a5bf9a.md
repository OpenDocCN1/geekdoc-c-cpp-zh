# 5.1. Introduction to OpenMP

which returns the total number of threads in a parallel region when called by any thread. Calls of these functions are legal only inside parallel regions. They may not be called from functions that are called from parallel regions. However, the critical construct can be used even in functions called from parallel regions.

In addition to the two functions above, constructs such as omp master, omp ordered are occasionally useful.

# 5.1.2 Shared variables and OpenMP’s memory model

Let us look again at the critical construct.

```
#pragma omp critical
ans += sum;
```

As stated earlier, the critical construct ensures that the statement ans += sum is executed by one thread at a time. That may seem sufficient to ensure the correctness of the program because each thread would separately add its local sum to the final answer, but it is not.

The compiler may decide to store the variable ans in a register and add its local sum to a register when ans += sum executes. The code for copying the register to the memory location of ans may be inserted after the critical block. In case, we are back to the situation where the threads interfere with each other.

Why is not a problem? In answering this question, we arrive at the flush feature, which is a vital part of the OpenMP memory model. When a thread has a shared variable as ans, it is allowed to keep a copy of that variable in a register. When, the compiler generates assembly instructions, it may keep multiple copies of the same variable in memory and in the file for its convenience. When an OpenMP flush operation is executed, a thread must make all its writes visible to other threads even if it has only modified stored copies of a shared variable. The temporary view of all shared variables must be synced with the global view in shared memory.

The OpenMP standard requires that a thread should implicitly carry a critical or parallel construct, and at each barrier it encounters. Even the basic program for summing the Leibniz series relies on this rule for its correctness. Each thread syncs its local copy of ans with the global copy in shared memory when it enters the critical region, updates its local copy in the