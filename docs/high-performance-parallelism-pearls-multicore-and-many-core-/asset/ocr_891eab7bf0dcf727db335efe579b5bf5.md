![](bbox=[0.21, 0.11, 0.78, 0.36])

# FIGURE 14.22

Bandwidth achieved with the pyMIC OffloadArray classes transfer functions.

# GPAW

The possible benefits of offloading depend on the overhead due to data transfers and the performance differences between the host and the coprocessor. One can make a simple performance model for the speed up obtainable from coprocessor as follows: assuming that the performance of host and coprocessor, P_h and P_c (GFLOPS), as well as the bandwidth between host and coprocessor, B (MB/s), do not depend on the size of the matrices, the times required for matrix-matrix operations in host T_h and in the coprocessor T_c are

```
T_h = a N_G N_b^2 / P_h   (14.17)
```

```
T_c = a N_G N_b^2 / P_c + b N_G N_b / B,   (14.18)
```

where a and b are constant prefactors. Thus, the cross over at which offloading becomes beneficial, that is, T_c < T_h, is directly proportional to the number of electronic bands N_b:

```
N_b > b P_h P_c / [a B (P_c - P_h)] .   (14.19)
```

In reality, all the performance parameters P_c, P_h, and B depend also on the size of the matrices, as seen in Figure 14.22, and the performance of the dgemm and zgemm operations. However, Eq. (14.19) shows that offloading is necessarily not beneficial in small systems (small number of atoms, small number electronic bands), but with increasing number of atoms/bands one should reach the maximum available speedup. As an example, Figure 14.23 shows the performance of subspace diagonalization Eq. (14.10) as a function of N_b with fixed N_g. It can be seen that offloading on the Taito cluster can speed up this part of the DFT algorithm up to factor of 4-5.