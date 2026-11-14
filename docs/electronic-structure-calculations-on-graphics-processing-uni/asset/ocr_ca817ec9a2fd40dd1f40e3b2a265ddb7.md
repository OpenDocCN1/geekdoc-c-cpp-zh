# ### 7.5.3.2 Single-Socket

The GPU implementation performs better in the non-self-consistent calculation than before. The GPU time is divided in similar proportions but the FFT, projection, and subspace diagonalization outperform their self-consistent counterparts. The kernels are parallelized over k-points, so that the difference is unlikely to have had an effect. The longer path to convergence likely increased the expansion set sizes, which therefore increased the size of the blocks and batches, improving occupancy.

# ### 7.5.3.3 Scaling

The scaling is very similar to the self-consistent case. FFTs scale very well, but communication in subspace diagonalization and other reduces the efficiency. The negative effects are somewhat lesser than in the self-consistent case; for the same reason, the single-socket performance is better: larger expansion set sizes improve the communication to computation ratios.

# ## 7.5.4 AIMD

Born-Oppenheimer MD is the classical movement of the ionic positions under forces derived from the quantum solution of the electron density. It consists of alternating electronic minimization and ionic motion steps, the former dominating the latter with respect to computational cost. To demonstrate the implementations on AIMD, we consider 64 atoms of bulk gold at 1600 K. One full ionic step is taken, using the RMM-DIIS diagonalizer for electronic minimization. The electronic minimization is performed using a 8 x 8 x 4 k-point grid, with the PBE functional [46]. The plane-wave cutoff energy was set at 229.6 eV. The results are given in Table 7.6.

# ### 7.5.4.1 Profile

Fourier transforms, subspace diagonalization, and projection are the dominant steps, taking 35%, 35%, and 15% of the runtime, respectively. The increase in importance of Fourier transforms and the associated decrease for subspace diagonalization are due to the use of the faster RMM-DIIS diagonalizer.

# ### 7.5.4.2 Single-Socket

Single-socket performance is 2X faster on the GPU than the CPU-only system. The Fourier transforms, projection, and local action all exhibit better performance than in silicon, which is significant

**Table 7.6** Ab-initio molecular dynamics of 64 gold atoms at 1600 K, seen in Figure 7.4 ($N_{band} = 64, N_{band} = 422, N_{pw} = 110, 592$)

| CPU cores/GPUs | 1/0 | 1/1 | x | 8/0 | 8/1 | x | 16/0 | 16/2 | x |
|---|---|---|---|---|---|---|---|---|---|
| Fourier | 2686.6 | 164.4 | 16.3 | 363.7 | 164.5 | 2.2 | 215.5 | 99.8 | 2.2 |
| Projection | 1160.1 | 77.9 | 14.9 | 211.6 | 53.6 | 4.0 | 141.3 | 42.8 | 3.3 |
| K and V | 604.4 | 37.5 | 16.1 | 89.3 | 22.2 | 4.0 | 63.3 | 14.8 | 4.3 |
| Nonlocal | 86.7 | 54.4 | 1.6 | 12 | 14.6 | 0.8 | 7.1 | 14.7 | 0.5 |
| Sub diag | 2495.6 | 208.9 | 12.0 | 433.9 | 160.7 | 2.7 | 312.1 | 120.1 | 2.6 |
| \(\rho\)-sum | 51.7 | 4.1 | 12.6 | 6.7 | 1.9 | 3.5 | 3.4 | 1.4 | 2.4 |
| Other | 191.1 | 163.4 | 1.2 | 99.6 | 173.8 | 0.6 | 65.3 | 164.8 | 0.4 |
| Total | 7278.4 | 710.6 | 10.2 | 1216.8 | 591.3 | 2.1 | 808.1 | 458.4 | 1.8 |

Calculation takes only one step and uses the RMM-DIIS diagonalizer.