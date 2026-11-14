the grid. Finally, the Becker and spherical weights are multiplied and the atomic labels are dropped to form the final set of quadrature points and weights:

```
$$w_{\vec{q}\lambda} \rho \rightarrow \omega_i, \qquad \vec{T}_{\vec{q}\rho} \rightarrow \vec{T}_i. \qquad (4.56)$$
```

Once the grid has been established, the density and its gradient at each grid point are needed in order to evaluate the XC kernel. For an AO alpha-spin density matrix, these are evaluated as follows:

```
$$\rho_a(\vec{T}) = \sum_{\mu\nu} P_{\mu\nu}^a \phi_\mu(\vec{T})\phi_\nu(\vec{T}), \qquad (4.57)$$
```

```
$$\nabla \rho_a(\vec{T}) = \sum_{\mu\nu} P_{\mu\nu}^a \phi_\mu(\vec{T})\nabla \phi_\nu(\vec{T}). \qquad (4.58)$$
```

As a result of the exponential decay of the basis functions $\phi_\mu$, the sum for each grid point $\vec{T}$ need only include a few significant AOs. These are efficiently identified by spatially binning the significant primitive pair distributions, which are determined as

```
$$\{ \chi_i, \chi'_i | e_{aw} < \max_{\vec{T}} \chi_i(\vec{T})\chi'_i(\vec{T}) P_i^{\text{max}}, \chi_i \in \phi_\mu, \chi'_i \in \phi_\nu \}, \qquad (4.59)$$
```

where $e_{aw}$ is some small threshold. The primitive lists and quadrature points are then copied to the GPU, where each thread computes the sums of Eqs. (4.57) and (4.58) for a single grid point. The primitive pairs are sorted by increasing exponent within each spatial bin. As a result, the entire bin may be skipped after the first negligible pair-combination has been reached. As in the evaluation of quadrature weights, the spatial binning of grid points minimizes warp divergence by ensuring that neighboring threads share identical sets of significant basis functions. The same procedure is repeated for the beta density in spin-polarized calculations.

Next, the density at each quadrature point is used to evaluate the XC-kernel function and its various derivatives on the grid. Thus the following values are computed for each grid point:

```
$$a_i = \omega f_{xc}(\rho_a(\vec{T}), \rho_b(\vec{T}), \gamma_{aa}(\vec{T}), \gamma_{ab}(\vec{T}), \gamma_{bb}(\vec{T})),$$
$$b_i = \omega \frac{\partial f_{xc}(\vec{T})}{\partial \rho_a},$$
$$c_i = \omega \left( 2 \frac{\partial f_{xc}(\vec{T})}{\partial \gamma_{aa}} \nabla \rho_a + \frac{\partial f_{xc}(\vec{T})}{\partial \gamma_{ab}} \nabla \rho_b \right). \qquad (4.60)$$
```

This step has a small computational cost and can be performed on the host without degrading performance. This is desirable as a programming convenience because implementing various density functionals can be performed without editing CUDA kernels and because the host provides robust and efficient support for various transcendental functions needed by some density functionals. During this step, the kernel values $a_i$ are also summed to evaluate the total exchange-correlation energy per Eq. (4.49).

The final step is to construct the AO matrix elements for the exchange-correlation potential. This task is again performed on the GPU. For all non-negligible primitive pair distributions $\{ \chi_i, \chi'_i | e_{aw} < \max_{\vec{T}} \chi_i(\vec{T})\chi'_i(\vec{T}), \chi_i \in \phi_\mu, \chi'_i \in \phi_\nu \}$, the pair quantities $K_{ij}$, $\vec{T}_{ij}$, and $\eta_{ij}$ from Eq. (4.22) are packed into arrays and transferred to device memory. The grid point positions $\vec{T}_a$ are spatially binned and