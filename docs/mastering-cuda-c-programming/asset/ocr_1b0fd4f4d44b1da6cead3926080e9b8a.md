# Parallel Execution Model

Another core distinction between CUDA C and standard C is the parallel execution model. Standard C is designed primarily for sequential execution of code, with parallelism (when utilized) often managed through libraries or extensions like OpenMP. CUDA C, however, inherently relies on a parallel execution model, defining a hierarchical organization of thread groups as the basis for its computation:

Here, the computation is broken down into a grid of blocks, each containing a set of threads. This model not only enables massive parallelism but also requires a different programming mindset, focusing on dividing tasks among an extensive set of parallel execution units.