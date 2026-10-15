$i$-boundary map is not explicitly computed; nevertheless, the new darts are linked according to its definition.

```
**Algorithm 47:** `closeNGMap(gm,i)`: i-close an $n$-Gmap

**Input:** `gm`: an $n$-Gmap;  
$i \in \{0,\ldots,n\}$.

**Result:** `gm` is i-closed.

```text
1  foreach i-free dart d ∈ gm.Darts do
2      d′ ← createDartNGMap(gm);
3      d′.Alphas[i] ← d; d.Alphas[i] ← d′;
4      foreach j ∈ {0, …, i − 2, i + 2, …, n} do
5          d″ ← d.Alphas[j];
6          if not isFreeNGMap(d,j) and not isFreeNGMap(d″,i) then
7              d′.Alphas[j] ← d″.Alphas[i];
8              d″.Alphas[i].Alphas[j] ← d′;
9      if i > 0 then
10         d″ ← d.Alphas[i − 1];
11         while not isFreeNGMap(d″,i) and not
           isFreeNGMap(d″.Alphas[i],i − 1) do
12             d″ ← d″.Alphas[i].Alphas[i − 1];
13         if not isFreeNGMap(d″,i) then
14             d′.Alphas[i − 1] ← d″.Alphas[i];
15             d″.Alphas[i].Alphas[i − 1] ← d′;
```
```

In this algorithm, the new darts are created and linked by $\alpha_i$ with the corresponding i-free darts. This corresponds to item 4 of the $i$-closure definition. Then, the other $\alpha$ links are defined according to the definition of the boundary map. $\alpha_{i+1}$ is initialized to the identity for all new darts (second item of the $i$-boundary map definition): this is a result of the `createDartNGMap` function.

For all $j \in \{0,\ldots,i-2,i+2,\ldots,n\}$, $\alpha_j$ is deduced from the definition of $\alpha_j$ on the i-free dart $d$. Indeed, $\alpha_i \circ \alpha_j$ is an involution. As $\alpha_i(d)=d'$ and $\alpha_i(d)=d''$, it is necessary that $\alpha_i(d')=\alpha_j(d'')$; since $d'=f(d)$ and $\alpha_i(d'')$ is equivalent to $\alpha_j''(f(d))=f(\alpha_j'(d))$: this corresponds to item 2 of the $i$-closure definition (remember that, in this algorithm, $\alpha_i$ stands also for $\alpha_i'$ and $\alpha_i''$).

Note that $\alpha_j$ can be defined only if $d$ is not $j$-free and $d''$ is not $j$-free. Indeed, if $d$ is $j$-free then $d'$ must be also $j$-free; thus, there is nothing to do as darts are created free in all dimensions. If $d''$ is i-free, the $\alpha_j$ link between $d'$ and $\alpha_i(d'')$ cannot yet be defined: the new dart associated with $\alpha_j(d)$ is not yet created. This definition will be done in a future step of the algorithm, when dart $\alpha_j(d)$ will be processed. Indeed, it will be possible to define the