We present benchmark calculations for matrices and quantum chemistry results for this method in the following section.

# 12.3 Performance of Accelerated RI-MP2

# 12.3.1 Matrix Benchmarks

As we are interested in accelerating quantum chemistry, the matrices calculated in RI-MP2 are of large size N and contain both large and small elements that are separated by orders of magnitude. Therefore, in the case of these methods, the heterogeneous approach seemed to be most effective to tackle mixed precision.

Our calculations were performed on an Intel Xeon E5472 (Harpetown) CPU clocked at 3.0 GHz and using an NVIDIA Tesla C1060 (packaged into a Tesla S1070). The GPU calls were limited to 256 MB of RAM to model a more restricted GPU in a typical BOINC (Berkeley Open Infrastructure for Network Computing) client [46–49].

We benchmark the heterogeneous MGEMM algorithm described in Section 12.2. Figure 12.2 shows the speedup of * GEMM calls on the GPU with respect to the size N of an N x N matrix, relative to the time taken for the corresponding DGEMM call on the CPU in serial.

In order to test the mixed-precision approach, we used matrices with random values in the range [–1, 1]. These were then “salted” with a fraction f_salt of values 2 orders of magnitude larger, in the range (90, 110). We tested three different salted fractions: f_salt = 10^-2, 10^-3, and 10^-4. The size of the cutoff parameter θ was chosen such that all the salted elements were considered “large”. All timings were averaged over 10 runs.

Running CUBLAS SGEMM is approximately 17.1 times faster than running DGEMM on the CPU for a matrix size 10,048 x 10,048. This represents an upper bound for the speedups we can hope to

![](bbox=[0.2, 0.52, 0.82, 0.83])

Figure 12.2 Speedup for various *GEMM calls as a function of matrix size. Most elements were in the range [–1, 1], with the “salt” values in the range [90, 110]. Times are scaled relative to running DGEMM on the CPU