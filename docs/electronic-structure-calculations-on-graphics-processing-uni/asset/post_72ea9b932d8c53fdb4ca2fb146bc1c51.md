
During the idle period, the CPU is reading wave functions from disk (routine wfs_read_disk in the "CPU routine markers" line). Performance of the code could, in principle, be improved by prefetching these wave functions before launching the cudaDeviceSynchronize call, which blocks the CPU for ~15 ms. Such an overlap between CPU and GPU work would be possible because there are no dependencies between the new wave function data fetched and the results calculated from preceding wave function data.

### 9.5.3 Results

Figure 9.5 shows the speedup for a test system Ni_72(0001) surface with 14 atoms in the unit cell. These results were obtained running on a system with two 6-core Intel X5650 CPUs and eight Nvidia C2075 GPUs. The speedup for a few representative functions is shown as black lines, and the total speedup is shown in red. As the number of u increases, the speedup of most functions plateaus. Some of them, such as zherk and our customized kernels ("paw_P_ai", "mapG", and so on), transform themselves from being memory-bound to being compute/latency-bound: the number of kernel launches is reduced, reducing the kernel launch overhead, and the cudaMemcpy is executed with a larger amount of data per copy. For large N_u, the FFT operations, employed by calling the CUFFT library in a batched manner, gain the least speedup (12), compared to FFTW. This is not surprising since FFT operations are highly nonlocalized. The CUBLAS zherk routine gains a speedup of 27 compared to MKL BLAS. The maximum speedup of 36 for zherk is not achieved here because we did not choose a large enough system to stress the GPUs; instead we chose a system that was more scientifically interesting. Our own customized kernels "mapG" and "paw_P_ai" gain the most significant speedup by parallelizing over as many indices as possible using GPU threads. For example, in the

![](img/255d48531d66773aa863436a333dac7d_235_0.png)

Figure 9.5 Speedup (eight GPUs vs. eight CPU cores) as a function of the number of u (N_u) for some representative functions such as get wave functions ("get_wfs"), mapping wave functions between the 3D FFT grid and reduced plane wave grid ("mapG"), PAW corrections ("paw_P_ai"), batched CUFFT ("fft"), and CUBLAS ("zherk" routine). For a full list of the GPU ported functions, refer to Ref. [49]. The test system is a Ni_72(0001) surface, modeled with four layers of Ru in a sqrt(3) × sqrt(3) unit cell. The speedup (timing) information comes from a summation of 1 k-point (per core), 5 occupied, and 1486 unoccupied bands with an energy cutoff 150 eV. The total speedups ("Total") in the optical limit (q → 0) and other q ≠ 0 are also shown.

**Table 9.3** Speedup (eight GPUs/eight CPU cores) for q ≠ 0 as well as time required for an entire RPA calculation with a response function cutoff of 150 eV for different simulations

| System | Phase | N_a | N_e | Spin | k-Points | Speedup | t_gpu |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| O2 | Gas | 2 | 12 | True | 1 | 11.3x | 41 seconds |
| Li2O | Bulk | 3 | 8 | False | 4 × 4 × 4 | 10.5x | 63 seconds |
| MoO3 | Bulk | 16 | 96 | False | 4 × 2 × 4 | 35.3x | 1.0 hour |
| N2/Ru(0001) | Surface | 14 | 202 | False | 4 × 4 × 1 | 36.1x | 1.4 hours |
| CO/Ni(111) | Surface | 22 | 210 | True | 4 × 4 × 1 | 37.0x | 5.5 hours |

N_a denotes the number of atoms and N_e the number of electrons in the unit cell. Spin polarization is indicated in the column “Spin.”

CPU code, the PAW corrections must loop over atoms, bands, and projector functions. In the GPU implementation, we parallelize all the atoms, bands, and projector function indices simultaneously using threads.

With a typical speedup of 40, RPA calculations can be performed in a timely manner using eight GPUs on the systems shown in Table 9.3. The speedup in the noninteracting response function makes it also applicable to other beyond-DFT methods such as GW and Bethe–Salpeter equation [51].

## 9.6 Summary and Outlook

The PAW method together with uniform real-space grids as implemented in the open-source software package GPAW has proven to be an accurate and scalable computational method for DFT-based calculations on traditional CPU-based supercomputers. As GPUs have been promising in speeding up DFT-based calculations, we have ported GPAW to utilize also GPUs.

