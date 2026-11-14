bases, most commonly *linear combinations of atomic orbitals* (LCAO) [8], attempt to concisely represent the Hilbert space using physically motivated, atom-centered nonelectronic functions, for example, model solutions of the Schrödinger equation. Their primary advantages are their small size and sparse overlap, which facilitate the development of low-order methods. However, they run the risk of poorly representing unexpected processes in regions not covered by model solutions [9]. Grid bases are either in real or reciprocal space, systematically resolve the Hilbert space. Their primary advantage is their completeness. However, they are much larger than orbital bases and are often nonlocal. If the primary representation of wavefunctions is on a reciprocal grid, then the basis is referred to as *planewave* (PW).

Plane-wave density functional theory (PWDF) is one of the most popular schemes for performing electronic structure calculations of condensed matter systems. In PWDF, the kinetic energy operator is expressed as a diagonal matrix in plane-wave space (g-space), while the local potential is expressed as a diagonal matrix in real space (r-space). In most cases, pseudopotentials are used to smooth the wavefunctions near atom cores, reducing the required number of planewaves (g-vectors) at the cost of a low-rank nonlocal potential.

The combined r-space and g-space representation of the Hamiltonian necessitates the use of matrix-free solvers that rely on the action of the Hamiltonian on a vector \(|\phi\rangle\), \(H|\phi\rangle\), rather than the elements of the Hamiltonian, \(\langle r_i | H | r_j \rangle\) or \(\langle g_i | H | g_j \rangle\). In computing the action on a vector \(|\phi\rangle\), fast Fourier transforms (FFTs) are used to switch between r-space, \(\langle r | \phi \rangle\), and g-space, \(\langle g | \phi \rangle\), representations of the vector \(|\phi\rangle\). The nonlocal potential is defined on subspaces that, in realspace, do not grow with the overall system size. This makes the action of the Hamiltonian formally \(O(n \log n)\), instead of \(O(n^2)\) as for a general matrix. This is the key feature of the PWDF method.

Implementations of PWDF can be further categorized by the type or types of pseudopotentials that they employ. Modern pseudopotentials come in three popular varieties: norm-conserving pseudopotentials (NCPP) [10], ultra-soft pseudopotentials (USPP) [11, 12], and projector-augmented wave (PAW) [13]. NCPPs only add a dense low-rank term to the Hamiltonian, making them the simplest. USPPs significantly reduce the grid resolution necessary to converge the electron density, but require the introduction of a nontrivial overlap matrix, which generalizes the eigenproblem and adds charge density dependence to the nonlocal potential. PAW is a generalization of USPP to arbitrary projector forms, but is very similar in practice and provides only modest improvements to the rate of grid convergence.

There are many implementations of PWDF, including Quantum Espresso [14], VASP [15], CASTEP [16, 17], and Qbox [18, 19]. This chapter will draw examples from the GPU ports of VASP.

# 7.2 Theoretical Background

# 7.2.1 Self-Consistent Field

Kohn-Sham DFT is fundamentally an eigenproblem: \(\hat{H}\psi = \epsilon\psi\), where \(\hat{H}\) is the Hamiltonian operator, \(\psi\) is a single-particle wavefunction, and \(\epsilon\) is the energy eigenvalue of \(\psi\). In the pseudopotential framework, the Hamiltonian takes the form

```
\(\hat{H} = \hat{T} + \hat{v}^{loc} + \hat{v}^{nl},\) (7.1)
```

where \(\hat{T} = -\frac{1}{2}\nabla^2\) is the kinetic energy operator, \(\hat{v}^{nl}\) is the nonlocal potential, and \(\hat{v}^{loc}\) is the local potential due to both ion–electron and electron–electron interactions.