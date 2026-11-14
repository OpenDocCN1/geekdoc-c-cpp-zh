with the KS single-particle Hamiltonian

$\hat{F}^{\text{KS}} = -\frac{1}{2}\nabla^2 + v_{\text{ext}}(\mathbf{r}) + v_{\text{H}}(\mathbf{r}) + v_{\text{xc}}(\mathbf{r}).$ (3.24)

Here,

$v_{\text{H}}(\mathbf{r}) = \int d\mathbf{r}' \frac{\rho(\mathbf{r}')}{|\mathbf{r} - \mathbf{r}'|}$ (3.25)

and

$v_{\text{xc}}(\mathbf{r}) = \frac{\delta E_{\text{x}}[\rho]}{\delta \rho(\mathbf{r})}$ (3.26)

are the Hartree potential and the xc potential, respectively. The KS Hamiltonian looks similar to the Fock operator in HF theory, but the xc potential is a local potential, whereas the exchange operator in HF theory is orbital-dependent and nonlocal. The single-particle KS equations (3.23) look deceptively simple, but the full many-body nature is reflected in the fact of our incomplete knowledge of the xc energy density functional.

In basis set representation the KS Hamiltonian becomes

$\mathbf{F}^{\text{KS}} = \mathbf{h} + \mathbf{J} + \mathbf{V}_{\text{xc}}.$ (3.27)

where the one-electron matrix elements $h_{\mu\nu}$ and Coulomb matrix elements $J_{\mu\nu}$ are the same as in HF theory (see Eqs. (3.13) and (3.14)), and the matrix elements of the xc potential are

$V_{\text{xc},\mu\nu} = \langle \mu | v_{\text{xc}} | \nu \rangle.$ (3.28)

Thus, it is straightforward to implement DFT into an HF program by replacing the HF exchange energy and operator with the xc energy and potential.

# 3.3.2 Exchange-Correlation Functionals

For the KS method to be successful, good approximations to the exchange-correlation energy $E_{\text{xc}}$ are required [47]. For many years, the local density approximation (LDA) was the most widely used scheme. Within the LDA, the xc energy is expressed as

$E_{\text{xc}}^{\text{LDA}}[\rho] = \int d\mathbf{r} \, e_{\text{xc}}(\rho(\mathbf{r})),$ (3.29)

where $e_{\text{xc}}$ is the xc energy density of a homogeneous electron gas, which is accurately known from QMC calculations [48]. The xc functional can be divided into exchange and correlation contributions according to

$E_{\text{xc}}^{\text{LDA}}[\rho] = E_{\text{x}}^{\text{LDA}}[\rho] + E_{\text{c}}^{\text{LDA}}[\rho].$ (3.30)

In the case of LDA, the Dirac exchange energy functional is used for $E_x$. Several expressions exist for the correlation contribution, with popular versions due to Vosko, Wilk, and Nusair (VWN) [49] or Perdew and Wang (PW92) [50]. For practical purposes, all LDA functionals are nearly equivalent. The LDA approximation works well in the limit of slowly varying densities, and became popular with condensed-matter physicists who found that LDA gave good descriptions of bulk solids and surfaces, but it was never widely adopted by quantum chemists.

The situation changed with introduction of the generalized gradient approximation (GGA), which supplements the LDA functional with a term that depends on the gradient of the electron density:

$E_{\text{xc}}^{\text{GGA}}[\rho] = \int d\mathbf{r} \, e_{\text{xc}}(\rho(\mathbf{r}), \nabla \rho(\mathbf{r})).$ (3.31)