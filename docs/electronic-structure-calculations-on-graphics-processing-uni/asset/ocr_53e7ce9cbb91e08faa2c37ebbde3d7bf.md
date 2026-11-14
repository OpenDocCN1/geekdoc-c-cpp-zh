In line with the definition of the Fock operator \(\hat{F}\) in Eq. (3.7), the Fock matrix elements are given as a sum of one-electron contributions (kinetic energy and external potential) and two-electron Coulomb and exchange contributions:

\(\mathbf{F} = \mathbf{h} + \mathbf{J} - \frac{1}{2}\mathbf{K}, \tag{3.12}\)

\(h_{\mu\nu} = \left\langle \mu \left| -\frac{1}{2}\nabla^2 + v_{\text{ext}} \right| \nu \right\rangle, \tag{3.13}\)

\(J_{\mu\nu} = \sum_{\kappa\lambda} P_{\kappa\lambda} (\mu\nu|\kappa\lambda), \tag{3.14}\)

\(K_{\mu\nu} = \sum_{\kappa\lambda} P_{\kappa\lambda} (\mu\kappa|\nu\lambda), \tag{3.15}\)

where

\(P_{\mu\nu} = 2 \sum_i^{\text{occ}} c_{\mu i} c_{\nu i} \tag{3.16}\)

are elements of the density matrix that can be used to express the electron density in terms of the basis functions

\(\rho(\mathbf{r}) = \sum_{\mu\nu} P_{\mu\nu} \phi_\mu(\mathbf{r}) \phi_\nu(\mathbf{r}). \tag{3.17}\)

The notation for the one-electron integrals and ERIs has been defined in Eqs. (3.4) and (3.5), but now the integrals are over basis functions and not MOs.

There are two major computational bottlenecks in HF calculations. These are the evaluation of the Fock matrix elements as defined in Eqs. (3.12)-(3.15), and solution of the SCF equations from Eq. (3.11). The latter requires diagonalization of the Fock matrix, which scales cubically with system size and eventually dominates the computational cost for very large calculations. In this case, alternative ways to solve the SCF equations that do not rely on matrix diagonalization must be employed [30, 31].

# 3.2.2 Two-Electron Repulsion Integrals

The computational cost for calculating the Fock matrix elements is dominated by the evaluation of the ERIs \((\mu\nu|\kappa\lambda)\), which are required for the Coulomb and exchange contributions, see Eqs. (3.14) and (3.15). The ERIs are four-index quantities

\((\mu\nu|\kappa\lambda) = \int d\mathbf{r}d\mathbf{r}' \frac{\phi_\mu(\mathbf{r})\phi_\nu(\mathbf{r})\phi_\kappa(\mathbf{r}')\phi_\lambda(\mathbf{r}')}{|\mathbf{r} - \mathbf{r}'|} \tag{3.18}\)

and formally there are \(O(N^4)\) ERIs that need to be evaluated during an HF calculation. Because of the sheer number of ERIs, storage in memory is not an option. Instead, so-called direct SCF methods recompute the ERIs during each iteration of the SCF cycle and contract them with the density matrix elements to directly obtain the corresponding Coulomb and exchange contributions to the Fock matrix [9–11].

For large, spatially extended systems, most of the ERIs are zero or negligible, which can be efficiently exploited to reduce the number of ERIs that have to be computed. This leads to an effective scaling of \(O(N^2)\) for most practical calculations. The reason for this asymptotic scaling with local, atom-centered basis sets consisting of Gaussian-type functions (GTFs), Slater-type functions (STFs), or numerical atomic orbitals is easy to understand. These basis functions decay to zero at large distances from their origin. As a consequence, an overlap density \(\rho_{\mu\nu} = \phi_\mu\phi_\nu\), that is, the product of two