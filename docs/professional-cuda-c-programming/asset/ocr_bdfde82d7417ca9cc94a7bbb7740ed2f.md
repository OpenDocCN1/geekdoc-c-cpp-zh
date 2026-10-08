+   Tesla K10 Peak Memory Bandwidth:
2 GPUs/board * 256 bit * 2500 MHz mem-clock * 2 DDR / 8 bits/
byte = 320 GB/s
Ratio of instruction:bytes:
4.58 TFLOPS / 320 GB/s yields 13.6 instructions:1

For Tesla K10, if your application issues more than 13.6 instructions for every byte accessed, then your application is bound by arithmetic performance. Most HPC workloads are bound by memory bandwidth.

# ORGANIZING PARALLEL THREADS

You have seen from the preceding examples that if you organize threads using the right grid and block size, it can make a big impact on kernel performance. In the example of vector addition, you adjusted the block size for optimal performance, and the grid size was calculated based on the block size and the vector data size.

You are now going to examine this issue in more depth through a matrix addition example. For matrix operations, a natural approach is to use a layout that contains a 2D grid with 2D blocks to organize the threads in your kernel. You will see that a naive approach will not yield the best performance. You are going to learn more about grid and block heuristics using the following layouts for matrix addition:

+   2D grid with 2D blocks
1D grid with 1D blocks
2D grid with 1D blocks

# Indexing Matrices with Blocks and Threads

Typically, a matrix is stored in global memory with a row-major approach. Figure 2-9 illustrates a small case for an 8 x 6 matrix.

| Row 0 | Row 1 | Row 2 | Row 3 | Row 4 | Row 5 |
|---|---|---|---|---|\||

FIGURE 2-9