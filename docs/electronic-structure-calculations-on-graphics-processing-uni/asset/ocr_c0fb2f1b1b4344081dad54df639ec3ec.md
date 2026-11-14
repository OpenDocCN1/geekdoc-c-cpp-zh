# 3.3 Density Functional Theory

The roots of DFT [15, 16, 37–40] can be traced back to work by Thomas and Fermi in the late 1920s who used models for the electronic structure of atoms that depend only on the electron density [41, 42]. Similarly, the Hartree–Fock–Slater or Xr method [43] replaces the nonlocal, orbital-dependent exchange term of the Hartree–Fock method by the appropriately local exchange potential of Dirac [44], which is very simple and given by \(j^{1/3}\). The basis for modern DFT, however, is the Hohenberg–Kohn theorems [45], later generalized by Levy, which prove that all properties of a many-electron system are functionals of the ground-state electron density. This means that, in place of solving the complicated many-electron Schrödinger equation, the ground-state energy can be obtained by minimizing the functional of the total electronic energy with respect to variations in the electron density. Unfortunately, this energy functional is not known, and it has proven difficult to develop functionals of the electron density that are sufficiently accurate for practical applications. This holds, in particular, for the density functional of the kinetic energy, a problem that already plagued the Thomas–Fermi approach. Thus, while the Hohenberg–Kohn theorems give a sound justification for DFT, the importance of this theory would not have risen above that of the Thomas–Fermi model if it was not for the work of Kohn and Sham.

# 3.3.1 Kohn–Sham Theory

Kohn and Sham had the ingenious idea to obtain the real, interacting electron density from an auxiliary system of noninteracting electrons with an electron density that is identical to that of the real system. The wave function for such a system of noninteracting electrons is a Slater determinant built from the eigenfunctions \(\psi_i\) of a single-particle Hamiltonian (similar to HF theory). In Kohn–Sham (KS) theory [46], the total electronic energy is given as

\(E[\rho] = T_s[\rho] + \int d\mathbf{r} \rho(\mathbf{r}) v_{\text{ext}}(\mathbf{r}) + \frac{1}{2} \int d\mathbf{r} \, d\mathbf{r}' \frac{\rho(\mathbf{r})\rho(\mathbf{r}')}{|\mathbf{r} - \mathbf{r}'|} + E_{\text{xc}}[\rho].\) (3.20)

where the various terms represent, in order, the kinetic energy of the KS system of noninteracting electrons, the interaction between the electrons and the external potential of nuclei and other fields, the Hartree energy arising from the Coulomb interaction of the electron density, and the remainder of the total energy, which is referred to as exchange-correlation (xc) energy \(E_{\text{xc}}\). The electron density is given in terms of the occupied orbitals

\(\rho(\mathbf{r}) = 2 \sum_i^{\text{occ}} |\psi_i(\mathbf{r})|^2,\) (3.21)

where, as before in the section on HF theory, we have assumed a closed-shell \(n\) electron system with \(n/2\) doubly occupied orbitals. The functional of the kinetic of noninteracting electrons is given as

\(T_s[\rho] = 2 \sum_i^{\text{occ}} \left\langle \psi_i \left| -\frac{1}{2} \nabla^2 \right| \psi_i \right\rangle.\) (3.22)

This noninteracting energy is different from the exact kinetic energy of the real system; however, it is a convenient and fairly good approximation. The remainder of the exact kinetic energy is taken into account as part of the xc energy \(E_{\text{xc}}\). Variational minimization of this total energy functional with respect to the electron density under the constraint that the orbitals remain orthonormal leads to the single-particle KS equations

\(\hat{h}^{\text{KS}} \psi_i = \epsilon_i \psi_i,\) (3.23)