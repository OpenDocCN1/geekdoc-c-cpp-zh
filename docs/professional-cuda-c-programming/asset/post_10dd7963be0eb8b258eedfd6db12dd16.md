
# WHAT BANDWIDTH CAN A KERNEL ACHIEVE?

When analyzing kernel performance, it is important to focus on memory latency, the time to satisfy an individual memory request, and memory bandwidth, the rate at which device memory can be accessed by an SM, measured in bytes per time unit.

In the last section, you experimented with two methods for improving kernel performance:

- Hiding memory latency by maximizing the number of concurrently executing swaps, leading to better saturation of the bus by keeping more memory accesses in-flight.
- Maximizing memory efficiency by properly aligning and coalescing memory accesses.

However, sometimes a bad access pattern is inherent to the nature of the problem at hand. How good is enough for a kernel? What is the best achievable performance in suboptimal situations? In this section, you will use a matrix transpose example to learn how kernel bandwidth can be adjusted using various tuning techniques. You will see that with an inherently imperfect access pattern, there are still options in redesigning your kernel to achieve good performance.

## Memory Bandwidth

Most kernels are very sensitive to memory bandwidth, that is, they are memory bandwidth-bound. As a result, it is often important to focus on memory bandwidth metrics while tuning kernels. Bandwidth can be dramatically affected by how data in global memory is arranged, and how that data is accessed by a warp. There are two types of bandwidth:

- Theoretical bandwidth
- Effective bandwidth

Theoretical bandwidth is the absolute maximum bandwidth achievable with the hardware at hand. For a Fermi M2090 with ECC disabled, the peak theoretical device bandwidth is 177.6 GB/s. Effective bandwidth is the measured bandwidth that a kernel actually achieves, and is calculated using the following equation:

```
effective bandwidth (GB/s) = (bytes read+bytes written) × 10 / time elapsed
```

For example, for a copy of a 2048 × 2048 matrix containing 4-byte integers to the device, the effective bandwidth can be computed with the following formula:

```
effective bandwidth (GB/s) = 2048 × 4 × 2 × 10 / time elapsed
```

You will measure and tune the effective bandwidth of the matrix transpose kernel in the following section.

## Matrix Transpose Problem

Matrix transpose is a basic problem in linear algebra. While basic, it is used in many applications. Taking the transpose of a matrix exchanging each row with the corresponding column. Figure 4-23 illustrates a simple matrix and its transpose.

| 0 | 1 | 2 | 3 |
|---|---|---|---|
| 4 | 5 | 6 | 7 |
| 8 | 9 | 10 | 11 |

matrix

FIGURE 4-23

| 0 | 4 | 8 |
|---|---|---|
| 1 | 5 | 9 |
| 2 | 6 | 10 |
| 3 | 7 | 11 |

transposed

The following is a host-based implementation of an out-of-place transpose algorithm using single-precision-floating point. Suppose the matrix is stored in a 1D array. The transpose can be easily calculated by transforming array index values to reverse row and column coordinates.

```
void transposeHost(float *out, float *in, const int nx, const int ny) {
  for (int iy = 0; iy < ny; ++iy) {
    for (int ix = 0; ix < nx; ++ix) {
      out[ix*ny+iy] = in[iy*nx+ix];
    }
  }
}
```

There are two 1D arrays storing matrices in this function: The input matrix and the transposed matrix. The matrix dimensionality is defined as nx rows by ny columns. The result of transpose operation when implemented on a 1D array is illustrated in Figure 4-24.

**data layout of original matrix**

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 |
|---|---|---|---|---|---|---|---|---|---|---|---|

**data layout of transposed matrix**

| 0 | 4 | 8 | 1 | 5 | 9 | 2 | 6 | 10 | 3 | 7 | 11 |
|---|---|---|---|---|---|---|---|---|---|---|---|

FIGURE 4-24

Observing the input and output layouts, you will notice:

- **Reads**: accessed by rows in the original matrix; results in coalesced access.
- **Writes**: accessed by columns in the transposed matrix; results in strided access.

Strided access is the worst memory access pattern for performance on GPUs. However, it is unavoidable in matrix transpose operations. For the remainder of this section, you will focus on improving bandwidth utilization using two versions of the transpose kernel: one that reads by rows and writes by columns, and one that reads by columns and writes by rows.

Figure 4-25 illustrates the first approach, and Figure 4-26 illustrates the second approach. Can you predict the relative performance of these two implementations? If the L1 cache is disabled for loads these two implementations are theoretically identical. However, if L1 cache is enabled, the second implementation should demonstrate better performance. While the reads performed by column will be coalesced the write will be wasted by bytes not requested), bringing extra bytes into the L1 cache means that the next read may be serviced out cache rather than global memory. Because writes are not cached in L1, the example that writes by column does not benefit from any caching. On Kepler K10, K20, and K20x devices, there should be no difference in performance between these two approaches because the L1 cache is not used.
