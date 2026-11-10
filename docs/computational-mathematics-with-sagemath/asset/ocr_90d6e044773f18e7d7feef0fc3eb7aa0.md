![](bbox=[0.128, 0.084, 0.872, 0.319])

Figure 17.1 — A maximum flow problem over Chvátal’s graph.

This being said, we are left with the task of maximising the flow leaving $s$: all of it will end up in $t$, as the other vertices are sending just as much as they receive. We can model the flow problem with the following linear program (assuming that the capacities of the edges are all equal to 1):

最大化：$\displaystyle \sum_{sv\in E(G)} f_{sv}$

使得：$\forall v\in V(G)\setminus\{s,t\},\quad \displaystyle\sum_{uv\in E(G)} f_{uv}=\sum_{uv\in E(G)} f_{vu}$

$\forall uv\in E(G),\ f_{uv}\leq 1$。

We will solve the flow problem over an orientation of Chvátal’s graph (cf. Figure 17.1), in which all edges have a capacity of 1:

```
```python
sage: g = graphs.ChvatalGraph()
sage: g = g.minimum_outdegree_orientation()
```
```

```
```python
sage: p = MixedIntegerLinearProgram()
sage: f = p.new_variable()
sage: s, t = 0, 2
```
```

```
```python
sage: for v in g:
.....:     if v == s or v == t: continue
.....:     p.add_constraint(
.....:         p.sum(f[v,u] for u in g.neighbors_out(v)) ==
.....:         p.sum(f[u,v] for u in g.neighbors_in(v)))
```
```

```
```python
sage: for e in g.edges(labels = False): p.add_constraint( f[e] <= 1 )
```
```

```
```python
sage: p.set_objective(p.sum( f[s,u] for u in g.neighbors_out(s)))
```
```

```
```python
sage: p.solve()
2.0
```
```