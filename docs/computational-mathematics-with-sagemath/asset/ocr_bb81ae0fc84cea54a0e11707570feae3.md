![](bbox=[0.182, 0.081, 0.818, 0.5])

Figure 15.3 — The simple graphs with 5 vertices and at most 4 edges.

```
24637809253125004524383007491432768
sage: Graphs(19).random_element()
Graph on 19 vertices
```

What we have seen so far also applies, in principle, to finite algebraic structures like the dihedral groups:

```
sage: G = DihedralGroup(4); G
Dihedral group of order 8 as a permutation group
sage: G.cardinality()
8
sage: G.list()
[(), (1,4)(2,3), (1,2,3,4), (1,3)(2,4), (1,3), (2,4), (1,4,3,2), (1,2)
    (3,4)]
```

or the algebra of 2 × 2 matrices over the finite field ℤ/2ℤ:

```
sage: C = MatrixSpace(GF(2), 2); C.list()
[
[0 0]  [1 0]  [0 1]  [0 0]  [0 0]  [1 1]  [1 0]  [1 0]  [0 1]
[0 0], [0 0], [0 0], [1 0], [0 1], [0 0], [1 0], [0 1], [1 0],
```