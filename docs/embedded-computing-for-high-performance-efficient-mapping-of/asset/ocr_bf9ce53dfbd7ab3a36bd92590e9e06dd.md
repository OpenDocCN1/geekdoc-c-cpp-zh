```
float dot_prod(float* a, float* b, int N) {
    float sum;
    #pragma omp parallel for shared(sum)
    for (int i = 0; i < N; i++) {
        #pragma omp critical {
            sum += a[i] * b[i];
        }
    }
    return sum;
}
```

Note that while omp critical can serialize any region of code, it exhibits an overhead. As an alternative, when the critical region is an expression statement updating a single memory location, the omp atomic clause may be used to provide lightweight locks. In OpenMP there are four atomic mode clauses: read, write, update, and capture. The read clause guarantees an atomic read operation, while the write clause ensures an atomic write operation. As an example, x is read atomically in the case of y = x + 5. The update clause guarantees an atomic update of a variable, e.g., y in the case of y = y + 1. Finally, the capture clause ensures an atomic update of a variable as well and the final value of the variables. For instance, if the capture clause is used with y = x++, then x is atomically updated and the value of y is captured.

Although shared variables can be accessed by all threads in a parallel region, OpenMP supports a relaxed consistency memory model, where at any point in time threads may not have the same view of the state of shared variables. This is because write operations performed in each thread may not immediately store data in main memory, opting instead to buffer the results to hide memory latency. To enforce a consistent view of shared variables at specific points in the thread execution, programmers need to use the omp flush ([a,b,c]) directive with the list of variables to be committed to main memory. If the list of variables is not specified, then all variables are flushed. As an example, consider the following code with two threads sharing two variables, x and y.

| thread 1 | thread 2 |
|---|---|
| int x = 0, y = 0; // shared variables | |
| x = 1; #pragma omp flush(x, y) if (y == 0) { /* critical section */ } | y = 1; #pragma omp flush(x,y) if (x == 0) { /* critical section */ } |

To ensure that only one thread has access to the “critical section,” the program must flush both variables to ensure the values observed by one thread are also observed by the other thread. While only one of the threads accesses the critical section, there is also a chance that neither will access the critical section. Memory flushes are thus not meant to synchronize different threads, but to ensure thread state is consistent with other threads. In general, a flush directive is required whenever shared data is accessed by multiple threads: after a write and before a read. Assuming a program with two threads T1 and T2 that share variable x, then the following sequence of operations must occur to ensure that both threads share a consistent view of that variable:

```
T1 [write X] -> T1 [flush X] -> T2 [flush X] -> T2 [read X]
```