# 4.2. Optimizing memory access

| Matrix Dimensions | b/w |
| 4 × 200 × 4 | 3.48 |
| 4 × 200 × 12 | 3.32 |
| 600 × 200 × 12 | 3.22 |
| 600 × 200 × 3000 | 3.21 |
| 3000 × 200 × 3000 | 3.19 |
| 9000 × 9000 × 9000 | 3.19 |

Table 4.7: Bandwidth in flops per cycle on a 2.6 GHz SSE2 machine for the multiplication of an $\ell \times m$ matrix with an $m \times n$ matrix. Matrix dimensions are reported as $\ell \times m \times n$.

We want the matrices to be big so that the arithmetic operations are far numerous than memory accesses, but the catch is that the matrices will not fit into cache when they are too big. One way to overcome this dilemma is to use block multiplication. We can pick the block sizes to be small enough to fit into cache large enough that the cost of loading from memory is outweighed by the cost of arithmetic operations. Careful blocking would indeed improve the simple programs of section 3.2.5 but not enough to get anywhere to peak bandwidth. A much more powerful set of ideas$^7$ shows how a program for multiplying matrices can approach the peak bandwidth for floating point arithmetic.

In outline, the basic idea remains to multiply in blocks, but intermediate blocks are stored in scratch space and in convenient formats to minimize TLB and cache misses. Far as possible, data is stored in a format that enables sequential access with stride. The actual execution of this idea can make it look more complicated than it is, but the idea is elegant as well as possibly applicable to many other problems.

As shown in 4.7, our implementation progresses systematically from the $4 \times 200 \times 4$ microkernel in section 3.3.4 to the multiplication of square matrices of dimension 9,000. We use a hierarchy of matrix multiplication functions with a function corresponding to each row of the table. Square matrices of dimension 9,000, which occurs at the last row, are too large to fit into cache cache misses. Limiting ourselves to matrices of specific dimensions keeps the exposition tractable.

The square matrices of dimension 9,000 at the bottom of table 4.7 are stored in column-major order. However, the storage format of the matrices in every other row

> $7Goto and van de Geijn (2008).