![](bbox=[0.17, 0.1, 0.81, 0.46])

# FIGURE 12.9

Parallel RF simulation with OpenMP. Tracing RF propagation paths is an embarrassingly parallel operation; however, careful attention to the expression of task-level parallelism in this context is required to maximize performance. These results depict scalar simulation performance, measured in terms of millions of rays per second, on two Intel Xeon E5-2699 processors using each of the three OpenMP parallelization strategies we explore.

As can be seen, when implemented in this way, simulator performance does not scale well with thread count. In fact, this version requires at least 16 threads before even a modest increase in performance is evident. This somewhat surprising behavior is a result of an implied barrier imposed at the end of the loop imposed by the parallel for construct. Each path segment will likely have a different computational cost due to variations in complexity of ray/object interactions or termination of the current path. Unfortunately, the barrier prevents other threads from making forward progress if any one segment is expensive to trace or if any one thread must create a new path. This parallelization strategy, though straightforward, induces unnecessary synchronization.

There are two approaches we examine to eliminate this unnecessary synchronization. One is to specify “nowait” which says that we do not want the implied barrier imposed at the end of the for loop. Another is to use the very flexible “task” capability of OpenMP.

First, we find that more careful use of OpenMP directives, by including the “nowait” clause, alleviates this issue (Figure 12.10). As before, this implementation spawns some number of threads using the omp parallel construct, but does so at the level of the while loop—not the nested for loop—so that