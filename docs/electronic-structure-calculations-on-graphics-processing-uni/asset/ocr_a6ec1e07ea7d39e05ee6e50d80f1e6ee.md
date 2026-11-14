# 7.2.2 Ultrasoft Pseudopotentials

In order to reduce the number of plane waves, actual calculations resort to pseudopotentials: close to each ion, the exact wavefunction is replaced by pseudo-wavefunctions centered on the ion.

The radial part of the pseudo-wavefunctions is nodeless. These pseudo-wavefunctions are localized in r-space and will be denoted by \(|\tilde{\beta}\rangle\). Projection on these pseudo-wavefunctions are denoted by \(\{\tilde{\beta}\}\), which are the dual vectors of \(|\tilde{\beta}\rangle\). The \(\tilde{\beta}\) functions of each type of atom are defined with respect to the displacement from an atomic center and vanish outside of a core region:

\(\tilde{\beta}(r) = \beta(r - R), \quad \beta(r > r_c) = 0,\)

where \(R_i\) is the position of the ion that \(\beta\) is centered around and \(r_c\) is the cut-off radius.

With USPPs, the tensor \(Q\) connects diagonal real-space 2-tensors, such as the density \(\rho\), to pairs of projectors [20]:

\(\langle \psi' | r | r' \psi \rangle \rightarrow \sum_{ij} \langle \psi' | r' \rangle \left( \langle r' | r \rangle \langle r | r' \rangle + \sum_{ij} \langle r' | \beta_i \rangle Q_{ij} \langle \beta_j | r' \rangle \right) \langle r' | \psi' \rangle,\) (7.9)

where \(\psi, \psi'\) are arbitrary vectors. Integrating over \(r\) yields an overlap matrix

\(S = I + \sum_{ij} |\beta_i\rangle Q_{ij} \langle \beta_j|,\) (7.10)

which defines the inner product \(\langle \phi | \psi \rangle \rightarrow \langle \phi | S | \psi \rangle\), where \(Q_{ij} = Q_{ij}(r)\). The eigenproblem is therefore generalized to

\(H|k\rangle |u_{nk}\rangle = \epsilon_{nk} S |u_{nk}\rangle.\) (7.11)

The change in inner product leads to an additional term in the charge density:

\(\langle r | \rho | r \rangle = \sum_{nk} f_{nk} \left( \langle r | u_{nk} \rangle \langle u_{nk} | r \rangle + \sum_{ij} \langle u_{nk} | \beta_i \rangle Q_{ij}(r) \langle \beta_j | u_{nk} \rangle \right)\) (7.12)

It also leads to the density-dependent nonlocal potential \(V^{nl}[\rho(u, \epsilon)]\), which adds to the cyclic dependence of Eq. (7.8). In the USPP scheme, \(V^{nl}\) is

\(V^{nl} = \sum_{ij} |\beta_i\rangle D_{ij} \langle \beta_j|,\) (7.13)

where the matrix \(D_{ij}\) depends on the density \(\rho\).

The rest of this chapter operates with the generality of USPP. The NCPP expressions are recovered by letting \(Q \rightarrow 0\), which implies \(S \rightarrow I\) and reduces the generalized eigenvalue problem to a standard one.

# 7.2.3 Projector Augmented Wave (PAW) Method

The PAW scheme [13] is a generalization of the USPP scheme [12] introduced in Section 7.2.2. In the PAW scheme, the wavefunction is related to smooth pseudo-wavefunctions by a linear transformation [13]:

\(|\psi\rangle = |\tilde{\psi}\rangle + \sum_i (|\phi_i\rangle - |\tilde{\phi}_i\rangle) \langle \tilde{\beta}_i | \tilde{\psi} \rangle.\) (7.14)

where the \(\phi\) are generally taken to be solutions to the radial Schrödinger equation for an isolated atom and tildes mark pseudo-quantities. Computationally, and USPP take very similar forms. The relationship between the two is discussed more formally in the literature [12]. Here, we maintain consistency with the notation used for USPPs by letting \(\tilde{\beta} \equiv \beta\).