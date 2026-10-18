# MULTICORE AND MANY-CORE ARCHITECTURES FOR QUANTUM SIMULATIONS

Multicore and many-core processors are all similar. They consist of a number of cores. Each core typically has its own L1 caches, and may have its own L2 cache or may share that cache with another core. Multicore processors usually have an additional shared L3 cache, while many-core processors do not.

The cores are connected by some form of network. Memory is also connected to that network. This often leads to a nonuniform memory architecture (NUMA) in which some memory is closer to a given core than other memory. Multi-socket systems always have NUMA characteristics.

Since access to cache is many times faster than access to main memory, it is important to optimize algorithms so that they reuse data from cache as much as possible. Many ES applications have already done this sort of optimization. This also helps to mitigate any issues caused by the NUMA architecture.

Each core has two or more hardware threads, which share the core’s resources but have their own register states and other internal state. Using hardware threads is a good way to hide memory latency; one thread can compute while another thread is waiting for a memory operation to complete. When the memory result is available the hardware will execute the waiting thread.

Cores also have SIMD (aka vector) units, enabling them to operate on several integer or floating-point numbers at the same time. Compilers will usually automatically vectorize innermost loops (e.g., over N_G). The user can assist with directives and by assuring that data are properly aligned and padded to fit the SIMD width.

Intel provides optimized FFT and BLAS libraries that are tuned for multicore and many-core architectures, so, in many cases, the application writer will find that much of the work has already been done.

# OpenMP 4.0 AFFINITY AND HOT TEAMS OF INTEL OpenMP RUNTIME

A node contains multiple parallel units—multiple cores, multiple sockets, multiple hardware threads, and optionally coprocessors. The ability to bind OpenMP threads to physical processing units has become increasingly important to achieve high performance on these modern CPUs. OpenMP 4.0 affinity features provide standard ways to control thread affinity that can have a dramatic performance effect. This impact is especially true on current generation Intel Xeon Phi processors: four hardware threads share the L1/L2 cache of an in-order core. We use OpenMP runtime environments to optimally bind MPI tasks and OpenMP threads. For instance, when using 5 MPI and 12 OpenMP threads for the band loop and 4 OpenMP threads for compute, they are set as

```
export OMP_NESTED=true
export OMP_NUM_THREADS=12,4
export OMP_PLACES=threads
export OMP_PROC_BIND=spread,close
mpirun -np 5 ./myapp
```

By default, Intel MPI runtime will partition the 5 MPI ranks over 60 cores so that each MPI task is allocated 12 cores. The OpenMP 4.0 affinity environment variables, OMP_PLACES and OMP_PROC_BIND, are set to bind one top-level thread per core and to bind four second-level threads (including the single top-level thread) to the hardware threads on the core.