
The above equations have become the standard equations for determining cluster amplitudes and corresponding energies. One should notice that, first, the nonlinear equations for the $T$ operator need to be solved iteratively before the energy can be calculated using the known cluster amplitudes.

In practical applications, the cluster operator is approximated by a many-body expansion truncated at a certain excitation level $m_k$ ($m_k \ll N$, where $N$ designates the number of correlated electrons in the system):

$T = \sum_{m_k}^{N} T_{m_k}, \qquad (14.8)$

where $T_n$ is a part of the cluster operator $T$, which produces $n$-tuple excitations when acting on the reference function. The structure of such approximations leads to a well-known “accuracy” hierarchy of the CC methods converging to the inclusion of higher rank excitations:

$\text{CCD} < \text{CCSD} < \text{CCSDT} < \text{CCSDTQ} < \cdots < \text{Full(CC)} \equiv \text{FCI}), \qquad (14.9)$

where CCD [1], CCSD [37], CCSDT [39–41], and CCSDTQ [42, 43] approaches are defined by $T \simeq T_2$, $T \simeq T_1 + T_2$, $T \simeq T_1 + T_2 + T_3$, and $T \simeq T_1 + T_2 + T_3 + T_4$, respectively. Although it has been shown that inclusion of higher order clusters provides more accurate estimates of the energy, this procedure quickly becomes numerically infeasible due to the cost of inclusion of higher rank clusters. The numerical complexity of CC approximations grows rapidly with the rank of cluster operators. For example, while CCD and CCSD approaches are characterized by $n_c^2 n_v^2$ numerical scaling ($n_c$ and $n_v$ refer to the number of occupied and unoccupied orbitals), for the CCSDT and CCSDTQ methods this scaling amounts to $n_c^3 n_v^3$ and $n_c^4 n_v^4$, respectively. Even though the cost of the CCSD methods seems to be relatively low compared to the numerical scaling of the CCSDTQ method, one should realize that performing calculations for a water pentamer will be $5^5 = 15,625$ times more expensive compared to the calculations for a water monomer (assuming that the same basis set is used). The growth in the numerical cost looks even more intimidating for higher order methods.

Unfortunately, in many calculations, especially in the area of thermochemistry, it quickly became clear that accuracies of CCSDT are needed. An efficient way of addressing this issue is to consider the links between SRCC theory and MBPT expansion. MBPT techniques enable one to determine a hierarchical structure of particular correlation effects. For example, the Møller–Plesset perturbation theory [44] establishes the following structure of the cluster operator:

$T_2 = T_2^{(1)} + T_2^{(2)} + T_2^{(3)} + \cdots \qquad (14.10)$
$T_1 = T_1^{(2)} + T_1^{(3)} + T_1^{(4)} + \cdots \qquad (14.11)$
$T_3 = T_3^{(3)} + T_3^{(4)} + T_3^{(5)} + \cdots \qquad (14.12)$
$T_4 = T_4^{(4)} + T_4^{(5)} + T_4^{(6)} + \cdots \qquad (14.13)$
$\cdots$

where the order of the perturbation expansion is denoted as the superscript. One can show that the triply excited clusters in the second order of perturbation theory can be expressed in terms of first-order doubly excited cluster amplitudes, for example,

$T_3^{(2)}|\Phi\rangle = R_3^{(0)}|V_N T_1^{(1)}|\Phi\rangle, \qquad (14.14)$

where $V_N$ is the two-body part of the Hamiltonian in normal ordered form $H_N = H - \langle \Phi | H | \Phi \rangle = F_N + V_N$, and $R_3^{(0)}$ is a three-body resolvent operator

$R_3^{(0)} = \sum_{i<j<k; a<b<c} \frac{|\Phi_{ijk}^{abc}\rangle \langle \Phi_{ijk}^{abc}|}{\epsilon_i + \epsilon_j + \epsilon_k - \epsilon_a - \epsilon_b - \epsilon_c}, \qquad (14.15)$

