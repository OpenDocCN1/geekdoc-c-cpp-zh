```
```text
(1,2,3,4)
sage: for e in F: print((e, on_pair(sigma, e)))
({1, 2}, {2, 3})
({1, 3}, {2, 4})
({1, 4}, {1, 2})
({2, 3}, {3, 4})
({2, 4}, {1, 3})
({3, 4}, {1, 4})
sage: on_pairs(sigma)
[{2, 3}, {2, 4}, {1, 2}, {3, 4}, {1, 3}, {1, 4}]
```
```

We can now construct the permutation group $G_n$ acting on pairs, induced by the action of $S_n$:

```
```text
sage: G = PermutationGroup([ on_pairs(sigma) for sigma in S.gens() ],
....:                       domain=F)
```
```

We compute the cycle indicator of $G_n$ next. This is a symmetric function that encodes the statistic of the cycle types of the permutations in $G_n$:

```
```text
sage: Z = G.cycle_index(); Z
1/24*p[1, 1, 1, 1, 1, 1] + 3/8*p[2, 2, 1, 1] + 1/3*p[3, 3] + 1/4*p[4, 2]
```
```

This gadget is to be interpreted as follows: the term $\frac{1}{4}p_{(4,2)}$ indicates that, in $G_4$, there are $|G_4| \cdot \frac{1}{4}=6$ permutations with one cycle of length 4 and one cycle of length 2; indeed:

```
```text
sage: [ sigma for sigma in G if sigma.cycle_type() == [4,2] ]
[({1,2},{2,3},{3,4},{1,4})({1,3},{2,4}),
 ({1,2},{2,4},{3,4},{1,3})({1,4},{2,3}),
 ({1,2},{1,3},{3,4},{2,4})({1,4},{2,3}),
 ({1,2},{1,4},{3,4},{2,3})({1,3},{2,4}),
 ({1,2},{1,4},{2,3},{3,4})({1,3},{2,4}),
 ({1,2},{3,4})({1,3},{2,3},{2,4},{1,4})]
```
```

The interesting fact about this symmetric function — and this is the content of Pólya’s enumeration formula — is that, *when evaluated on an alphabet* $A=(a_1,\ldots,a_n)$, *it returns the generating function, by weight, for the functions from* $E$ *to a set of size* $n$ *whose elements are weighted by* $A$. Skimming over the terminology, we illustrate this on our running example. We see a graph $G$ as a function from $F$ to a set with 2 elements, and weight edges with $t$ and non edges with $q$. The generating function of unlabelled graphs on 4 nodes by number of edges is then:

```
```text
sage: q,t = QQ['q,t'].gens()
sage: p = Z.expand(2, [q,t]); p
q^6 + q^5*t + 2*q^4*t^2 + 3*q^3*t^3 + 2*q^2*t^4 + q*t^5 + t^6
```
```

The term $2q^2t^4$ means that there are two graphs with four edges (and thus two non edges). The other coefficients can be checked with Figure 15.6. The total number of unlabelled graphs is obtained by further evaluating $p$ at $q=t=1$: