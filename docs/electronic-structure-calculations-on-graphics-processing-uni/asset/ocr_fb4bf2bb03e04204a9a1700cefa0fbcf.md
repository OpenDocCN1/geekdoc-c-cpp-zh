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