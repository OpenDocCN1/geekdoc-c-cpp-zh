
**Input:**

- `cm`: an $n$-map;

- $d \in \text{cm.Darts}$: a dart;

- $(i_1,\ldots,i_k)$: a valid sequence of integers between $0$ and $n$.

**Result:** Run through all the darts of $\langle\beta_{i_1},\ldots,\beta_{i_k}\rangle(d)$.

```
 1 ma ← reserveMarkNMap(cm);
 2 P ← an empty stack of pointer to Dart;
 3 push(P,d);
 4 markNMap(d,ma);
 5 markNMap(cm.null_dart,ma);
 6 while P is not empty do
 7     cur ← top(P);
 8     // process dart cur
 9     pop(P);
10     for j ← 1 to k do
11         if not isMarkedNMap(cur.Betas[i_j],ma) then
12             markNMap(cur.Betas[i_j],ma);
13             push(P,cur.Betas[i_j]);
14 unmark all marked darts and cm.null_dart for ma;
15 freeMarkNMap(cm,ma);
```

Algorithm 29 makes a breadth-first traversal. For that we use a stack of darts to process. We take a dart, $cur$, which belongs to $\langle\beta_{i_1},\ldots,\beta_{i_k}\rangle(d)$, and we process it. Then for each $i_j$ in the sequence, we know that $\beta_{i_j}(cur)$ belongs also to $\langle\beta_{i_1},\ldots,\beta_{i_k}\rangle(d)$. Thus we need to process it and for that it is enough to add it in the stack of dart to process. Before doing so, we test if this dart is marked. Indeed, if it is the case, this dart was already processed. Otherwise, we mark it in order to not reconsider it later and push it in the stack.

At the end of the algorithm, we must unmark all the marked darts in order to satisfy the property that all the darts are always unmarked for unused marks. This can be achieved easily by reusing the same algorithm to iterate onto these darts and reversing the role of marked and unmarked darts.

The complexity of this algorithm is linear in the number of darts of $\langle\beta_{i_1},\ldots,\beta_{i_k}\rangle(d)$, because each dart is considered exactly twice (a first time during the main loop, a second time during the unmarking step), and all operations are atomic ones.

Algorithm 29 can for example be used with the sequence $(0,\ldots,i-1,i+1,\ldots,n)$ in order to iterate through all darts of the $i$-cell $c_i(d)$ containing a given dart, for any $i \in \{1,\ldots,n\}$. For instance, the sequence $(0,1,2)$ is used to iterate through all the darts of the volume containing a given dart in a 3-map.

Note that this generic algorithm can be optimized for several specific cases by using the properties of $n$-maps. For example, the use of stack $P$ can be avoided, when iterating through the darts of a face in a 3-map, because a linear order exists for these darts. For instance, given dart $d$, we apply successively $\beta_1$ in order to traverse orbit $\langle\beta_1\rangle(d)$, then apply $\beta_3$ to $d$, and apply again successively $\beta_1$. This optimization is based upon the fact that $\beta_1 \circ \beta_3$ is a partial involution. The traversal of other orbits can be optimized in this way for similar reasons.

### Algorithm 30: Vertex iterator for $n$-maps

**Input:** `cm`: an $n$-map; $d \in \text{cm.Darts}$: a dart.

**Result:** Run through all the darts of $c_0(d)$.

```
1 ma ← reserveMarkNMap(cm);
2 P ← an empty stack of pointer to Dart;
3 push(P,d);
4 markNMap(d,ma);
5 markNMap(cm.null_dart,ma);
6 while P is not empty do
7   cur ← top(P);
8   // process dart cur
9   pop(P);
10  for i ← 1 to n − 1 do
11    for j ← i + 1 to n do
12      if not isMarkedNMap(cur.Betas[j].Betas[i],ma) then
13        markNMap(cur.Betas[j].Betas[i],ma);
14        push(P,cur.Betas[j].Betas[i]);
15      if not isMarkedNMap(cur.Betas[inv(i)].Betas[j],ma) then
16        markNMap(cur.Betas[inv(i)].Betas[j],ma);
17        push(P,cur.Betas[inv(i)].Betas[j]);
18 unmark all marked darts and cm.null_dart for ma;
19 freeMarkNMap(cm,ma);
```

