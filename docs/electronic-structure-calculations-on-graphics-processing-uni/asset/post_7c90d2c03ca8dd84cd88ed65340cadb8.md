
Here, P is the density matrix represented in the AO basis:

\( P_{\mu\nu} = \sum_i^C c_\mu^i c_\nu^i \) (4.15)

E is a diagonal matrix of MO energies (formally, this matrix is the set of Lagrange multipliers enforcing the constraint that all the molecular orbitals remain orthonormal, i.e., Eq. (4.8)); S is the AO overlap matrix

\( S_{\mu\nu} = \langle \phi_\mu | \phi_\nu \rangle \) (4.16)

and F(P) is the nonlinear Fock operator, defined slightly differently for HF and DFT as follows:

\( F_{\mu\nu}^{\text{HF}}(P) = h_{\mu\nu} + \sum_{\lambda\sigma}^N P_{\lambda\sigma} [2(\mu\nu|\sigma\lambda) - (\mu\lambda|\sigma\nu)] \), (4.17)

\( F_{\mu\nu}^{\text{DFT}}(P) = h_{\mu\nu} + 2 \sum_{\lambda\sigma}^N (\mu\nu|\sigma\lambda)P_{\lambda\sigma} + V_{\mu\nu}^{\text{XC}}, \) (4.18)

where h is the core Hamiltonian from Eq. (4.9) now in the AO basis:

\( h_{\mu\nu} = \left\langle \phi_\mu \left| \sum_a^A \frac{Z_a}{|\vec{r}_1 - \vec{R}_a|} - \frac{\nabla^2}{2} \right| \phi_\nu \right\rangle \) (4.19)

and the two-electron ERIs are defined in the AO basis as follows:

\( (\mu\nu|\lambda\sigma) = \int d^3\vec{r}_1 \int d^3\vec{r}_2 \frac{\phi_\mu^*(\vec{r}_1)\phi_\nu(\vec{r}_1)\phi_\lambda^*(\vec{r}_2)\phi_\sigma(\vec{r}_2)}{|\vec{r}_1 - \vec{r}_2|} \\
= \sum_{a \in \phi_\mu} \sum_{b \in \phi_\nu} \sum_{c \in \phi_\lambda} \sum_{d \in \phi_\sigma} c_{\mu a}^* c_{\nu b} c_{\lambda c}^* c_{\sigma d} \int d^3\vec{r}_1 \int d^3\vec{r}_2 \frac{\chi_a^*(\vec{r}_1)\chi_b(\vec{r}_1)\chi_c^*(\vec{r}_2)\chi_d(\vec{r}_2)}{|\vec{r}_1 - \vec{r}_2|} \\
= \sum_{a \in \phi_\mu} \sum_{b \in \phi_\nu} \sum_{c \in \phi_\lambda} \sum_{d \in \phi_\sigma} c_{\mu a}^* c_{\nu b} c_{\lambda c}^* c_{\sigma d} [ij|kl]. \) (4.20)

Note that we use round braces to refer to ERIs involving contracted basis functions and square braces to refer to primitive ERIs. Also, to specify that the \(i\)th primitive is restricted to members of the \(j\)th atomic orbital, we use the notation \(i \in \phi_j\). Finally, for DFT, \(V^{\text{XC}}\) is determined by functional differentiation of the exchange-correlation energy expression:

\( V_{\mu\nu}^{\text{XC}} = \left\langle \phi_\mu \left| \frac{\delta E_{\text{XC}}}{\delta \rho} \right| \phi_\nu \right\rangle. \) (4.21)

Because the HF and DFT operators are nonlinear, Eq. (4.14) cannot be solved in a closed form; instead, an iterative approach is used. Starting from some guess for the density matrix P, the Fock matrix is constructed and then diagonalized to obtain a matrix of approximate MO orbitals, C. The MO coefficients C are then used to construct an improved guess for the density matrix using Eq. (4.15), and the process is repeated until F and P converge to stable values.

### 4.1.2 Electron–Electron Repulsion Integral Evaluation

The generation and contraction of ERIs into the Fock matrix is the main bottleneck in finite-basis SCF algorithms, and therefore our primary focus in the present chapter. Here, we provide mathematical background which will be useful when considering the implementation of ERIs on GPUs in subsequent sections. Efficient ERI evaluation begins by invoking the Gaussian product theorem, which allows a product of two primitive Gaussian functions located at different centers to be combined into a single Gaussian centered at a point \(\overrightarrow{P}\) between the original centers [17]:

\(\Omega_{ij} = e^{-\alpha(\overrightarrow{r}-\overrightarrow{P}_i)^2} e^{-\alpha(\overrightarrow{r}-\overrightarrow{P}_j)^2} = K_{ij} e^{-\alpha(\overrightarrow{r}-\overrightarrow{P}_{ij})^2}, \\
\eta_{ij} = \alpha_i + \alpha_j, \\
K_{ij} = e^{-\frac{\alpha_i \alpha_j}{\alpha_i + \alpha_j} \overrightarrow{P}_{ij}^2}, \\
\overrightarrow{P}_{ij} = \frac{\alpha_i \overrightarrow{R}_i + \alpha_j \overrightarrow{R}_j}{\alpha_i + \alpha_j}.\)
(4.22)

