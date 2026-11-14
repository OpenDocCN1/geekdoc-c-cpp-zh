Table 5.3 CPU timings for a GPU-accelerated single-point DFT calculation on the budesonide molecule (C29H42O8) using a Becke-type grid, a TZ2P basis set, the GGA BLYP functional, and the frozen cores “small” setting in ADF.

| Integration grid accuracy | Total time | SCF cycle | Total focky | Numerical integration | Generate potentials | Other |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Computational cost in seconds** | | | | | | |
| Normal | 94.1 | 56.3 | 36.7 | 3.0 | 24.3 | 9.4 |
| Good | 170.7 | 86.3 | 67.7 | 6.7 | 49.0 | 12.0 |
| Very good | 375.7 | 194.5 | 170.6 | 14.7 | 132.5 | 23.4 |
| **Speed-up factor compared to CPU-only calculation** | | | | | | |
| Normal | 1.45 | 1.79 | 2.24 | | | |
| Good | 1.61 | 2.29 | 2.64 | | | |
| Very good | 1.89 | 2.80 | 3.04 | | | |

*The calculation was performed on 12 cores of the Intel Xeon E5-2620 CPU and a single Nvidia K40.*

# ## 5.3.4 Speed-Up Results for a Single-Point Calculation

Table 5.3 shows the results of the test calculations with GPU acceleration enabled, as well as the speedup when compared to the CPU timings from Table 5.1. The hybrid computing scheme clearly performs as planned, as almost no time is spent on numerical integration. The small part that remains is mostly the overhead of the wrapper routine handling the memory transfers.

We can now also estimate the minimum average speedup of the numerical integration: the 12 CPU cores needed 338.2 s (Table 5.1) to perform the numerical integration on the “very good” grid setting, where the K40 used at most 170.6 s to perform the calculation. This makes the K40 1.98 times faster when compared to 12 CPU cores, or 23.8 times faster when compared to a single core. If we compare this number to the K40 curve in Figure 4.2, knowing that the average block in the calculation has between 300 and 700 active basis functions, we can conclude that the HyperQ feature works and multiple blocks are computed concurrently on the device.

# ## 5.3.5 Speed-Up Results for an Analytical Frequency Calculation

A large part of the computational cost during an analytical frequency calculation is spent on numerical integration (see Section 5.2.2). These calculations can also be GPU-accelerated using a hybrid scheme similar to the one used for the Fock matrix formation by the SCF. The most expensive part is the numerical integration of derivative Fock matrix elements, Eq. (5.3), which can be performed with a slightly modified kernel that includes a loop over the geometric derivatives of the basis functions. This method was chosen for ease of implementation, but requires the GPU I/O perform 3 x (3N_at x N_ao^2) operations to calculate the full derivative Fock matrix. The CPU code uses an auxiliary matrix (Eq. (3.4)), and thus only needs SN_ao x N_oc + 2N_ao x N_oc operations to calculate the derivative Fock matrix:

```
$$A_{\mu\nu} = \sum_d Q_{\mu\nu} \phi_{\mu\nu,d}^*$$ (5.4)
```

Because the GPU code does not use the auxiliary matrix, it is less efficient when compared to the CPU code, meaning that we will only see good acceleration if the ratio of CPU cores to GPU devices is small. A calculation with two CPU cores and two GPUs (a K20 and a K40) will give an estimation of the speedup that could be obtained with a realistic production setup (6–8 cores per GPU), if the GPU kernel is rewritten to use an auxiliary matrix.