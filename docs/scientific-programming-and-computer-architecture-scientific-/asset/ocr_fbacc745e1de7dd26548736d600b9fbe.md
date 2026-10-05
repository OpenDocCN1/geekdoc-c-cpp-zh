# 5.2. Optimizing OpenMP programs

| Computer | # of Threads/Cores | N | bw |
|---|---|---||}{
| 2.6 GHz SSE2 | 12 | 64 | 0.35 (8) |
| | | 1024 | 0.29 (8) |
| | | 8192 | 0.33 (9) |
| 2.2 GHz AVX | 16 | 64 | 0.16 (7) |
| | | 1024 | 0.15 (12) |
| | | 8192 | 0.14 (13) |

Table 5.5: Bandwidth (more precisely, the inverse bandwidth) given as the number of cycles consumed by an FFT of size $N$ divided by $N \log_2 N$. The parenthesized numbers are speedups relative to a single core (for the full names of the machines, see Table A.1).

In chapter 2, we discussed the FFTW and MKL libraries and their interfaces to the 1D inverse DFT. We return to topic to make a few points about the FFT and its implementation.

Table 5.5 shows the number of cycles used by the FFT for various $N$ as a function of the number of threads. The speedups are quite good and reach 75% of linear speedup for some of the values of $N$. The numbers in the table were obtained by lining up complex numbers (or $2N$ double-precision numbers) in 16 GB of memory. The number of blocks is approximately $10^8/N$, and the FFT of each block was computed. The blocks were split between threads using OpenMP. Each thread applied MKL's 1D FFT to its share of the blocks.

# On 1D versus 2D FFT

Let us suppose that $N = 2n$. The basic idea of the radix-2 FFT is as follows.$^\superscript{4}$ First rearrange the data $a_0, a_1, \dots, a_{2n-1}$ as a $2 \times n$ matrix:

```
$$\left(egin{matrix} a_0 & a_2 & \dots & a_{2n-2} \ a_1 & a_3 & \dots & a_{2n-1} \end{matrix}\right)$
```

> ^4For the FFT algorithm see, van Loan (1992) and Cormen et al. (2001). The Wikipedia pages on the FFT and related topics have a wealth of information.