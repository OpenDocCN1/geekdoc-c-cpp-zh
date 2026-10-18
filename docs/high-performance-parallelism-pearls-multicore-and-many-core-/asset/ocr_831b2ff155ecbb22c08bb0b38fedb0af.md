# Sub-matrices in the blocked LU factorization algorithm
and two iterations of the algorithm

![](bbox=[0.28, 0.2, 0.72, 0.33])

# FIGURE 20.13

Blocked LU factorization data breakdown. The input matrix is viewed as a set of submatrices (blocks), which are updated one by one. There are three types of submatrices depending on their position in the input matrix: diagonal (D), perimeter (P), and inner (I) blocks. At each iteration, the input matrix shrinks down as elements at the diagonal and perimeter submatrices get their result values and these submatrices do not “participate” in the next iteration (in gray).

# CFD BENCHMARK

The CFD benchmark is an unstructured-grid finite-volume solver for the three-dimensional Euler equations with compressible flow. The CFD solver iteratively calculates fluxes and updates an array of structures (AoS) that contain density, density power, and momenta. The benchmark has three compute kernels; each of them contains a single OpenMP parallel loop.

After we put target pragmas to the OpenMP code, it ran about three times slower than the OpenCL code. In this case, the compiler does not vectorize the loop annotated with the OpenMP parallel for directive.

To enable compiler vectorization, we added one more loop over blocks as shown in Figure 20.14. With this, the OpenMP scheduler works at a coarser block level and at the same time each block gets vectorized within a thread. Such a transformation gave some performance boost but not enough to reach the OpenCL code performance.

Setting the MIC_USE_2MB_BUFFERS=64K environment variable to make the offload runtime allocate large pages for the OpenMP version does not improve the performance. At the same time, VTune Amplifier shows that the OpenMP code still has some potential vectorization improvements (see Figure 20.15a).

Here, we noticed that there is one big difference between the OpenCL and OpenMP implementation. The OpenCL version stored density, density power, and momentums data as a structure of arrays (SoA), while the OpenMP version stored the same data as an AoS.

While AoS allows writing code that is easy to understand and maintain, it does not lend itself well to data locality and SIMD execution. In contrast, SoA in the OpenCL implementation enables better locality and vectorization and, consequently, performance. Switching the OpenMP code to use SoA helps to reach better vectorization intensity, cache utilization (see Figure 20.15b), and to achieve the same performance as the OpenCL code.