The principle of this algorithm is similar to the principle of Algorithm 29. The only difference is about the considered relations. We follow here the definition of 0-cells in an $n$-map (cf. Def. 31) and thus we need to consider $\beta_i \circ \beta_j$ for any $1 \leq i < j \leq n$, and their inverses.

The complexity of Algorithm 30 is linear in the number of darts of $c_0(d)$ (because $n$ is constant).

These two algorithms are a basis for several other algorithms allowing to iterate through some specific cells based on incidence and adjacency relations. We illustrate this by showing three useful examples. In the first one, detailed in Algorithm 31, we run through one dart per each $i$-cell of an $n$-map. This algorithm allows us to process each $i$-cell exactly once.

### Algorithm 31: Iterator over one dart per each $i$-cell for $n$-maps

**Input:** `cm`: an $n$-map; $i \in \{0, \ldots, n\}$.

**Result:** Run through one dart per each $i$-cell of `cm`.

```
1  ma ← reserveMarkNMap(cm);
2  foreach dart d ∈ cm.darts do
3    if not isMarkedNMap(d,ma) then
4      // process dart d
5      mark all the darts in c_i(d) for ma;
6  unmark all darts for ma;
7  freeMarkNMap(cm,ma);
```

Algorithm 31 runs through all darts of the $n$-map, and for each nonmarked dart $d$, it marks the darts of the $i$-cell $c_i(d)$ containing $d$. Note that these darts are marked by using Algorithm 29 with the sequence $(0,\ldots,i-1,i+1,\ldots,n)$ for $i>0$ or Algorithm 30 for $i=0$. To optimize the algorithm, we use in Algorithms 29 and 30 the same mark `ma` reserved in Algorithm 31 (indeed, as the goal of line 5 is to mark all the darts in $c_i(d)$, it is useless and inefficient to use a local mark in Algorithms 29 or 30 for iterating through these darts, and to unmark these darts at the end of the iterator). At the end of Algorithm 31, we need to unmark all the marked darts. Here we are in the case where all the darts of the $n$-map are marked, thus we can simply negate the mask of mark `ma`.

The complexity of Algorithm 31 is linear in the number of darts of the $n$-map because each dart is considered in the first loop (line 2 of the algorithm), and thus each dart is marked exactly once in line 5.

A second example given in Algorithm 32 consists in iterating through one dart per each $i$-cell incident to a given $j$-cell for two given dimensions $i$ and $j$, with $i \ne j$.

This algorithm is similar to the previous one, by replacing the loop over all the darts of the $n$-map by a loop over all the darts of $c_j(d)$ (loop achieved by using Algorithms 29 or 30). Thanks to the definition of incidence in $n$-maps, we are sure that during this loop we discover at least one dart of each incident $i$-cell, and by using a mark, we ensure to process each $i$-cell only once.

### Algorithm 32: Iterator over one dart per each $i$-cell incident to a $j$-cell for $n$-maps

**Input:**

- `cm`: an $n$-map;

- $d \in \text{cm.Darts}$: a dart;

- $i \in \{0,\ldots,n\}$;

- $j \in \{0,\ldots,n\}$; with $i \ne j$.

**Result:** Run through one dart per each $i$-cell incident to $c_j(d)$.

```
1 ma ← reserveMarkNMap(cm);
2 foreach dart e ∈ c_j(d) do
3   if not isMarkedNMap(e,ma) then
4     // process dart e
5     mark all the darts in c_i(e) for ma;
6 unmark all marked darts for ma;
7 freeMarkNMap(cm,ma);
```

To unmark all the marked darts, we reuse the same algorithm by reversing the role of marked and unmarked darts.

The complexity of this algorithm is linear in the number of darts discovered during the traversal, i.e. in the number of darts of $c_j(d)$ plus the number of darts of the incident cells.

The last example given in Algorithm 33 allows to run through one dart per each $i$-cell adjacent to a given $i$-cell, for $i > 0$.

Once again we use the same principle as for the two previous examples, but here, we have to test dart $\beta_i(e)$ for each $e \in c_i(d)$. Indeed, due to the definition of adjacency relations in $n$-maps, we know that all adjacent $i$-cells to $c_i(d)$ can be reached by such a dart. For $i = 1$ it is also required to test $\beta_i^{-1}(e)$, i.e. $\beta_0(e)$. It is easy to modify this algorithm to consider the case $i = 0$ thanks to Def. 33.
