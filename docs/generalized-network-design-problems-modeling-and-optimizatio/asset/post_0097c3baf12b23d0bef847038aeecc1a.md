
![](img/8ee31706d554c7b9e05caa9ab83aec83_178_0.png)

Figure 6.1. Example of a hierarchical network design.

fixed-charge network design (GFCND) problem and was introduced by Thomadsen and Stidsen [200].

The GFCND problem belongs to the class of generalized network design problems which are obtained from the classical network design problems in a natural way by considering a related problem relative to a given partition of the nodes of the graph into node sets.

## 6.1 Definition of the GFCNDP

Given an n-node undirected graph G = (V, E) and V1,...,Vm a partition of V into m clusters, we assume that the nodes in each cluster are internally connected by a cluster-network and the clusters, on the other hand, are not connected but have to be connected by a backbone-network, in order to be able to communicate. We assume as well, that between any two selected nodes (hubs) from different clusters there exists an inter-cluster edge having a positive cost. In addition to the costs of edge establishment, each inter-cluster edge has a required capacity that depends on the communication demand and on the way the demands are routed.

The GFCNDP seeks to find the cheapest backbone network connecting exactly one hub from each of the given clusters. The problem involves two related decisions

- Selecting a hub from each cluster |Vi|, for all i = 1, ..., m.
- Finding the cheapest backbone network connecting exactly the selected hubs.

In Figure 6.2(a) five node sets (clusters) are presented. The clusters may have a different number of nodes. We assume that all nodes from each cluster are connected by an intercluster network.

![](img/8ee31706d554c7b9e05caa9ab83aec83_179_0.png)

Figure 6.2. The generalized fixed-charge network design (a) node sets (clusters), (b) backbone network.

The clusters, on the other hand, are not connected but have to be connected by a backbone network, in order to be able to communicate. In Figure 6.2 b) such a possible backbone network is presented.

## 6.2 Integer programming formulations of the GFCNDP

Given an undirected graph \( G = (V, E) \), the associated directed graph is obtained by replacing each edge \( e = \{i, j\} \in E \) with the opposite arcs \( (i, j) \) and \( (j, i) \) with the same weight as the edge \( \{i, j\} \in E \). In order to model the GFCND problem as a mixed integer programming problem, we define the following related sets, parameters and decision variables

### Sets and notations:

- \( V \) – the set of all the nodes, \( i \in V \).
- \( V_1, \dots, V_m \) – a partition of \( V \) into \( m \) subsets called *clusters*.
- \( E \) – the set of edges (unordered node-pairs), \( e \in E \).
- \( A \) – the set of arcs (ordered node-pairs), \( a \in A \).
- \( D \) – the set of commodities which represent the demands to be satisfied between any unordered cluster-pair, \( d \in D \).
- \( s_a \) and \( t_a \) – denote the start and terminating nodes of arc \( a \).
- \( s_d \) and \( t_d \) – denote the start and terminating clusters of demand \( d \).

### Parameters:

- $c_e$ – the fixed cost of the edge $e, e \in E$.
- $g_a$ – the capacity cost of arc $a$, which is the cost per unit of demand using that arc.
- $b_d$ – the communication demand volume for demand $d$.

### Decision Variables:

- The binary decision variables

