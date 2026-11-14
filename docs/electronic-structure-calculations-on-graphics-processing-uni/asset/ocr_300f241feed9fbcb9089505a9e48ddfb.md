where \(|g_i\rangle\) is the gradient of the total energy with respect to the wave function \(|\Psi_j\rangle\), of energy \(\epsilon_j\). The preconditioned gradient \(|\bar{g}_i\rangle\) is found by solving Eq. (6.12) by a preconditioned conjugate gradient method.

The complete Hamiltonian contains also the nonlocal part of the pseudopotential which, thanks to the orthogonality of Daubechies wavelets, can directly be applied in the compressed form. A schematic of all these operations is depicted in Figure 6.3.

# 6.2.3 Three-Dimensional Basis

For a 3D description, the simplest basis set is obtained by a set of products of equally spaced scaling functions on a grid of spacing \(h\):

\(\phi_{ijk}^h(\mathbf{r}) = \phi(x/h - i)\phi(y/h - j)\phi(z/h - k).\) (6.13)

In other words, the 3D basis functions are a tensor product of 1D basis functions. Note that we are using a cubic grid, where the grid spacing is the same in all directions, but the following description can be straightforwardly applied to general orthorhombic grids.

The basis set of Eq. (6.13) is equivalent to a mixed basis set of scaling functions on a twice coarser grid of grid spacing \(h = 2h\):

\(\phi_{ijk}^{h/2}(\mathbf{r}) = \phi(x/h - i)\phi(y/h - j)\phi(z/h - k)\) (6.14)

augmented by a set of seven wavelets

\(\phi_{ijk}^1(\mathbf{r}) = \psi(x/h - i)\phi(y/h - j)\phi(z/h - k),\)
\(\phi_{ijk}^2(\mathbf{r}) = \phi(x/h - i)\psi(y/h - j)\phi(z/h - k),\)
\(\phi_{ijk}^3(\mathbf{r}) = \psi(x/h - i)\psi(y/h - j)\phi(z/h - k),\)
\(\phi_{ijk}^4(\mathbf{r}) = \phi(x/h - i)\phi(y/h - j)\psi(z/h - k),\)
\(\phi_{ijk}^5(\mathbf{r}) = \psi(x/h - i)\phi(y/h - j)\psi(z/h - k),\)
\(\phi_{ijk}^6(\mathbf{r}) = \phi(x/h - i)\psi(y/h - j)\psi(z/h - k),\)
\(\phi_{ijk}^7(\mathbf{r}) = \psi(x/h - i)\psi(y/h - j)\psi(z/h - k).\) (6.15)

This equivalence follows from the fact that, from Eq. (6.3), every scaling function and wavelet on a coarse grid of spacing \(h'\) can be expressed as a linear combination of scaling functions at the fine grid level \(h'\), and vice versa.

A KS wave function \(\Psi(\mathbf{r})\) can thus be expanded in this basis:

\(\Psi(\mathbf{r}) = \sum_{l_1,j_2,k} c_{l_1,j_2,k}^0 \phi_{l_1,j_2,k}^0(\mathbf{r}) + \sum_{l_1,j_2,k} \sum_{w=1}^7 x_{l_1,j_2,k}^w \phi_{l_1,j_2,k}^w(\mathbf{r}).\) (6.16)

The sums over \(l_1, l_2, l_3 (j_1, j_2, j_3)\) run over all grid points where scaling functions (wavelets) are centered. These points are associated with regions of low and high resolution levels, respectively.

In a simulation domain, there are three categories of grid points: those that are closest to the atoms ("fine region") carry 1D (3D) scaling function and seven (3D) wavelets; those that are further from the atoms ("coarse region") carry only one scaling function, corresponding to a resolution which is half of that of the fine region; and those that are even further away ("empty region") carry neither scaling functions nor wavelets. To determine these regions of different resolution, we construct two spheres around each atom \(a\): a small one with radius \(R_a^I = \lambda^I \cdot r_c^a\), and a large one with radius \(R_a^O = \kappa^I \cdot r_c^a\) (\(R_a^O > R_a^I\)). The values of \(r_c^a\) and \(r_a^a\) are fixed for each atom type, whereas \(\lambda^I\) and \(\kappa^I\) can be specified