This reduces each four-center primitive ERI to a simpler two-center problem:

\([(ij|kl] = [\Omega_{ij} | \Omega_{kl}].\)
(4.23)

Following the McMurchie-Davidson scheme for ERI evaluation, each primitive pair is exactly expanded in a basis of Hermite Gaussians [A] [13]:

\(\Omega_{[ij]} = \sum_{t=0}^{l_i+l_j} E_{ij}^{[t]} \Lambda_t.\)
(4.24)

The expansion coefficients \(E_{ij}^{[t]}\) differ for each primitive pair \(\chi, \chi\) and are calculated from simple recurrence relations [13]. The primitive ERI then becomes:

\([(ij|kl] = \sum_r \sum_q E_{ij}^{[r]} E_{kl}^{[q]} [\Lambda_r | \Lambda_q].\)
(4.25)

The Hermite ERIs \([\Lambda_r | \Lambda_q]\) are efficiently calculated by recurrence relations starting from the Boys function \(F_n(x)\) [13]:

\(F_n(x) = \int_0^1 t^{2n} e^{-xt^2} dt.\)
(4.26)

Although the Fock matrices of Eqs. (4.17) and (4.18) involve contributions from \(N^4\) ERIs, many individual terms may be neglected. Because each AO basis function is localized in space, a pair distribution \(\Omega_{ij}\) will approach zero exponentially as the distance between primitive functions increases. Thus, an AO ERI \([\mu\nu|\lambda\sigma]\) will be nonnegligible only if \(\mu\) is centered near \(\nu\) and \(\lambda\) is near \(\sigma\). For large systems, this reduces the number of integrals to a more manageable \(N^2\). In order to efficiently identify significant ERIs, a Schwarz inequality can be applied to either contracted or primitive integrals [18]:

\(|[\mu\nu|\lambda\sigma]| \le ([\mu\nu|\mu\nu])^{1/2} ([\lambda\sigma|\lambda\sigma])^{1/2}.\)
(4.27)

## 4.2 Hardware and CUDA Overview

While Chapter 2 provided an introduction to the concept of GPU programming, we believe it is useful to the reader to briefly repeat some of the essential points as they pertain to GPU acceleration of ERI evaluation. As mentioned previously, each GPU is a massively parallel device, containing thousands of execution cores. However, the performance of these processors relies not only from the raw width of execution units but also from a hierarchy of parallelism that forms the foundation of the hardware architecture and, in the case of Nvidia hardware, is ingeniously exposed to the programmer through the CUDA programming model [19]. Developers must understand and respect these hierarchical boundaries if their programs are to run efficiently on GPUs.

At the lowest level, the CUDA programmer writes a small procedure – called a kernel in “CUDA-speak” – that is to be executed by tens of thousands of individual threads in parallel. Although each CUDA thread is logically autonomous, the hardware does not execute each thread independently. Instead, instructions are scheduled for groups of 32 threads, called warps, in a single-instruction multiple-thread (SIMT) manner. Every thread in a warp executes the same instruction stream, with threads masked to null operations (no-ops) for instructions in which they do not participate.

Warps are grouped into larger blocks of up to 1024 threads. Blocks are assigned to local groups of execution units called streaming multiprocessors (SMs). The SM provides hardware-based intra-block synchronization methods, and a small on-chip shared memory is often used for intra-block communication. CUDA blocks can be indexed in one, two, or three dimensions at the convenience of the programmer.

At the highest level, blocks are organized into a CUDA grid. As with blocks, the grid can have up to three dimensions. In general, the grid contains many more blocks and threads than the GPU has physical execution units. When a grid is launched, a hardware scheduler streams CUDA blocks onto the processors. By breaking a task into fine-grained units of work, the GPU can be kept constantly busy, maximizing performance.

As highlighted in Chapter 2 in CUDA, the memory is also structured hierarchically. The host (CPU) memory usually provides the largest space, but can only be accessed through the PCIe interface, which suffers from latencies on the order of several thousand instruction cycles. The GPU’s main (global) memory provides several gigabytes of high-bandwidth memory capable of more than 250 GB/s of sustained throughput. In order to enable this bandwidth, global memory accesses incur long latencies, on the order of >500 clock cycles. Global memory operations are parallelized in a SIMT-friendly manner in which the natural width of the memory controller allows simultaneous access by all threads of a warp as long as those threads target contiguous memory locations. Low-latency, on-chip memory is also available. Most usefully, each block can use up to 64 KB of shared memory for intrablock communication, and each thread has up to 255 local registers in which to store intermediate results.

Consideration of the basic hardware design suggests the following basic strategies for maximizing the performance of GPU kernels:

- 1. Launch many threads, ideally one to two orders of magnitude more threads than the GPU has execution cores. For example, a Tesla K20 with 2496 cores may not reach peak performance until at least O(10^5) threads are launched. Having thousands of processors will be an advantage only if they are all saturated with work. All threads are hardware-scheduled, making them very lightweight to create, unlike host threads. Also, the streaming model ensures that the GPU will not execute more threads than it can efficiently schedule. Thus oversubscription will not throttle performance. Context switches are also instantaneous, and this is beneficial because they allow a processor to stay busy when it might otherwise be stalled, for example, waiting for a memory transaction to complete.
