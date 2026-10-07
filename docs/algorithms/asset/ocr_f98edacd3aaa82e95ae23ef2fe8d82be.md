# Chapter 5

# Algorithms 135

cannot have common descendants, since by Property 1 any element has at most
one ancestor of rank k. Which means

**Property 3** If there are n elements overall, there can be at most n/2 nodes of
rank k.

This last observation implies, crucially, the maximum rank is log n. Therefore,
all the trees have height ≤ n, and this is an upper bound on the running time of
find and union.

**Path compression:**

![](bbox=[0.0, 0.0, 0.0, 0.0])

With the data structure presented so far, the total time for Kruskal's algorithm
comes O(|E|log|V|) for sorting edges (remember, log|E| ≈ log|V|) plus an
O(|E|log|V|) for the union and find operations that dominate the rest of
t algorithm. So there seems to be little incentive to make our data structure
more efficient.

But if the edges are given unsorted? Or if the weights are small, O(|E))
 sorting can be done in linear time? Then the data structure becomes the
bleneck, and it is useful to think about improving its performance beyond log
per operation. As it turns out, the improved data structure is useful in many other
applications.

But can we perform union's and find faster than log n? The answer is,
being a more careful to maintain our data structure in good shape. As any
housekeeper knows, a little extra effort into maintenance can pay off
handsomely in the long run, by forestalling calamities. We have in mind
particular operation for our union-find data structure, intended to keep
the trees—during each find, when a series of pointers is followed to
to root of the tree, we will change all pointers so they point directly
to the root (Figure 5.7). This path compression heuristic only slightly increases the
time needed for a find and is easy to code.

```
function find(x)
  if x ≠ π(x): π(x) = find(π(x))
  return π(x)
```

The benefit of this simple alteration is long-term rather instantaneous and thus
nitates a particular kind of analysis: we need to look at sequences of find and
union operations, starting from an empty data structure, and measure the average
time per operation. This amortized cost turns out to be barely more O(1),
from the early O(log n).

Think of the data structure as having a “top level” consisting of the root nodes,
below it, the insides of the trees. There is a division of labor: find operations,
with without path compression) only touch the insides of trees, whereas union's only
look at the top level. Thus path compression has no effect on union operations and
leaves the top level unchanged.

We know that the ranks of root nodes are unaltered, but about what nonroot
nodes? The key point is here that once a node ceases to be a root, it never resurfaces,