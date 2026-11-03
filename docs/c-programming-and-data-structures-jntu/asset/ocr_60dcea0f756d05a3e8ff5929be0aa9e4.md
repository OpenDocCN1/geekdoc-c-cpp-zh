in_order (root->right);

This will cause a call to itself with the value c now, so it will print c.

At this stage, the traversal from d to the left sub-tree is over. So, the function will print d.

After this, the right sub-tree of the root (i.e. e-f-g) gets printed similar to the way the left sub-tree was printed earlier, using recursive calls. We will not explain it, as it is exactly similar to the way a-b-c were printed.

# The pre-order traversal would look as follows.

```
```c
void pre_order (struct tree *root)
{
    if (!root)
        return;

    printf ("%d", root->number);
    pre_order (root->left);
    pre_order (root->right);
}
```
```

# Finally, the function for a post-order traversal would be as follows.

```
```c
void post_order (struct tree *root)
{
    if (!root)
        return;

    post_order (root->left);
    post_order (root->right);
    printf ("%d", root->number);
}
```
```

# Depth-first and Breadth-first traversals of a binary tree

In the depth-first traversal technique, we traverse a single path of the tree as far as we can. That is, we visit a node with no successors or a node, all of whose successors have already been visited. We then resume at the last node on the path just traversed that has an unvisited successor, and begin traversing a new path starting with that node. Spanning trees created with depth-first traversal are usually very deep.

In the breadth-first traversal mechanism, we visit all successors of a visited node before we visit any successors of any of those successors. This is in contrast to the depth-first traversal, wherein we visit the successor of a visited node before visiting any other nodes at its level (i.e. its brothers). Breadth-first trees are usually not deep—instead, they are short and wide.

The following program finds the depth of a binary tree:

```
```c
/* Finding the depth of Binary Tree */
```
```