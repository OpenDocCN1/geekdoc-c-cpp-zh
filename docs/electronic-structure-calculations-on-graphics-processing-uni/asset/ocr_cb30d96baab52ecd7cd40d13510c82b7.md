![](bbox=[0.22, 0.11, 0.48, 0.26])

| # f GPU added | 2 | 4 | 8 |
|---|---|---|---|
| Speedup (SU) | 5.5 | 9.8 | 11.6 |
| # MPI equiv. | 44 | 80 | 96 |
| Acceler. Eff. | 1 | 0.94 | 0.56 |

![](bbox=[0.52, 0.08, 0.85, 0.36])

Figure 6.8. (a) Speedup of the BigDFT code for a four-carbon-atom supercell (graphene) with 164 K-points. The calculation is performed with eight MPI processes on the CEA-DAM INTI machine, based on Westmere processors and Nvidia Fermi. For each run, the number of the equivalent MPI processes is indicated, given that the parallel efficiency of this run is 98%. Also, the efficiency of the GPU acceleration is presented.(b) Speedup of the same run on different hybrid architectures in combination with MPI runs

![](bbox=[0.25, 0.48, 0.82, 0.83])

Figure 6.9. Relative speedup of the hybrid DFT code with respect to the equivalent pure CPU run. Different runs for simulations of increasing system size have been performed on an Intel X5472 3 GHz (Harpertown) machine, with a Fermi GPU card