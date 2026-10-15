```
Algorithm 14: copyNGMap (gm, gm′): copy an n-Gmap into a second n′-Gmap

Input: gm: an n-Gmap;
       gm′: an n′-Gmap.
Result: Copy gm into gm′ until minimum(n, n′).

1  gm′.Darts ← ∅;
2  gm′.FreeMarks ← gm.FreeMarks;
3  assoc ← an empty associative array between darts;
4  foreach dart d ∈ gm.Darts do
5      assoc[d] ← createDartNGMap(gm′);
6  k ← min(n, n′);
7  foreach dart d ∈ gm.Darts do
8      d′ ← assoc[d];
9      for i ← 0 to k do
10         d′.Alphas[i] ← assoc[d.Alphas[i]];
11     for i ← 0 to NB_MARKS − 1 do
12         d′.Marks[i] ← d.Marks[i];
```

```
Algorithm 15: increaseDimNGMap (gm): increase the dimension of an n-Gmap

Input: gm: an n-Gmap.
Output: The (n + 1)-Gmap obtained from gm by increasing its dimension.

1  gm′ ← createNGMap(n + 1);
2  copyNGMap(gm, gm′);
3  return gm′;
```