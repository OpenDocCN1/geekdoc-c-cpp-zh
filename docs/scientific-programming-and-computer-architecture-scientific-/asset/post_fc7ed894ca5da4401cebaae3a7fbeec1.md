
# 312 Chapter 5. Threads and Shared Memory

frames. The same page of memory in either $a[]$ or $b[]$ may be accessed by more than one thread. In that case, whichever races to the page first gets a page clone to itself. If the two threads are on the same processor package, the page will be near both the threads.

## 5.2.4 Fast Fourier transform

For a purely arithmetic program, such as summing the Leibniz series, the speed of the program increases linearly with the number of cores, provided the number of terms summed is large enough to outweigh the overhead of entering and leaving OpenMP parallel region. Other tasks, such as transposing a matrix, are limited by bandwidth to memory. The bandwidth does not increase linearly with the number of cores employed. Many problems in scientific computing—finite differences or finite elements on a 3D mesh to give two examples—fall in the latter category.

Dense algebra problems, such as matrix multiplication, are limited by memory bandwidth in a straightforward way. In Chapter 3, we showed how to write a microkernel for matrix multiplication that takes advantage of parallelism in the instruction set. Chapter 4 showed how to cleverly hide the cost of accessing memory. A multithreaded matrix multiplication must account for cache memory slightly differently than the L3 cache is common to all the processor cores on the same package. Yet linear speedup with increasing processor cores can be achieved without drastic rethinking.

Hiding the cost of memory accesses and making efficient use of processor resources are essential for optimized FFT results as well. The inverse Fourier Transform (DFT) of the sequence $a_0, \dots, a_{N-1}$ is given by

```
$b_j = \sum_{k=0}^{N-1} \omega^{jk} a_k$
```

where $\omega = exp(2\pi i/N)$ is a primitive $Nth$ root of unity. This transformation is sometimes called the DFT, but we prefer to call it the inverse DFT to maintain an analogy with Fourier analysis. If the $a_j$ are discrete Fourier coefficients, we may think of $b_j$ as equispaced samples in the time domain. The FFT is a fast algorithm for computing the DFT or its inverse.

## 5.2. Optimizing OpenMP programs

| Computer | # of Threads/Cores | N | bw |
|---|---|---|---|
| 2.6 GHz SSE2 | 12 | 64 | 0.35 (8) |
| | | 1024 | 0.29 (8) |
| | | 8192 | 0.33 (9) |
| 2.2 GHz AVX | 16 | 64 | 0.16 (7) |
| | | 1024 | 0.15 (12) |
| | | 8192 | 0.14 (13) |

Table 5.5: Bandwidth (more precisely, the inverse bandwidth) given as the number of cycles consumed by an FFT of size $N$ divided by $N \log_2 N$. The parenthesized numbers are speedups relative to a single core (for the full names of the machines, see Table A.1).

In chapter 2, we discussed the FFTW and MKL libraries and their interfaces to the 1D inverse DFT. We return to topic to make a few points about the FFT and its implementation.

Table 5.5 shows the number of cycles used by the FFT for various $N$ as a function of the number of threads. The speedups are quite good and reach 75% of linear speedup for some of the values of $N$. The numbers in the table were obtained by lining up complex numbers (or $2N$ double-precision numbers) in 16 GB of memory. The number of blocks is approximately $10^8/N$, and the FFT of each block was computed. The blocks were split between threads using OpenMP. Each thread applied MKL's 1D FFT to its share of the blocks.

### On 1D versus 2D FFT

Let us suppose that $N = 2n$. The basic idea of the radix-2 FFT is as follows.$^4$ First rearrange the data $a_0, a_1, \dots, a_{2n-1}$ as a $2 \times n$ matrix:

$$\left(\begin{matrix} a_0 & a_2 & \dots & a_{2n-2} \\ a_1 & a_3 & \dots & a_{2n-1} \end{matrix}\right)$$

> ^4For the FFT algorithm see, van Loan (1992) and Cormen et al. (2001). The Wikipedia pages on the FFT and related topics have a wealth of information.

The original vector is recovered by reading this matrix in column-major order. The first step is to take the $n$-dimensional FFT of each row to get

$$\begin{pmatrix} \tilde{a}_0 & \tilde{a}_2 & \cdots & \tilde{a}_{2n-2} \\ \tilde{a}_1 & \tilde{a}_3 & & \tilde{a}_{2n-1} \end{pmatrix}$$

The next step is to multiply by the twiddle factors to get

$$\begin{pmatrix} \tilde{a}_0 & \tilde{a}_2 & \cdots & \tilde{a}_{2n-2} \\ \tilde{a}_1 & \omega\tilde{a}_3 & & \omega^{n-1}\tilde{a}_{2n-1} \end{pmatrix}$$

Here $\omega = exp(2\pi i/N)$. If this matrix is multiplied by

$$\begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix}$$

which is the 1D transform matrix with $N=2$, we will have the inverse DFT of the original matrix organized as a matrix in column-major format. The mathematical justification of this claim is omitted.

The $5N\log_2 N$ operation count of the FFT is obtained by recursive applications of the same idea, which is possible if $N$ is power of 2. An implementation that follows the resulting scheme will be quite inefficient, however. The scheme as it is presented will lead to a lot of cache conflicts.

The first decomposition, which we described in detail, thinks of a vector $a_i, 0 \le i < N$, as two vectors of length $N/2$. The two vectors are

$$a_i, a_{i+2}, a_{i+4}, a_{i+6}, \dots$$

with $i=0,1,\dots,N/2-1$. If we assume $N$ is power of 2 and go to a depth of $k$ in the recursion, we find that the FFT is breaking the given into $2^k$ vectors. The successive entries are given by$$a_i, a_{i+2^k}, a_{i+2\cdot2^k}, a_{i+3\cdot2^k}, \dots$$

for $i=0,1,\dots,2^k-1$. The successive entries of each of these vectors are separated by $2^k$ in memory, which are likely to map to the same sets in L1 and L2 cache and create a lot of cache conflicts.