The ground-state algorithm in GPAW contains several parts with non-negligible computation time including solution of the Poisson equation with the multigrid method, projector function–wave function integrals, application of the Hamiltonian operator to the wave functions, multigrid preconditioning and dense matrix–matrix products in subspace diagonalization, and orthonormalization of wave functions. All these parts can be executed on GPUs either with custom CUDA kernels or with the CUBLAS library. Multiple GPUs can be utilized on the MPI-based implementation. We have implemented also hybrid versions of special matrix–matrix operations, which can utilize concurrently both CPUs and GPUs. In single CPU core–GPU comparison, the individual computational kernels achieve speedups of a factor of 10–40, and the whole calculation can obtain speedups up to ~20. Also, we have demonstrated that the multi-GPU ground-state algorithm scales efficiently at least to 256 GPUs. In typical hardware configurations, there are several CPU cores available per GPU, and in a CPU node–GPU node comparison the speedup for the full calculation is typically 3–4. This speedup is significant and justifies the use of GPUs when considering acquisition price versus performance or energy consumption versus performance.

GPAW implements also TD-DFT for studies of excited state properties. As the TD-DFT real-time propagation algorithm utilizes largely the same kernels as the ground-state algorithm, the GPU-based implementation is relatively straightforward based on the existing ground-state GPU implementation. The achievable speedup and scalability of TD-DFT calculations is similar to those of ground-state calculations.

For special GPAW features, it is possible to obtain very high speedups with GPUs. The RPA to the correlation energy is computationally very demanding, and the algorithm itself is well suited for GPUs. The RPA GPU implementation is also able to utilize multiple GPUs and achieves speedups of almost 40 in single CPU core–single GPU comparison.

Generally, DFT-based methods contain several time-consuming computational kernels whose optimization for GPUs is nontrivial. Thus, it is expected that there is room for further improvements in the GPU implementation of GPAW. In addition, hardware developments (e.g., caches in GPUs) as well as developments in the compilers are likely to improve the performance of GPU implementations, and make it also easier to implement new features utilizing GPUs. Even though GPUs might not become mainstream for DFT-based simulations, there are clearly application cases where GPUs are highly competitive.

## Acknowledgments

This work has been supported by the Academy of Finland (Project 110013 and the Center of Excellence program). This research used resources of CSC-IT Center for Science Ltd., Finland, and PRACE Research Infrastructure resource CURIE based in France at GENCI/CEA. Work on the RPA method was supported by the U.S. Department of Energy Chemical Sciences, Geosciences, and Biosciences Division under the Materials Genome Initiative: Predictive Theory of Transition Metal Oxide Catalysis grant.

## References

- 1. Hohenberg, P. and Kohn, W. (1964) Inhomogeneous electron gas. *Phys. Rev.*, **136** (3B), B864–B871.
- 2. Kohn, W. and Sham, L.J. (1965) Self-consistent equations including exchange and correlation effects. *Phys. Rev.*, **140** (4A), A1133–A1138.
- 3. Mortensen, J.J., Hansen, L.B. and Jacobsen, K.W. (2005) Real-space grid implementation of the projector augmented wave method. *Phys. Rev. B*, **71**, 035109.
- 4. Enkovaara, J., Rostgaard, C., Mortensen, J.J., Chen, J., Dulak, M., Ferrighi, L. *et al.* (2010) Electronic structure calculations with GPAW: a real-space implementation of the projector augmented-wave method. *J. Phys: Condens. Matter*, **22** (25), 253202.
- 5. Payne, M.C., Teter, M.P., Allan, D.C., Arias, T.A. and Joannopoulos, J.D. (1992) Iterative minimization techniques for ab initio total-energy calculations: molecular dynamics and conjugate gradients. *Rev. Mod. Phys.*, **64** (4), 1045–1096.
- 6. Gonze, X., Beuken, J.M., Caracas, R., Detraux, F., Fuchs, M., Rignanese, G.M. *et al.* (2002) First-principle computation of material properties: the ABINIT software project. *Comput. Mater. Sci.*, **25**, 478.
- 7. Kresse, G. and Furthmüller, J. (1996) Efficiency of Ab-initio total energy calculations for metals and semiconductors using a plane-wave basis set. *Comput. Mater. Sci.*, **6**, 15–50.
- 8. Giannozzi, P., Baroni, S., Bonini, N., Calandra, M., Car, R., Cavazzoni, C. *et al.* (2009) QUANTUM ESPRESSO: a modular and open-source software project for quantum simulations of materials. *J. Phys. Condens. Matter*, **21** (39), 395502 (19pp). Available from `http://www.quantum-espresso.org`.
- 9. Soler, J.M., Artacho, E., Gale, J.D., García, A., Junquera, J., Ordejón, P. *et al.* (2002) The SIESTA method for Ab initio order-N materials simulation. *J. Phys. Condens. Matter*, **14** (11), 2745.
- 10. Ahlrichs, R., Bär, M., Häser, M., Horn, H. and Kölmel, C. (1989) Electronic structure calculations on workstation computers: the program system Turbomole. *Chem. Phys. Lett.*, **162** (3), 165–169.
- 11. Chelikowsky, J.R., Troullier, N. and Saad, Y. (1994) Finite-difference-pseudopotential method: electronic structure calculations without a basis. *Phys. Rev. Lett.*, **72** (8), 1240–1243.
