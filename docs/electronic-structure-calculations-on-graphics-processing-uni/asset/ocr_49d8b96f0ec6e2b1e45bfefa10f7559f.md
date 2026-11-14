# Table 7.3 Self-consistent electron density calculation of bulk Si with a supercell of 512 atoms using block Davidson diagonalization (Nion = 512, Nband = 1284, Npw = 864,000)

| CPU cores/GPUs | 1/0 | 1/1 | x | 8/0 | 8/1 | x | 16/0 | 16/2 | x |
|---|---|---|---|---|---|---|---|---|---|
| Fourier | 7,307.6 | 589.0 | 12.4 | 1,199.7 | 527.3 | 2.3 | 770.9 | 246.4 | 3.1 |
| Projection | 4,437.5 | 142.8 | 31.1 | 604.9 | 151.1 | 4.0 | 428.8 | 90.6 | 4.7 |
| K and V | 853.1 | 43.6 | 19.6 | 144.3 | 41.3 | 3.5 | 124.7 | 19.1 | 6.5 |
| Nonlocal | 34.7 | 34.8 | 1.0 | 5.6 | 9.0 | 0.6 | 4.3 | 8.8 | 0.5 |
| Sub diag | 34,050.8 | 542.7 | 62.7 | 3,958.2 | 432.4 | 9.2 | 1,779.5 | 260.8 | 6.8 |
| p-sum | 46.3 | 2.5 | 18.5 | 7.0 | 1.8 | 3.9 | 5.0 | 1.0 | 5.0 |
| Other | 418.2 | 275.5 | 1.5 | 369.8 | 379.3 | 1.0 | 237.2 | 351.1 | 0.7 |
| Total | 47,148.1 | 1,630.9 | 28.9 | 6,289.6 | 1,542.2 | 4.1 | 3,350.5 | 977.8 | 3.4 |

Times in seconds, GPU speedup denoted by x.

# Table 7.4 Self-consistent electron density calculation of bulk Si with a supercell of 256 atoms using RMM-DIIS diagonalization (Nion = 256, Nband = 644, Npw = 432,000)

| CPU cores/GPUs | 1/0 | 1/1 | x | 8/0 | 8/1 | x | 16/0 | 16/2 | x |
|---|---|---|---|---|---|---|---|---|---|
| Fourier | 10,760.5 | 1,001.3 | 10.7 | 1,692.6 | 611.1 | 2.8 | 1,182.0 | 284.7 | 4.2 |
| Projection | 4,487.8 | 201.6 | 22.3 | 722.6 | 215.5 | 3.4 | 552.2 | 107.1 | 5.2 |
| K and V | 2,448.8 | 107.7 | 22.7 | 401.9 | 294.6 | 1.0 | 252.2 | 159.6 | 2.0 |
| Nonlocal | 81.8 | 59.1 | 1.4 | 11.5 | 36.7 | 0.3 | 27.7 | 19.0 | 0.4 |
| Sub diag | 10,619.1 | 507.7 | 20.9 | 1,596.0 | 747.0 | 2.1 | 1,059.2 | 438.8 | 2.4 |
| p-sum | 146.2 | 9.1 | 16.1 | 21.0 | 19.1 | 1.1 | 16.3 | 6.8 | 2.4 |
| Other | 734.2 | 568.8 | 1.3 | 473.3 | 635.8 | 0.7 | 236.9 | 469.2 | 0.5 |
| Total | 29,278.5 | 2,455.3 | 11.9 | 4,918.9 | 2,659.8 | 1.8 | 3,374.6 | 1,485.2 | 2.3 |

Times in seconds, GPU speedup denoted by x.

Switching from block Davidson to RMM-DIIS evens the distribution of costs between Fourier transforms and subspace diagonalization at 35% each. Projection remains the next largest cost at 15%, followed by the local action at around half that.

# 7.5.2.2 Single-Socket

For the 128-atom system, single-socket GPU acceleration is 2x. The subspace diagonalization, and local action steps are about 3x faster but the Fourier transforms only exhibit 40% improvement.

For the 256-atom system, single-socket performance with GPU improves to nearly 3x. The improvement can be attributed to two factors: the performance-relevant sections each exhibit improved performance and the overall effort in the calculation has shifted towards subspace diagonalization, which performs better on the GPU than the Fourier transforms. Larger problems will generally take greater advantage of the GPU both on a kernel by kernel basis and by spending more time in highly efficient dense linear algebra.

Single-socket RMM-DIIS GPU performance trails block Davidson with respect to both absolute time and the comparison to the CPU socket. The absolute time gap is around 5 min in favor of block Davidson, compared to 25 min in favor of RMM-DIIS on the CPU. The difference is mostly in the efficiency of the subspace diagonalization. The larger subspace problems in block Davidson do a better