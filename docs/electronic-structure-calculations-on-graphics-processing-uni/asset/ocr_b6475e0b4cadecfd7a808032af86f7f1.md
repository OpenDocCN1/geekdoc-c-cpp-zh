# ## 3.4.4 Representations on a Numerical Grid

In place of localized basis functions on plane waves, electronic structure calculations can also employ real-space discretizations on a numerical grid [73–75]. In this case, physical quantities such as the orbitals and the electron density are explicitly represented via their numerical values at the grid points, while operators such as the Laplacian of the kinetic energy are approximated via finite differences. The simplest approach is to use uniform grids [74], while nonuniform grids can be employed to reduce the number of points in regions of space that require lower resolution. Similar to plane wave methods, grid-based implementations usually employ pseudopotentials or related approaches such as the PAW method [71] to circumvent the problem of representing the nuclear Coulomb potential and the complicated shape of the core orbitals near the nuclei.

An advantage of numerical grids is that the discretization error can be controlled systematically by increasing the number of grid points. This is harder to achieve with localized basis sets based on GTFs or STFs, where the choice of basis typically requires considerable experience by the user. Real-space grids obviously are well suited for parallelization, and GPU implementations of grid-based ground- and excited-state DFT methods are discussed in Chapters 9 and 10.

# ## 3.4.5 Auxiliary Basis Sets

As mentioned previously, three- and four-center ERIs cannot be computed if STFs are employed as the orbital basis set. In this case, an auxiliary basis set \(\{t_n\}\) of STFs is used to expand the electron density [63] according to

$$\rho(\mathbf{r}) \approx \sum_a d_a t_a(\mathbf{r}).$$ (3.46)

The Hartee potential of Eq. (3.25) can then be analytically computed on the points of a numerical integration grid and the corresponding contributions to the energy and matrix elements of the KS potential obtained by numerical quadrature, as explained in more detail in Chapter 5.

Without going into great details, such auxiliary basis expansions are widely used also with Gaussian basis sets and for HF theory and wave function-based electron correlation methods [76, 77]. These methods are sometimes referred to as density fitting or resolution of the identity (RI) methods. In brief, the four-index ERIs of Eq. (3.18) can, in general, be approximated as

$$(\mu\nu|\kappa\lambda) \approx \sum_{ab} (\mu\nu|a)[J^{-1}]_{ab}(b|\kappa\lambda),$$ (3.47)

where the two-index quantity \([J^{-1}]\) is the inverse of the Coulomb metric evaluated in the auxiliary basis

$$J_{ab} = \int d\mathbf{r} \frac{t_a(\mathbf{r})t_b(\mathbf{r}')}{|\mathbf{r} - \mathbf{r}'|}.$$ (3.48)

The three-index ERIs \((\mu\nu|a)\) thus project the basis function products \(\phi_\mu\phi_\nu\) onto the space spanned by the auxiliary basis set \(\{t_n\}\). A variety of other closely related approaches to approximate the four-index ERIs through three-index intermediates are available, including the pseudospectral [78, 79] and Cholesky decomposition [76, 80, 81] techniques.

The auxiliary basis sets used in density fitting have to be optimized both for the corresponding orbital basis set and for the specific application. For instance, the requirements to the auxiliary basis set in DFT methods are different than those in ab initio wave function methods. For DFT, only the electron density n needs to be well approximated, while in the latter case the auxiliary basis needs to represent more complicated functions such as the orbital products \(\psi_\mu\psi_\nu\) between occupied and virtual molecular orbitals.

Significant speedups are obtained using density-fitting approaches in HF and DFT calculations for small to medium sized molecules in which linear scaling techniques are not yet efficient. Similarly,