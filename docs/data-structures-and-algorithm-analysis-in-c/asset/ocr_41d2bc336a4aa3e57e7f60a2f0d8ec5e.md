![](bbox=[0.05, 0.08, 0.78, 0.22])

# Figure 4.48 Zig-zag

![](bbox=[0.05, 0.29, 0.78, 0.41])

# Figure 4.49 Zig-zig

path. Let X be a (non-root) node on the access path at which we are rotating. If the parent of X is the root of the tree, we merely rotate X and the root. This is the last rotation along the access path. Otherwise, X has both a parent (P) and a grandparent (G), and there are two cases, plus symmetries, to consider. The first case is the zig-zag case (see Fig. 4.48). Here X is a right child and P is a left child (or vice versa). If this is the case, we perform a double rotation, exactly like an AVL double rotation. Otherwise, we have a zig-zig case: X and P are both left children (or, in the symmetric case, both right children). In that case, we transform the tree on the left of Figure 4.49 to the tree on the right.

As an example, consider the tree from the last example, with a rotations on k1:

![](bbox=[0.05, 0.66, 0.85, 0.86])

The first splay step is at k1 and is clearly a zig-zag, so we perform a standard AVL double rotation using k1, k2, and k3. The resulting tree follows: