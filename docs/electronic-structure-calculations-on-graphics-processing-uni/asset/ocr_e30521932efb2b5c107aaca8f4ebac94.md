$K_{\mu}$, and packed in a bit mask, 1 indicating that the exchange element should be evaluated and 0 indicating that it should be skipped. Each block of CUDA threads checks its mask at the beginning of the exchange kernel, and blocks that are assigned a zero bit exit immediately. As will be shown for practical calculations in the following, this distance mask greatly reduces the number of ERIs evaluated by the K-Engine.

A potential problem with the simple distance mask is that $R^{\text{MASK}}$ is basis set and system-dependent. For example, for range at which the density matrix decays depends on the energy gap between the highest occupied and the lowest unoccupied molecular orbitals (HOMO and LUMO). Also, diffuse functions in the basis sets will increase the distance at which the $\mu A$-Schwarz bound becomes negligible.

These limitations can be overcome by employing the Schwarz bound to produce a rigorous bound on the full exchange matrix elements as follows:

$K_{\mu\nu} = \sum_{\lambda\sigma}^{\mathcal{N}} (\mu\lambda|\nu\sigma) P_{\lambda\sigma} \le \sum_{\lambda\sigma}^{\mathcal{N}} (\mu\lambda|\mu\lambda)^{1/2} P_{\lambda\sigma} (\nu\sigma|\nu\sigma)^{1/2}$. (4.46)

Casting the AO Schwarz bounds as a matrix Q

$Q_{\mu\nu} = (\mu\nu|\mu\nu)^{1/2}$ (4.47)

the following rigorous bound on the density matrix can be derived [25]:

$K_{\mu\nu} \le (QPQ)_{\mu\nu}$. (4.48)

For large systems, the matrix products can easily be computed in sparse algebra. Then, a bit mask is constructed to neglect all matrix elements $K_{\mu\nu}$ for which $(QPQ)_{\mu\nu} < \epsilon^{\text{MASK}}$ and the kernels are called just as in the distance mask case.

# 4.4.3 Exchange-Correlation Integration

After ERIs, the evaluation of the exchange-correlation potential represents a second major bottleneck for DFT calculations. For clarity we limit our consideration here to the acceleration of GGA-type functionals using GPUs. Our implementation is very similar to that reported by Yasuda [26]. In the general spin-polarized case, where $\rho_p \neq \rho_q$, Eqs. (4.13) and (4.21) for the exchange-correlation energy and potential become the following:

$E_{\text{XC}} = \int f_a(\rho_\alpha(\vec{r}), \rho_\beta(\vec{r}), \gamma_{aa}(\vec{r}), \gamma_{ab}(\vec{r}), \gamma_{bb}(\vec{r})) d^3\vec{r}$, (4.49)

$V_{\mu\nu}^{\text{XC}\alpha} = \int \left[ \frac{\partial f_{\text{XC}}}{\partial \rho_\alpha} \phi_\mu \phi_\nu + \left( 2 \frac{\partial f_{\text{XC}}}{\partial \gamma_{aa}} \nabla \rho_\alpha + \frac{\partial f_{\text{XC}}}{\partial \gamma_{ab}} \nabla \rho_\beta \right) \cdot \nabla (\phi_\mu \phi_\nu) \right] d^3\vec{r}$, (4.50)

where an equation analogous to Eq. (4.50) is used for $V_{\mu\nu}^{\text{XC}\beta}$, and $\gamma$ represents the gradient invariants as follows:

$\gamma_{aa}(\vec{r}) = \nabla \rho_\alpha(\vec{r}) \cdot \nabla \rho_\alpha(\vec{r})$. (4.51)

Typical XC kernel functions $f_{\text{XC}}$ are not amenable to analytical integration; thus, instead, a quadrature grid is employed to evaluate Eqs (4.49) and (4.50). Because molecular potentials exhibit discontinuous cusps near each nucleus, molecular quadrature grids are typically constructed by superposing spherical grids centered at each atom. One common and efficient approach combines the Euler-Maclaurin radial and Lebedev angular quadratures for each atomic grid. Thus, integration