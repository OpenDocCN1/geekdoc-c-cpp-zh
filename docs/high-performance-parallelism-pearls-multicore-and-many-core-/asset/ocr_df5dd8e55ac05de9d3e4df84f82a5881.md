![](bbox=[0.133, 0.117, 0.887, 0.356])

(a)                                                (b)

**FIGURE 18.11**
On E5-2697, (a) the throughputs (number of FFT transforms per second) normalized by those at 2 MPI tasks and 14 OpenMP, while using `MKL_NUM_THREADS=1`. (b) Strong scaling of FFT of $N_{FFT}=N^3$ with respect to `MKL_NUM_THREADS`. The number of MPI tasks is fixed at 2.

use modes. Now, we turn our attention to user codes and discuss how we can apply similar techniques to boost their performance.

We use the 3D diffusion code (referenced below) as a prototype. The stencil operations on a regular 3D grid of the diffusion code are representative of the class of computations performed by `compute_r` in the ES codes. We will skip the discussion of the performance of hybrid MPI/OpenMP of a user kernel at the band level, since there are no special properties of these kernels that will prevent the same parallel performance with any distribution of the bands over MPI and OpenMP. The performance of the nested OpenMP is predictable when this kernel is called within the band loop.

A more interesting scenario we will consider is when this user code is used at the same level of the band loop as shown in Figure 18.12. This is the realistic use case. For instance, the computations of Coulomb interactions between the electrons and ions in the ES codes use the charge density, $\rho(\mathbf{r})=\sum_k w_k\sum_i|\psi_i^k(\mathbf{r})|^2$, that is computed in the preceding loop over the bands.

Amdahl’s scaling law states that the speedup of parallel computing is limited by the sequential fraction of the program and we need to make sure the user codes (e.g., `diffusion`) do not limit the performance of the applications.

The diffusion code used in our experiments has been already parallelized by OpenMP and several optimizations were made to achieve high performance on Intel Xeon Phi coprocessors as discussed in Chapter 5 in *High Performance Parallelism Pearls (HPPP)*, ©2015, James Reinders and Jim Jeffers, Morgan Kaufmann Publications. We use the tiled version of the diffusion code in Figure 5.3 (p. 91) in HPPP as the reference. We recommend the readers to review the step-by-step improvement in the diffusion code through padding, cache blocking, and peeling as detailed by Dempsey. Finally, `collapse(2)` is used to extract enough parallelism after the blocking and `pragma vector nontemporal` to increase streaming storage bandwidth. All these resulted in 10× speedup over the basic OpenMP code which is included in `diffusion.c`.