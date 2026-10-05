# 5.2. Optimizing OpenMP programs

powers of 2 are likely to map to the same sets in L1 and L2 cache and create a lot of
cache conflicts. This problem may be tackled using the bit-reversed permutation as
explained in chapter 2.

Suppose the data is 2D and arranged in an $M 	imes N$ matrix:

```
$$\begin{pmatrix} a_{0,0} & a_{0,1} & a_{0,2} & \dots \ a_{1,0} & a_{1,1} & a_{1,2} & \dots \ a_{2,0} & a_{2,1} & a_{2,2} & \dots \ \vdots & \vdots & \vdots & \ddots \end{pmatrix}_{M 	imes N}$
```

The 2D FFT of this matrix is obtained by applying an FFT of size $M$ to every column
followed by an application of an FFT of size $N$ to every row. The structure of the
algorithm is similar to the recursive decomposition of a 1D FFT of size $MN$ into
FFTs of size $M$ and $N$, but there are no twiddle factors this time. The 2D structure
is imposed by the data but not by the algorithm.

If the data is in column-major order, the application of 1D FFTs of size $M$ to
columns involves no new point. However, the rows are different. If $M$ is a large power
of2, for example, the successive entries in a row are separated by a large power of 2
in memory, increasing the risk of cache conflicts. Thus, it is not a good idea to apply
1D FFTs by row. It is better to directly invoke library functions for 2D FFT.

# Exercise 5.2.1. Suppose a large array to be reversed. What is the best way to split
the array between, that most of the entries that are accessed in near memory?
Explain why the `init_manycore()` function would not be suitable for initializing entries.

# Exercise 5.2.2. Suppose a large array needs to be sorted. Would the `init_manycore()`
function be a good way to initialize the array to allocate pages in near memory?

# Exercise 5.2.3. Implement an in-place transformation of square matrices using OpenMP. Esti-
m the bandwidth to memory realized by your program.

# Exercise 5.2.4. Implement an out-of-place FFT for multiple threads (using library func-
t). Determine the speedup on a machine with multiple cores.

# Exercise 5.2.5. Refer to table 5.5 and determine that the fraction of the peak bandwidth
realized is 35% and 28%, respectively, for the 12-core 6.2 GHz SSE machine and the 16-core
2.2 GHz AVX machine (see table A.1 for information about these machines).