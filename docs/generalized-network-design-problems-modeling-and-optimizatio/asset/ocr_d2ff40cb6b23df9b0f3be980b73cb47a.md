# Subtour elimination constraints

Formation of any subtour between clusters excluding \(V_0\) is not allowed by the following constraint:

\(u_p - u_r + Qw_{pr} + (Q - q_p - q_r)w_{rp} \le Q - q_r \quad p \neq r \neq 0, p, r \in C \quad (5.12)\)

where \(w_{pr} = 0\), whenever \(q_p + q_r > Q\) with \(p \neq r\) and \(p, r \in C\).

These constraints are adapted from the subtour elimination constraints of the capacitated VRP (see Desrochers and Laporte [23] and Kara et al. [93]).

Note that the constraints given in (5.10) guarantee that \(u_p \ge 0\) for all \(p \in C\). Therefore, we do not need nonnegativity constraints.

The first integer linear programming formulation of the GVRP is given by:

\(\text{(NB) minimize } \sum_{i=1}^n \sum_{j=1}^n x_{ij}\)
subject to (5.1)–(5.6) and (5.9)–(5.12),
\(x_{ij} \in \{0, 1\}, \forall(i, j) \in A.\)

where, \(x_{ij} = 0\) whenever \(i, j \in V_r, r \in K\) and \(w_{pr} = 0\) whenever \(q_p + q_r > Q\).

In the above formulation, the total number of binary variables is \(n(n + 1)\), i.e. \(O(n^2)\). The variables \(w_{pr}\) automatically take on binary variables. The respective numbers of constraints implied by (5.1), (5.2), (5.3), (5.4), (5.5), (5.6), (5.9), (5.10), (5.11) and (5.12) are \(m, m, 1, 1, (n + 1), m(m + 1), n, m, m\) and \(m(m - 1)\), respectively, where \(n\) is the number of customers, \(m\) is the number of clusters and \(m \le n\). Hence the total number of constraints is \(2m^2 + n + 5m + 3\), i.e. \(O(m^2) = O(n^2)\).

(NB) the node based formulation of the GVRP is structurally similar to the Kara-Bektas [92] formulation, but it contains completely different bounding constraints. We will show below, that the node based formulation produces a stronger lower bound than the formulation described by Kara and Bektas [92].

We denote the feasible set of the linear programming relaxation of the node based formulation of the GVRP by \(P_{NB}\), where we replace the integrality constraints \(x_{ij} \in \{0, 1\}\) by \(0 \le x_{ij} \le 1\). If we denote the feasible set of the linear programming relaxation of the Kara-Bektas formulation by \(P_{K-B}\), then the following result holds:

# **Proposition 5.4.** \(P_{NB} \subseteq P_{K-B}\).

**Proof.** The degree constraints, subtour elimination constraints and route continuity constraints of the two formulations are the same. They differ from each other with respect to their bounding constraints. As we discussed in the proof of the previous proposition, any cluster \(V_p\) may be on the first, or last or an intermediate position of a vehicle tour, i.e., either \(w_{0p} = 1\) or \(w_{p0} = 1\) or there exist some clusters \(V_s\) and \(V_t\) such that \(w_{sp} = w_{pt} = 1\).