where \(\epsilon\)'s refer to the HF orbital energies. Using similar arguments the authors of Ref. [45] have introduced the corrections to the energy obtained in the CCSD calculations (\(E^{CCSD}\)):

\(E^{CCSD(T)} = E^{CCSD} + \langle \Phi | T_1^\dagger V_N R_4^{(0)} V T_2 | \Phi \rangle + \langle \Phi | T_1^\dagger V_N R_3^{(0)} V T_2 | \Phi \rangle , \quad (14.16)\)

which defines the so-called CCSD(T) approach. An important feature of the CCSD(T) approach is the fact that it combines elements of fourth and fifth order of the standard MBPT expansion containing triply excited intermediate states. The CCSD(T) approach can also be viewed as an extension of the CCSD(T) method [46]. Currently, the CCSD(T) method is the most frequently employed CC approach especially in studies of spectroscopic properties, geometry optimization, and chemical reactions.

The indisputable success of the CCSD(T) method in describing nondegenerate electronic states has sparked an interest toward extension of the perturbative methods accounting for the effect of triples toward more challenging cases where the wave function is no longer dominated by a single determinant. This is a typical situation encountered in bond-breaking/forming processes.

Significant progress in addressing these challenges has been achieved by developing perturbative techniques based on the partitioning of similarity-transformed Hamiltonians [47–49]. These ideas have spawned into several formulations of noniterative ground-state corrections [50–58]. Another class of methods tackling the problem of bond-breaking processes are anchored in the method of moments (MCC) formalism [59], where the expansion for the exact energy is expressed in terms of nonvanishing moments corresponding to the approximate CC approaches. The algebraic structure of these expansions makes them a very efficient tool in designing noniterative approaches. Especially effective in recovering the correlation effects is the recently introduced variant of the MMCC method based on the use of left eigenvectors of the similarity-transformed Hamiltonian (see the CR-CC(2,3) and CR-CC(2,4) approaches introduced by Piecuch et al. [60, 61]).

Recently, a new formalism, which combines a new form of the moment expansion with regularization of the cluster operator, has emerged. In the so-called generating functional (GF) moment expansion [62] (or GF expansion for short), the exact energy (\(E\)) is expressed in terms of approximate CC energy (\(E^M\)), the moments of the CC equations (\(M_J\), \(J\) labels here excited configurations), and derivatives of the GF (\(W\)), which corresponds to a connected part of the overlap between exact and auxiliary wave functions in the exponential parametrization, defined by \(\Sigma\) and \(S\) cluster operators, respectively.

\(E = E^{(A)} + \sum_{J \neq \emptyset} \tilde{M}_J^{(A)} \left[ \frac{d}{\delta S_J} W(\Sigma, S) \right]_{S|_{\Sigma=0,T=T^M}, \Sigma=0}, \quad (14.17)\)

where

\(W(\Sigma, S) = \ln \langle \Phi | (e^{\Sigma^\dagger} e^S) | \Phi \rangle . \quad (14.18)\)

The validity of the expansion (14.17) is limited only to regions where the correlation effects are characterized by rather small values of corresponding cluster amplitudes. In order to extend the GF expansion to strongly interacting systems, the regularization of cluster amplitudes is necessary. These factors have been included in the design of the regularized version of the CCSD(T) (Reg-CCSD(T)) [63], which is defined by a formula analogous to Eq. (14.16):

\(E^{reg-CCSD(T)} = E^{CCSD} + \langle \Phi | \Sigma_{reg,2}^\dagger V_N R_3^{(0)}(\omega^2) V T_2 | \Phi \rangle + \langle \Phi | \Sigma_{reg,1}^\dagger V_N R_3^{(0)}(\omega^2) V T_2 | \Phi \rangle , \quad (14.19)\)

where \(\Sigma_{reg,1}\) and \(\Sigma_{reg,2}\) are regularized cluster operators, \(\omega^2\) is a regularization parameter, and \(R_3^{(0)}(\omega^2)\) is a \(\omega^2\)-dependent three-body resolvent

