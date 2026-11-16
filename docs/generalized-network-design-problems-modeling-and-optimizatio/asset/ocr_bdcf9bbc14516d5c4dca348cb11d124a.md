the flow variables will be directed, although the edges are undirected. That is, for each edge \(\{i, j\} \in E\), we will have flow in both directions \(i\) to \(j\) and \(j\) to \(i\).

# Single commodity flow formulation Pop [142]

In the *single commodity model*, the source cluster \(V_1\) sends one unit of flow to every other cluster. Let \(f_{ij}\) denote the flow on edge \(e = \{i, j\}\) in the direction \(i\) to \(j\). This leads to the following formulation:

```
\(\min \sum_{e \in E} c_e x_e\)
\(\text{s.t. } z(V_k) = 1, \quad \forall k \in K = \{1, \dots, m\}\)
\(x(E) = m - 1\)
\(\sum_{e \in \delta^+(i)} f_e - \sum_{e \in \delta^-(i)} f_e = \begin{cases} (m-1)z_i & \text{for } i \in V_1 \\ -z_i & \text{for } i \in V \\ V_1 \end{cases} \quad (2.17)\)
\(f_{ij} \le (m-1)x_e, \quad \forall e = \{i, j\} \in E \quad (2.18)\)
\(f_{ji} \le (m-1)x_e, \quad \forall e = \{i, j\} \in E \quad (2.19)\)
\(f_{ij}, f_{ji} \ge 0, \quad \forall e = \{i, j\} \in E \quad (2.20)\)
\(x, z \in \{0, 1\}.\)
```

In this model, the mass balance equations (2.17) imply that the network defined by any solution \((x, z)\) must be connected. Since the constraints (2.1) and (2.3) state that the network defined by any solution contains \(m - 1\) edges and one node from every cluster, every feasible solution must be a generalized spanning tree. Therefore, when projected into the space of the \((x, z)\) variables, this formulation correctly models the GMSTP. We let \(P_{\text{flow}}\) denote the projection of the feasible set of the linear programming relaxation of this model into the \((x, z)\)-space.

# Multicommodity flow formulation (Myung et al. [118])

A stronger relaxation is obtained by considering multicommodity flows. This *directed multicommodity flow model* was introduced by Myung et al. in [128]. In this model, every node set \(k \in K_1\) defines a commodity. One unit of commodity \(k\) originates from \(V_1\) and must be delivered to node set \(V_k\). Letting \(f^k_{ij}\) be the flow of commodity \(k\) in arc \((i, j)\), we obtain the following formulation:

```
\(\min \sum_{e \in E} c_e x_e\)
\(\text{s.t. } z(V_k) = 1, \quad \forall k \in K = \{1, \dots, m\}\)
\(x(E) = m - 1\)
```