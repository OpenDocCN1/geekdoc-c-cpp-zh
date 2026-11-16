# ## 2.3.2 Formulations based on arborescence properties

Consider the directed graph \( D = (V, A) \), obtained by replacing each edge \( e = (i, j) \in E \) with the opposite arcs \( (i, j) \) and \( (j, i) \) in \( A \), having the same weight as the edge \( (i, j) \in E \). The directed version of the GMSTP introduced by Myung et al. [128], called the generalized minimum spanning arborescence problem is defined on the directed graph \( D = (V, A) \), rooted at a given cluster, here chosen to be \( V_1 \) which loss of generality, and consists of determining a minimum cost arborescence which includes exactly one node from every cluster.

The next two formulations that we will present in this section, were introduced by Feremans et al. [37].

# ### Directed generalized outset formulation (Feremans [37])

We first consider a directed generalized outset formulation of the GMSTP. In this model we consider the directed graph \( D = (V, A) \) with the cluster \( V_1 \) chosen as a root without loss of generality, and we denote with \( K_1 = K \\ \{1\} \).

```
min \sum_{e \in E} c_e x_e
s.t. \quad z(V_k) = 1, \quad \forall k \in K = \{1, \dots, m\}
x(E) = m - 1
w(\delta^-(S)) \ge z_i, \quad \forall i \in S \subseteq V \\ V_1 \quad (2.9)
w_{ij} \le z_i \quad \forall i \in V_1, j \notin V_1 \quad (2.10)
w_{ij} + w_{ji} = x_e \quad \forall e = (i, j) \in E \quad (2.11)
x, z, w \in \{0, 1\}. \quad (2.12)
```

In this model, the constraints (2.9) and (2.10) guarantee existence of a path from the selected root node to any other selected node, which includes only the selected nodes. Let \( P_{rcut} \) denote the projection of the feasible set of the linear programming relaxation of this model into the \( (x, z) \)-space.

Another possible directed generalized outset formulation, considered by Myung et al. in [128], was obtained by replacing (2.3) with the following constraints:

```
w(\delta^-(V_1)) = 0 \quad (2.13)
w(\delta^-(V_k)) \le 1, \quad \forall k \in K_1. \quad (2.14)
```

# ### Directed subpacking formulation (Feremans [37])

We now introduce a formulation of the GMSTP based on branchings. Consider, as in the previous formulation, the digraph \( D = (V, A) \), with \( V_1 \) chosen as the cluster root.