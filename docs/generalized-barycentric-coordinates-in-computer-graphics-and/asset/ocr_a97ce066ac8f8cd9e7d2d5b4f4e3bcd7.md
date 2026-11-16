# Interior basis functions \(\phi_{P, \alpha}\)

These are the basis functions associated with the internal degrees of freedom in (15.9). We determine the coefficients \(C_{P, \gamma}^{P, \alpha}\) in (15.10) for \(1 \le \alpha, \gamma \le \mathcal{N}_P\) by explicitly requiring that

\(\int_P \phi_{P, \alpha} q_{P, \beta} dV = \delta_{\alpha, \beta}, \quad 1 \le \alpha, \beta \le \mathcal{N}_P.\)

# Edge basis functions \(\phi_{e, \alpha}\)

These are the basis functions associated with the edge degrees of freedom in (15.8). In (15.11), we determine the coefficients \(c_{e', \gamma}^{e, \alpha}\) by explicitly requiring that

\(\int_{e'} \phi_{e, \alpha} q_{e', \beta} dS = \begin{cases} \delta_{\alpha, \beta}, & \text{for } e = e', \\ 0, & \text{otherwise} \end{cases} \quad \forall e, e' \in \mathcal{E}_P, \quad 1 \le \alpha, \quad \beta \le k-1,\)

and the coefficients \(C_{P, \gamma}^{e, \alpha}\) by explicitly requiring that

\(\int_P \phi_{e, \alpha} q_{P, \beta} dV = 0 \quad \forall e \in \mathcal{E}_P, \quad 1 \le \alpha \le k-1, \quad 1 \le \beta \le \mathcal{N}_P.\)

# Vertex basis functions \(\phi_{\mathbf{v}_i}\)

These are the basis functions associated with the cell vertices according to Definition 15.3. The canonical condition \(\phi_{\mathbf{v}_i}(\mathbf{x}_j) = \delta_{ij}\) is automatically satisfied by the definition given in (15.12) since \(\psi_{\mathbf{v}_i}(\mathbf{x}_j) = \delta_{ij}\), while \(\psi_{\mathbf{e}, \gamma}(\mathbf{x}_j) = 0\) for every \(e \in \mathcal{E}_P\) and \(1 \le \gamma \le k-1\), and \(\psi_{P, \gamma}(\mathbf{x}_j) = 0\) for every \(1 \le \gamma \le \mathcal{N}_P\). Hence, the coefficients "C" on the right-hand side of (15.12) must be determined so that all internal moments and edge moments of each \(\phi_{\mathbf{v}_i}\) are zero. To this end, we require that the coefficients \(C_{e, \gamma}^{\mathbf{v}_i, \gamma}\) of (15.12) satisfy the condition

\(\int_e \phi_{\mathbf{v}_i} dS = 0 \quad \forall \mathbf{v}_i \in \partial P, \quad \forall e \in \mathcal{E}_P, \quad 1 \le \beta \le k-1,\)

and the coefficients \(C_{P, \gamma}^{\mathbf{v}_i}\) satisfy the condition:

\(\int_P \phi_{\mathbf{v}_i} q_{P, \beta} dV = 0 \quad \forall \mathbf{v}_i \in \partial P, \quad 1 \le \beta \le \mathcal{N}_P.\)

It is easy to prove that the above set of conditions is unisolvent and hence the two bases represent the same space. However, we stress that the VEM uses the virtual basis directly through the corresponding degrees of freedom, and none of the local basis functions are ever computed or evaluated in practice.