The master now gathers different sections of the computed C matrix to assemble or produce the final result:

```
/* master gathers processed work*/
if (rank == 0) {
    for (i = 1; i < nprocs; i++) {
        /* receive lower bound from the worker */
        MPI_Recv(&lower_bound, 1, MPI_INT, i, STAG, MPI_COMM_WORLD, &status);
        //receive upper bound from a slave
        MPI_Recv(&upper_bound, 1, MPI_INT, i, STAG + 1, MPI_COMM_WORLD, &status);
        /* receive processed data from worker */
        MPI_Recv(&C[low_bound*n/2], (upper_bound - lower_bound) * nz, MPI_DOUBLE, i,
        STAG + 2, MPI_COMM_WORLD, &status);
    }
}
```

This implementation is not optimal, as it requires sending matrix B over the network for every worker. Given its importance, there has been considerable research on how to reduce communication bandwidth and increase parallelism for this problem, including using stencil distributed patterns and performing block matrix decompositions [15].

# 6.7 CACHE-BASED PROGRAM OPTIMIZATIONS

Despite considerable advances in computer architectures and in compilation techniques aimed at accelerating computations, often the bottleneck in performance lies in the relatively large latencies of memory and I/O, with data not arriving fast enough to the CPU to be processed at full computational rate. In this context, it is important to leverage the different types of memories available in the system, in particular to use as much as possible faster memories or caches. Because data is transferred transparently (without manual intervention) between slower and faster memories, it is important to understand how they operate to make effective use of them.

Caches exploit the principle of locality. This principle takes into consideration two aspects. The first, temporal locality, states that individual memory locations once referenced are likely to be referenced again. The second, spatial locality, states that if a location is referenced, then it is likely that nearby locations will be referenced as well. Hence, whenever a data element or an instruction is sought, the system first verifies if it is in the cache, otherwise the system loads it automatically from the slower memories (e.g., RAM) to the faster memories (e.g., cache L3, L2, and L1), including data or instructions from nearby locations. The goal is to maximize the use of the cache (minimizing the number of cache misses), thus increasing the performance of the application.