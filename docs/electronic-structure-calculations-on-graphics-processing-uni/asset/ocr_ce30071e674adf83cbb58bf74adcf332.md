the Global Arrays toolkit [42, 43]. For all computations using these packages, seven of eight cores were dedicated to computations, while one was reserved as a communication helper thread. It has been shown that NWChem performs as well (and often significantly better) when one core is dedicated to communication [44]. The native PSI3 CCSD implementation and our own CPU code utilize shared-memory parallelism through threaded BLAS calls of the GotoBLAS2 library. For consistency, all computations with all packages were performed using C1 point-group symmetry.

# 13.5.2 Density-Fitted CCSD

The computations using our density-fitted CCSD algorithm were performed on a single workstation consisting of a 6-core Intel i7-3930K (3.20GHz) CPU with access to 64 GB RAM and either a single Nvidia Tesla K20 (Kepler) GPU or two Nvidia Tesla C2070 (Fermi) GPUs. The GPU-accelerated DF-CCSD algorithm was implemented in a development version of the PS4 electronic structure package [45]. All computations were performed within the frozen core approximation. For an analysis of the performance of the underlying DF-CCSD CPU implementation, the reader is directed to Ref. [35]. Again, all computations were performed using C1 point-group symmetry.

# 13.6 Results

# 13.6.1 Communication-Avoiding CCD

The performance of the low-communication GPU-CCD algorithm is compared to two well-known electronic structure packages in Table 13.1. We consider hydrocarbons with as many as 20 carbon atoms described by the modest 6-31G basis set. Timings correspond to only the iterative portions of the CCD algorithm. For the GPU implementation, the initial integral push to the device is excluded. Also, the CPU and GPU implementations of Ref. [3] do not involve any I/O-intensive processes such as the DIIS convergence acceleration. For Molpro and NWChem, the times corresponding to integral generation and sorting were excluded. The C2050 GPU-CCD algorithm consistently outperforms all other implementations on a per iteration basis.

Table 13.1 Comparison of CPU and GPU implementations of CCD

| Molecule | o | v | C2050 | X5550 | Molpro | NWChem |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| | | | Ref. [3] | | | |
| C8H10 | 21 | 63 | 0.3 | 1.3 | 2.3 | 5.1 |
| C10H8 | 24 | 72 | 0.5 | 2.5 | 4.8 | 10.6 |
| C10H12 | 26 | 78 | 0.8 | 3.5 | 7.1 | 16.2 |
| C12H14 | 31 | 93 | 2.0 | 10.0 | 17.6 | 42.0 |
| C14H10 | 33 | 99 | 2.7 | 13.9 | 29.1 | 59.5 |
| C14H16 | 36 | 108 | 2.5 | 21.6 | 41.5 | 93.2 |
| C16H16 | 40 | 120 | 8.8* | 40.3 | 103.0 | 166.3 |
| C18H18 | 41 | 123 | 10.5 | 50.2 | 83.3 | 190.8 |
| C18H12 | 42 | 126 | 12.7*# | 50.3 | 111.8 | 218.4 |
| C18H20 | 46 | 138 | 20.1*# | 86.6 | 157.4 | 372.1 |

Times doubly occupied and virtual orbitals are given in each row, respectively; the letters and represent the number
*The matrix-matrix multiplication involving (ac|bd) was tiled.
#Some two-electron integrals were pushed to the GPU every iteration.