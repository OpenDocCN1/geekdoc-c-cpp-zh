# Figure 5.5 A directed-tree representation of two sets {B, E} and {A, C, D, F, G, H}.

![](bbox=[0.417, 0.137, 0.786, 0.303])

As can be expected, maket is a constant-time operation. On the other hand, find follows parent pointers to the root of the tree and takes time proportional to the height of the tree. The tree actually gets built via the third operation, union, and we must make sure that this procedure keeps trees shallow.

Merging two sets is easy: make the root of one point to the root of the other. But we have a choice here. If the representatives (roots) of the sets are $r_x$ and $r_y$, we make $r_x$ point to $r_y$ or the other way around? Since tree height is the main impediment to computational efficiency, a good strategy is to make the root of the shorter tree point to the root of the taller tree. This way, the overall height increases only if the two trees being merged are equally tall. Instead of explicitly computing heights of trees, we will use the rank of their root nodes—which is why this scheme is called union by rank.

```
procedure union(x, y)
  rx = find(x)
  ry = find(y)
  if rx = ry: return
  if rank(rx) > rank(ry):
    π(ry) = rx
  else:
    π(rx) = ry
    if rank(rx) = rank(ry): rank(ry) = rank(ry) + 1
```

Figure 5.6 for an example.

By design, the rank of a node is exactly the height of the subtree rooted at that node. This means, for instance, as you move up a path toward a root node, the rank values along it are strictly increasing.

+   Property 1 For any x, rank(x) < rank(π(x)).