\(R_3^{(0)}(\omega^2) = \sum_{i<j<k; a<b<c; \epsilon_i + \epsilon_j + \epsilon_k - \epsilon_a - \epsilon_b - \epsilon_c - \epsilon = 3\omega^2} \frac{|\Phi_{ijk}^{abc}\rangle \langle \Phi_{ijk}^{abc}|}{\dots} - 3\omega^2 . \quad (14.20)\)

Similar regularization techniques based on the Tikhonov regularization have been used to alleviate problems encountered by the linear SRCC formulations in the quasi-degenerate regime [64]. For \(\omega^2 = 0\), the Reg-CCSD(T) approach is identical to the original CCSD(T) formulation. It has been demonstrated that the regularization algorithm, Eq. (14.19), leads to significant improvements of the CCSD(T) results in the geometry regions corresponding to stretched nuclear geometries [63]. It should also be mentioned that the Reg-CCSD(T) and CCSD(T) approaches are characterized by the same numerical overhead proportional to \(n^2 o^4\). As mentioned earlier, the expressions for the Reg-CCSD(T) and CCSD(T) methods have the same algebraic structure. Therefore, the GPU implementation for the noniterative Reg-CCSD(T) methods also provides the GPU implementation for the CCSD(T) approach (\(\omega^2 = 0\)).

### 14.2.2 Multi-Reference Coupled-Cluster Formulations

Many aspects of computational chemistry require methodologies capable of describing a delicate balance between static and dynamic correlation effects for systems and processes belonging to the so-called multi-reference chemistry. The common feature of systems falling into this class of problems is the fact that the corresponding wave functions, in contrast to the closed-shell systems, cannot be described by a single Slater determinant. This situation commonly occurs in bond-breaking processes, poly-radical species, transition-metal compounds, low-spin open-shell states, and reactions involving potential energy surface crossing. To describe these problems, one has to resort to multi-reference methods such as complete active space self-consistent field formalisms, various variants of multi-reference many-body perturbation theory (MRMBPT) methods [65–73] (such as the ubiquitous CASPT2 approach [74]), and multi-reference configuration interaction functions (MRCI) [75], MRCC Methods [76–99], and canonical transformation theory [100].

The dawn of peta-scale computer architectures offers a unique opportunity to validate and apply accurate yet numerically expensive multi-reference theories to large molecular systems. The MRCC method is among the methodologies that can take advantage of this fact. The MRCC formalisms extend the applicability of the SRCC methods to quasi-degenerate situations by replacing the notion of a reference function \(|\Phi\rangle\) used in the SRCC theories by the concept of the model space (\(\mathcal{M}_0\)) spanned (\(l_S\)) by the most important Slater determinants \(|\Phi_\mu\rangle\), \(\mu = 1, \cdots, M\)

\(\mathcal{M}_0 = l_S \{|\Phi_\mu\rangle\}_{\mu=1}^{M_0}\) (14.21)

required to describe a certain subset of electronic states. In a natural way, the MRCC formalisms lead to partitioning of correlation effects into static (associated with the many-body effects within the model space \(\mathcal{M}_0\)) and dynamic (associated with the many-body effects within the complement of the model space \(\mathcal{M}_0^c\)) effects. These methods thus provide a way to properly treat correlation effects for electronic states characterized by strong correlation effects.

In this chapter, we will focus on the state-specific Hilbert space (HS) formulation of the MRCC theory, where the electronic wave function \(|\Psi\rangle\) is expressed by the Jeziorski–Monkhorst Ansatz [87]

\(|\Psi\rangle = \sum_{\mu=1}^M c_\mu e^{T(\mu)} |\Phi_\mu\rangle\) (14.22)

where the \(T^{(\mu)}\) are the reference-specific cluster operators. For the complete model space (CMS), which is defined by determinants obtained by all possible distributions of the active electrons among the active spin orbitals, the intermediate normalization condition [87] requires that the cluster operators do not produce any excitations within the model space, that is,

\(\langle \Phi_\mu | T^{(\nu)} |\Phi_\mu \rangle = 0 \quad \forall_{\mu \neq \nu}\) (14.23)
