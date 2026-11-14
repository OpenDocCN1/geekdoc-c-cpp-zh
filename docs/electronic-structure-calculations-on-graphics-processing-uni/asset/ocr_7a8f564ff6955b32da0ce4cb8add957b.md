# ## 9.2 General Overview

In this section we provide a short overview of the PAW method and discuss its implementation with uniform real-space grids. We also present an overview of one of the key algorithms in our real-space implementation, the multigrid method, which is used in the solution of the Poisson equation and in the preconditioning of the Kohn-Sham eigenproblem. More detailed descriptions of the underlying formalism and its implementation can be found in the original references of the PAW method [18] and the GPAW implementation [3, 4]. Atomic units ($\hbar = m = e = \frac{1}{4\pi\epsilon_0} = 1$) are used throughout the chapter.

# ### 9.2.1 Projector-Augmented Wave Method

The Kohn-Sham equations describe the core and valence electrons on equal footing. However, chemical environments affect mostly the valence electrons, and the core electrons remain in their atomic configuration. Thus, for many physical properties it is sufficient to solve the equations explicitly only for valence electrons. Because of the strong Coulomb interaction, the single-particle valence wave functions vary strongly near the atomic nuclei. The PAW method provides a rigorous formalism for working with smooth pseudo-valence wave functions, so that the resulting equations can be discretized more easily, for example, with plane waves (see Chapter 7) or uniform real-space grids (see also Chapter 10).

At the heart of the PAW formalism is a linear transformation between the AE wave function $\psi_n$ and the smooth valence pseudo (PS) wave function $\tilde{\psi}_n$:

$\psi_n(\mathbf{r}) = \hat{\mathcal{T}}\tilde{\psi}_n(\mathbf{r}),$ (9.1)

where $n$ is the electronic state index. The transformation operator $\hat{\mathcal{T}}$ is constructed in a manner such that the AE wave functions are orthogonal to the core wave functions $\phi_i^{\text{core}}$, which are fixed to their reference shape in the isolated atom.

The transformation operator $\hat{\mathcal{T}}$ is defined in terms of atom-centered AE partial waves $\phi_i^l(\mathbf{r})$, the corresponding smooth partial waves $\tilde{\phi}_i^l(\mathbf{r})$, and projector functions $\tilde{p}^l(\mathbf{r})$ as

$\hat{\mathcal{T}} = 1 + \sum_a \sum_l (|\phi^l\rangle - |\tilde{\phi}^l\rangle)\langle\tilde{p}^l|,$ (9.2)

where atom $a$ is at the position $\mathbf{R}^a$. The atom-centered AE partial waves and smooth PS partial waves are equal outside the atom-centered augmentation spheres of radii $r_c^l$:

$\phi_i^l(\mathbf{r}) = \tilde{\phi}_i^l(\mathbf{r}), |\mathbf{r} - \mathbf{R}^a| > r_c^l.$ (9.3)

The projector functions are localized inside the augmentation spheres and are orthogonal to the PS partial waves:

$\langle \tilde{p}_i^l | \tilde{\phi}_{i'}^{l'} \rangle = \delta_{i,i'}.$ (9.4)

The projectors and partial waves are constructed from an AE calculation for a spherically symmetric atom, and the index $i$ in Eq. (9.2) refers to the principal and angular momentum quantum numbers in an isolated atom. Given a complete set of atom-centered partial waves and projectors, the PAW transformation is exact. In practical calculations, two functions per angular momentum is typically enough.