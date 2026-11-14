The MP2 method has been useful in the study of biochemistry, such as in the study of larger biomolecules [4] and the study of dispersion energy in protein folding [5]. It has also found use in the generation of force fields for metal-organic frameworks [6] and, more recently, in the study of interactions in organic photovoltaic materials [7]. Recently, the use of MP2 in extended systems [8] has yielded interesting results in the study of adsorption energies [9].

Several methods have been applied and developed to extend the applicability of MP2 to larger systems. In this chapter, we will be focusing on the resolution-of-the-identity (RI) methods, also known as RI [10–13]. However, several other successful methods have also been developed, including local-MP2 [14], Cholesky decomposition (CD) [15, 16], and divide-and-conquer (DC) methods [17, 18].

The RI approximation reduces the number of operations by at least an order of magnitude for a triple-zeta basis set calculation. In RI-MP2, a larger basis set entails a larger relative speedup [19]. Therefore, RI-MP2 enables both the study of larger systems and also a more accurate representation, as it allows treatments of larger basis sets. Several steps in this method are matrix-matrix multiplications, which allow for a facile translation into the single-instruction multiple-data (SIMD) calculation paradigm, and hence to be further accelerated with graphics processing units (GPUs).

We begin describing the Hartree-Fock (HF) ansatz (guess) by using the electronic Hamiltonian under the Born-Oppenheimer (BO) approximation [20]:

```
\hat{H}_{el} = -\frac{1}{2} \sum_i^N \nabla_i^2 - \sum_i^N \sum_{I=1}^M \frac{Z_I}{r_{iI}} + \sum_{i \neq j}^N \sum_{i > j}^N \frac{1}{r_{ij}}
= \sum_i^N \hat{h}_i + \sum_i^N \sum_{j > i}^N \frac{1}{r_{ij}}.
(12.1)
```

for a system with N electrons and M atoms, where \(\hat{h}_i = -\frac{1}{2}\nabla_i^2 - \sum_I \frac{Z_I}{r_{iI}}\).

The HF method approximates the wave function as a product of molecular orbitals (MOs) \(\phi_i\), which are wave functions for a single electron under a one-electron Hamiltonian, the Fock operator:

```
\(\hat{f}_i = \hat{h}_i + \sum_{j \neq i}^{N/2} [2\hat{J}_j - \hat{K}_j].\)
(12.2)
```

where \(\hat{J}\) and \(\hat{K}\) represent the Coulomb and exchange operators, respectively [21]. The associated HF equations \(\hat{f}_i \phi_i = \epsilon_i \phi_i\) yield a complete set of eigenfunctions. This set of equations is typically solved using the Roothaan-Hall self-consistent field eigenvalue equations. The method scales cubically with system size: \(\mathcal{O}(M^4)\) [22].

As mentioned above and in Chapter 3, post-HF methods are able to systematically recover the electronic energy. Multi-configurational methods are able to obtain the so-called static correlation, as the wave function ansatz requires more than a single Slater determinant to properly describe its ground state. Dynamic correlation arises from the instantaneous Coulombic repulsion. As HF is a mean-field, single-determinant method, it is unable to capture either of these terms. MP2 theory is able to obtain some of the dynamic correlation, which makes it an efficient method to obtain quantitative predictions for systems close to their equilibrium structures.

Perturbation theory methods partition the Hamiltonian \(\hat{H} = H_0 + V\). In MP2 theory, the electronic Hamiltonian is divided as

```
\(\hat{H} = \sum_i \hat{f}_i + \Phi.\)
(12.3)
```

where \(\Phi\) represents the perturbation potential:

```
\(\Phi = \hat{H} - \sum_i \hat{f}_i.\)
```