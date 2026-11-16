$u_p = \sum_k \langle u, \phi_k \rangle \phi_k.$
(2.46)

We remark here that the approximation error $u - u_p$ is orthogonal to the space $V$:

$\langle u - u_p, \phi_k \rangle = 0 \quad \forall k.$

Furthermore, mean square error (MSE) of such approximation is minimum. To prove the minimality of MSE for any orthogonal projection, consider a function \( g \in L^2[a, b] \), which is approximated by using a set of orthonormal basis functions \(\{\phi_k : k = 0, \cdots, N-1\}\) such that

$g(t) = g_c(t) = \sum_{j=0}^{N-1} c_j \phi_j(t), \text{ with}$
(2.47)

$c_j = \langle g, \phi_j \rangle.$
(2.48)

The pointwise error \(\varepsilon_c(t)\) in the approximation of the function \(g(t)\) is

\(\varepsilon_c(t) = g(t) - g_c(t) = g(t) - \sum_{j=0}^{N-1} c_j \phi_j(t).\)
(2.49)

We wish to show that when the coefficient sequence \(\{c_j\}\) is obtained by orthogonal projection given by (2.48), the