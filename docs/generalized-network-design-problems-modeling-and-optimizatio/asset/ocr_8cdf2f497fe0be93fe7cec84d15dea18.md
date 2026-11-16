$x_e \in \{0, 1\}, \quad \forall e \in E, \qquad (3.4)$
$z_i \in \{0, 1\}, \quad \forall i \in V. \qquad (3.5)$

Here, we used the same notations as in Chapter 2 for the case of the generalized minimum spanning tree problem.

In this formulation, the objective function clearly describes the cost of an optimal generalized tour. Constraints (3.1) guarantee that we select exactly one node from each cluster, constraints (3.2) are _degree constraints_. They specify that, if a node of $G$ is selected, it is entered and left exactly once. The constraints (3.3) are _subtour elimination constraints_, that prohibit the formation of subtours, i.e. tours on subsets of less than $n$ nodes. Because of the degree constraints, subtours over one node (and hence, over $n-1$ nodes) cannot occur. Therefore, it is valid to define constraints (3.3) only for $2 \le |S| \le n-2$. Finally, the constraints (3.4) and (3.5) impose binary conditions on the variables.

This formulation, introduced by Fischetti et al. [43], is called the _generalized subtour elimination formulation_, since the constraints (3.3) eliminate all cycles on subsets with less than $n$ nodes.

Since, in the GTSP, exactly one node from each cluster must be visited, we can drop the intra-cluster edges. In view of this reduction, the constraints (3.2) are equivalent to

$x(\delta(V_k)) = 2, \quad \forall k \in K = \{1, \dots, m\},$

and the constraints (3.3) are equivalent to

$x(E(S)) \le r - 1, \quad \forall S = \cup_{j=1}^r V_j \quad \text{and} \quad 2 \le r \le m - 2.$

We may replace the subtour elimination constraints (3.3) with connectivity constraints, resulting in the _generalized cutset formulation_, introduced in [43] as well

\(\begin{aligned}
\min \quad & \sum_{e \in E} c_e x_e, \\
\text{s.t.} \quad & (3.1), (3.4), (3.5), \\
& x(\delta(S)) \ge 2(z_i + z_j - 1), \quad \forall S \subset V, \quad 2 \le |S| \le n - 2, \\
& \quad \quad \quad i \in S, \quad j \notin S. \qquad (3.6)
\end{aligned}\)

Both formulations that we have described so far, have an exponential number of constraints. The formulations that we will consider next will only have a polynomial number of constraints, but we will add a number of variables.

# ## 3.4.2 Flow based formulations

In order to give compact formulations of the GTSP, one possibility is to introduce ‘auxiliary’ flow variables, beyond the natural binary edge, and node variables.