\( z_i = \left\{ \begin{array}{ll} 1 & \text{if the node } i \text{ is selected as a hub-node} \\ 0 & \text{otherwise} \end{array} \right. \) ,
\( x_e = \left\{ \begin{array}{ll} 1 & \text{if the edge } e \in E \text{ is chosen between two hub-nodes} \\ 0 & \text{otherwise} \end{array} \right. \) ,
\( w_a = \left\{ \begin{array}{ll} 1 & \text{if the arc } a \in A \text{ is chosen between two hub-nodes} \\ 0 & \text{otherwise} \end{array} \right. \) .

- The fractional continuous flow variables: \( f_{ij}^d \) reflect transportation decisions for each arc \( (i, j) \in A \) and commodity \( d \in D \).

Our first model uses the binary decision variables defined above and the multicommodity flow variables \( f_a^d \).

```
\(\min \sum_{e \in E} c_e x_e + \sum_{d \in D, a \in A} g_a b_d f_a^d\)
\(s.t.\)
\( z(V_k) = 1, \quad \forall k \in K = \{1, \dots, m\}, \) (6.1)
\( \sum_{a \in \delta^+(i)} f_a^d - \sum_{a \in \delta^-(i)} f_a^d = \left\{ \begin{array}{ll} z_i, & i \in s_d \\ -z_i, & i \in t_d \\ 0 & \text{otherwise} \end{array} \right. \quad d \in D, i \in V, \) (6.2)
\( x_e \le z_i, \quad \forall e \in E \text{ and } i \in e, \) (6.3)
\( f_{ij}^d \le w_{ij}, \quad \forall a = (i, j) \in A, d \in D, \) (6.4)
\( w_{ij} + w_{ji} = x_e, \quad \forall e = \{i, j\} \in E, \) (6.5)
\( f_a^d \ge 0, \quad \forall a = (i, j) \in A, d \in D, \) (6.6)
\( x, z, w \in \{0, 1\}. \) (6.7)
```

In the above mixed integer programming formulation of the GFCNDP, the objective function represents the combined edge establishment costs and edge capacity requirement costs, the constraints (6.1) guarantee that exactly one hub node is selected from each cluster, the flow conservation constraints (6.2) guarantee that demands are satisfied between each origin-destinations clusters. The right hand-side is $z_i$ if the demand originates at the cluster $s_d$, $-z_i$ if the demand ends in the cluster $t_d$ and 0 otherwise. The restrictions (6.3) guarantee that only edges between selected hubs will be established. The restrictions (6.4) not only ensure that arc capacities are respected, but they force the flow of any commodity to be 0 if the arc is not chosen in the design and the constraints (6.5) relate the connection between the variables attached to the edges and those attached to the arcs. Finally the constraints (6.7) and (6.8) define the domains of the variables.

We will call this model the directed multicommodity flow model. We let $P_{\text{mcflow}}$ denote the projection of the feasible set of the linear programming relaxation of this model into the $(x, z)$-space.

We obtain a closely related formulation by eliminating the binary variables $w_{ij}$. The resulting formulation consists of the constraints (6.1), (6.2), (6.3), (6.6), (6.7) plus

```
$f_{ij}^d + f_{ji}^{d'} \le x_e, \quad \forall d \in D \text{ and } \forall e \in E. \quad (6.8)$
```

We refer to this model as the *bidirectional flow formulation* of the GFCNDP and let $P_{\text{bidflow}}$ denote its set of feasible solutions in $(x, z)$-space. Observe that, since we have eliminated the variables $w_a$ in constructing the bidirectional flow formulation, this model is defined on the undirected graph $G = (V, E)$, even though for each demand $d \in D$ we perform flows $f_{ij}^d$ and $f_{ji}^d$ in both directions on edge $e = \{i, j\}$. This model was introduced by Thoradsen and Stidsen [200] and, based on it, the authors proposed a branch-cut-and-price algorithm for solving the GFCNDP.

In the bidirectional flow formulation, the constraints (6.8) which we called the bidirectional flow inequalities, link the flow of different demands flowing in different directions on the edge $\{i, j\}$.

The following result holds:

### Proposition 6.1.

$P_{\text{mcflow}} = P_{\text{bidflow}}$.

**Proof.** If $(w, x, z, f) \in P_{\text{mcflow}}$, then, using the constraints (6.4) we have that

```
$f_{ij}^d + f_{ji}^{d'} \le w_{ij} + w_{ji} = x_e, \quad \forall e = \{i, j\} \in E \text{ and } \forall d, d' \in D.$
```

On the other hand, assume that $(x, z, f) \in P_{\text{bidflow}}$. From the constraints (6.8), we get

```
$\max_d f_{ij}^d + \max_{d'} f_{ji}^{d'} \le x_e. \quad \forall e = \{i, j\} \in E.$
```

Hence, we can choose $w$ such that $\max_d f_{ij}^d \le w_{ij}$ and $x_e = w_{ij} + w_{ji}$ for all $e = (i, j) \in E$. For example, take

```
$w_{ij} = \frac{1}{2}(x_e + \max_d f_{ij}^d - \max_{d'} f_{ji}^{d'}).$
```

Clearly, $(w, x, z, f) \in P_{\text{mcflow}}.$

Let \( G' \) be the graph obtained from \( G \) after replacing all nodes of a cluster \( V_i \) with a supernode representing \( V_i \). For convenience, we identify \( V_i \) with the supernode that represents it. We will call this graph the global graph and we assume that \( G' \) with vertex set \( \{V_1, ..., V_m\} \) is complete. We will denote the set of nodes of this global graph by \( V_g \), \( V_g = \{1, ..., m\} \), the set of edges by \( E_g \), \( E_g = \{e_g = (i, j) \mid i, j \in \{1, ..., m\} \} \) and the set of arcs to \( A_g \).

Our last formulation aims to distinguish between global, i.e. inter-cluster connections, and local ones, i.e. connections between nodes from different clusters. The local-global approach introduced by Pop [142] was applied successfully to provide strong integer programming formulations, exact algorithms, solution procedures in the case of the generalized minimum spanning tree problem [160, 150] and the generalized traveling salesman problem [79].

We introduce the binary variables \( y_{ij} \) (\( i, j \in \{1, ..., m\} \)) to describe the global connections, so \( y_{ij} = 1 \) if cluster \( V_i \) is connected to cluster \( V_j \) and \( y_{ij} = 0 \) otherwise. This polytope, denoted by \( P_{FCND} \), can be represented by the following polynomial number of constraints:

```
\sum_{a_g \in \delta^+(i)} F_{a_g}^d - \sum_{a_g \in \delta^-(i)} F_{a_g}^d = \begin{cases} 1, & i \in s_{gd} \\ -1, & i \in t_{gd} \\ 0, & \text{otherwise} \end{cases} \quad \forall d \in D, i \in V_g, \quad (6.9)
F_{ij}^d + F_{ji}^d \leq y_e \kappa_e, \quad \forall e_g = (i, j) \in E_g, d \in D. \quad (6.10)
y_{ij} \in \{0, 1\}, \quad \forall i, j \in V_g. \quad (6.11)
F_{a_g}^d \geq 0, \quad \forall a_g \in A_g, d \in D. \quad (6.12)
```

where the continuous decision variables \( F_{a_g}^d \) correspond to the fraction of demand \( d \) routed on the arc \( a_g \) and the relation to the decision variables \( f_a^d \) is given by \( F_{a_g}^d = \sum_{(a=(i,j)) \in A \mid i \in V_k, j \in V_l} f_a^d \). \( \kappa_e = (k,l) \in A_g \).

If the 0-1 vector \( y \) corresponds to a fixed-charge network design problem on the contracted graph, the corresponding local solution \( x, z \in \{0, 1\}^{|E|} \) that minimizes the costs can be obtained by solving the following integer linear programming problem:

```
\min \sum_{e \in E} c_e x_e
s.t.
z(V_k) = 1, \quad \forall k \in K = \{1, ..., m\},
x(V_l, V_r) = y_{lr}, \quad \forall l, r \in K = \{1, ..., m\}, l \neq r,
x(i, V_r) \leq z_i, \quad \forall r \in K, \forall i \in V \setminus V_r,
x_e, z_i \in \{0, 1\}, \quad \forall e = \{i, j\} \in E, \forall i \in V,
```

where \( x(V_l, V_r) = \sum_{i \in V_l, j \in V_r} x_{ij} \) and \( x(i, V_r) = \sum_{j \in V_r} x_{ij} \).
