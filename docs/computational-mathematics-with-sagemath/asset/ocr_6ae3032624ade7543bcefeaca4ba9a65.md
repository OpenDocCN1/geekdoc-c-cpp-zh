$$\max: \sum_{e\in E(G)} m_e$$

$$\text{such that: } \forall v\in V(G), \sum_{e\in E(G), e\sim v} m_e \leq 1.$$

This problem is readily adapted to a MILP using Sage:

```
```sage
sage: g = graphs.PetersenGraph()
sage: p = MixedIntegerLinearProgram()
sage: matching = p.new_variable(binary = True)

sage: p.set_objective(p.sum(matching[e]
....:                     for e in g.edges(labels = False)))

sage: for v in g:
....:     p.add_constraint(p.sum(matching[e]
....:                          for e in g.edges_incident(v, labels = False)) <= 1)
sage: p.solve()
5.0

sage: matching = p.get_values(matching)
sage: [e for e, b in matching.iteritems() if b == 1]
[(0, 1), (4, 9), (6, 8), (5, 7), (2, 3)]
```
```

**Exercise 66** (*Dominating set*). A dominating set in a graph is a set of vertices $S$ such that each vertex which is not in $S$ has at least one neighbour in $S$. Write a linear program over the integers to find a dominating set whose cardinality is minimal for the Petersen graph.

# ### 17.4.3 Flow

In this section we present yet another fundamental algorithm in graph theory: maximum flow! Given a pair of vertices $s$ and $t$ of a *directed graph* $G$ (that is, the edges have a direction, see Figure 17.1), this problem consists in sending from $s$ to $t$ a *maximum flow*, using the edges of $G$. Each one of these edges has an associated *maximal capacity* — i.e., the maximal flow which can go through it.

The definition of this problem is almost its formulation as a linear program: we are looking for a real value associated to each edge, representing the intensity of flow going through it, under two types of constraints:

+   - the amount of flow arriving at a vertex (different from $s$ or $t$) should equal the amount of flow leaving it;
+   - the flow over an edge cannot exceed its capacity.