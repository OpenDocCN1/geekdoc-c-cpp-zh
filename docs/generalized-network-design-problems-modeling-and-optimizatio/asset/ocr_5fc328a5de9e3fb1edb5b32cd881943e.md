We refer to this model as the bidirectional flow formulation of the GMSTP and let \( P_{bidflow} \) denote its set of feasible solutions in \( (x, z) \)-space. Note that, since we have eliminated the variables \( w_e \) when constructing the bidirectional flow formulation, this model is defined on the undirected graph \( G = (V, E) \), even though for each commodity \( k \) we permit flows \( f_{ij}^k \) and \( f_{ji}^k \) in both directions on edge \( e = \{i, j\} \).

In the bidirectional flow formulation, the constraints (2.24), which we are called the bidirectional flow inequalities, link the flow of different commodities flowing in different directions on the edge \(\{i, j\}\). These constraints model the fact that in any feasible generalized spanning tree, if we eliminate edge \(\{i, j\}\) and divide the nodes in two sets, any commodity whose associated node is in the same set as the root node, does not flow on edge \(\{i, j\}\). Additionally, any two commodities whose associated nodes are both in the set without the root, both flow on edge \(\{i, j\}\) in the same direction. So, whenever two commodities \( h \) and \( k \) both flow on edge \(\{i, j\}\), they both flow in the same direction and therefore one of \( f_{ij}^h \) and \( f_{ij}^k \) equals zero.

# **Proposition 2.6** (Pop [142]). \( P_{mcflow} = P_{bidflow} \).

Proof. If \( (w, x, z, f) \in P_{mcflow} \) then, using the constraints (2.11) we have

```
\( f_{ij}^h + f_{ji}^k \le w_{ij} + w_{ji} = x_e, \quad \forall e = \{i, j\} \in E \text{ and } \forall h, k \in K_1. \)
```

On the other hand, assume that \( (x, z, f) \in P_{bidflow} \). From the constraints (2.24), we get

```
\( \max_h f_{ij}^h + \max_k f_{ji}^k \le x_e \quad \forall e = \{i, j\} \in E. \)
```

Hence, we can choose \( w \) such that \( \max_h f_{ij}^h \le w_{ij} \) and \( x_e = w_{ij} + w_{ji} \) for all \( e = \{i, j\} \in E \). Take for example

```
\( w_{ij} = \frac{1}{2}(x_e + \max_h f_{ij}^h - \max_k f_{ji}^k). \)
```

Clearly, \( (w, x, z, f) \in P_{mcflow} \). \(\square\)

We obtain another formulation, referred to as the undirected multicommodity flow model, by replacing the inequalities (2.22) with the weaker constraints:

```
\( f_{ij}^k \le x_e \text{ for every } k \in K_1 \text{ and } e \in E. \)
```

# **Flow cut formulation** (Feremans [37])

The flow cut formulation is closely related to the multicommodity flow formulation. The main difference between the two is that the flow balance constraints (2.21) and