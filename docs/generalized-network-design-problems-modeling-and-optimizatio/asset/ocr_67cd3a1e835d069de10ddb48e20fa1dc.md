We wish to send a flow between the nodes of the network and view an edge variable \(x_e\) as indicating whether the edge \(e \in E\) is able to carry a flow or not. We consider three such flow formulations: a single commodity model, a multicommodity model, and a bidirectional flow model. In each of these models, although the edges are undirected, the flow variables will be directed. That is, for each edge \(\{i, j\} \in E\), we will have flow in both the directions \(i\) to \(j\) and \(j\) to \(i\).

In the single commodity model, the source cluster \(V_1\) sends one unit of flow to every other cluster. Let \(f_{ij}\) denote the flow on edge \(e = \{i, j\}\) in the direction \(i\) to \(j\). This leads to the following formulation:

```
\(\begin{aligned}
\min & \sum_{e \in E} c_e x_e \\
\text{s.t.} & \quad (3.1), (3.2), \\
 & \Delta(f_e) = \mu, \quad (3.7) \\
 & f_{ij}, f_{ji} \le (m-1)x_e, \quad \forall e = (i, j) \in E, \quad (3.8) \\
 & f_{ij} \ge 0, \quad (3.9) \\
 & x, z \in \{0, 1\},
\end{aligned}\)
```

where \(\Delta(f_e) = \sum_{e \in \delta^+(i)} f_e - \sum_{e \in \delta^-(i)} f_e\) and
\(\mu = \begin{cases} (m-1)z_i & \text{for } i \in V \\ V_1 \\ -z_i & \text{if } i \in V_1 \end{cases}\).

In this model, the constraints (3.7) restrict \(m-1\) units of a single commodity flow to the cluster \(V_1\) and 1 unit of flow out of each of the other clusters. These constraints are called *mass balance equations* and imply that the network defined by any solution contains one node from every cluster and satisfies the degree constraints, every feasible solution must be a generalized Hamiltonian tour. Therefore, when projected into the space of the \((x, z)\) variables, this formulation correctly models the GTSP.

We let \(\mathcal{P}_{flow}\) denote the projection of the feasible set of the linear programming relaxation of this model into the \((x, z)\)-space.

A stronger relaxation is obtained by considering multicommodity flows. In this model every node set \(k \in K_1 = \{2, \dots, m\}\) defines a commodity. One unit of commodity \(k\) originates from \(V_1\) and must be delivered to node set \(V_k\). Letting \(f_{ij}^k\) be the flow of commodity \(k\) in arc \((i, j)\) we obtain the following formulation:

```
\(\begin{aligned}
\min & \sum_{e \in E} c_e x_e. \\
\text{s.t.} & \quad (3.1), (3.2), \\
 & \Delta(f_a^k) = \mu_k, \quad \forall k \in K_1, \quad (3.10) \\
 & f_{ij}^k \le w_{ij}, \quad \forall a = (i, j) \in A, k \in K_1, \quad (3.11)
\end{aligned}\)
```