These decisions are interrelated in several ways. We should only measure those layout quality attributes that can be influenced by the parameterized layout elements. As described in Section 11.4.2, a good layout has few edge crossings and edge bends, few node overlaps, favors short edges, and has a balanced aspect ratio. More subtle, and thus harder to measure and constrain, quality considerations are that the layout should reflect the graph symmetry and structure. Finally, although we may be able to design an energy function that measures all our quality attributes, finding the parameter values for which this function is minimal can be very costly and difficult.

To illustrate the preceding technique, we shall use a simple energy function that, nevertheless, is able in practice to produce good graph layouts [Fruchterman and Reingold 91]. This energy function attempts to enforce two quality criteria:

+   - connected graph nodes should be close;
+   - no two different nodes should be too close.

A simple way to describe an energy function that models these quality criteria is to use a physical analogy. Imagine that every node in the graph is a charged electric particle and every edge is an elastic spring. Hence, nodes connected by edges will exert an attraction force upon each other. This models the quality constraint that edges should be short. Additionally, all nodes will exert a repelling force on each other, regardless of whether they are connected or not. This models the second quality criterion that nodes should not overlap.

We now have to choose explicit expressions for the attractive and repulsive forces. Many choices are possible, some based on physical motivations, and some others following heuristics that yield good results in practice. A popular model for obtaining good quality layouts is to use the following forces:

```
$$
\mathbf{F}_a(n_i, n_j) = \frac{\|p_i - p_j\|}{k}(p_j - p_i),
$$
$$
\mathbf{F}_r(n_i, n_j) = -\frac{k^2}{\|p_i - p_j\|}(p_j - p_i),
$$ (11.3)
```

where $\mathbf{F}_a$ is the attraction force and $\mathbf{F}_r$ is the repulsion force between two graph nodes $n_i$ and $n_j$, $p_i$ and $p_j$ are the positions of these nodes, and $k$ is a constant. Following Fruchterman and Reingold, we set $k$ to $\sqrt{\frac{A}{N}}$, where $A$ is the area in which we want to do the layout, and $N$ is the number of graph nodes [Fruchterman and Reingold 91].

Another model for the forces is as follows [Eades 84]:

```
$$
\mathbf{F}_a(n_i, n_j) = k \log(\|p_i - p_j\|)\frac{p_i - p_j}{\|p_i - p_j\|},
$$
$$
\mathbf{F}_r(n_i, n_j) = -\frac{k}{\|p_i - p_j\|}(p_j - p_i).
$$ (11.4)
```