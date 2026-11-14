![](bbox=[0.25, 0.11, 0.8, 0.4])

# FIG. 6.6 OpenMP loop worksharing execution.

variable as it was defined outside the parallel block. Shared variables can be accessed by all threads in the team and can be used for interthread communication, however special care is required to avoid data races. In this example, the parallel directive creates a SPMD (single program, multiple data) computation where each thread executes the same code on different data items.

In addition to providing an interface to expose concurrency, OpenMP also supports directives for workload distribution between threads within a team. Specifically, OpenMP supports different forms of worksharing: (1) loop, (2) sections, and (3) tasks, which we explain next.

Loops are often the hotspots in a program, and are therefore prime candidates for optimization and parallelization. The loop worksharing directive omp parallel for distributes loop iterations across all threads in a team (Fig. 6.6) as follows:

```
int A[N];
#pragma omp parallel for
for (i = 0; i < N; i++) {
    A[i] = fn(i);
}
```

With the omp parallel for directive, the loop iteration space is divided by the number of threads available in the parallel region, and therefore iterations cannot have dependences between them. In many cases, output- and anti-dependences can be removed with techniques such as variable renaming, scalar expansion, node splitting, and induction variable substitution. Other techniques to remove dependences require complex data dependence analysis, code restructuring, e.g., reordering statements, to parallelize loops. OpenMP, however, supports parallelization of loops