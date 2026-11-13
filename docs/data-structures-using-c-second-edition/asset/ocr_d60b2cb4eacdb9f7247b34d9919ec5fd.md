# 10.5.2 Operations on Red-Black Trees

Preforming a read-only operation (like traversing the nodes in a tree) on a red-black tree requires no modification from those used for binary search trees. Remember that every red-black tree is a special case of a binary search tree. However, insertion and deletion operations may violate the properties of a red-black tree. Therefore, these operations may create a need to restore the red-black properties that may require a small number of O(log n) or amortized O(1)) colour changes.

# Inserting a Node in a Red-Black Tree

The insertion operation starts in the same way as we add a new node in the binary search tree. However, in a binary search tree, we always add the new node as a leaf, while in a red-black tree, leaf nodes contain no data. So instead of adding the new node as a leaf node, we add a red internal node that has two black leaf nodes. Note that the colour of the new node is red and its leaf nodes are coloured in black.

Once a new node is added, it may violate some properties of the red-black tree. So in order to restore their property, we check for certain cases and restore the property depending on the case that turns up after insertion. But before learning these cases in detail, first let us discuss certain important terms that will be used.

Grandparent node (g) of a node (n) refers to the parent of N’s parent (P), as in human family trees. The C code to find a node’s grandparent can be given as follows:

```
struct node * grand_parent(struct node *n)
{
    // No parent means no grandparent
    if ((n != NULL) && (n->parent != NULL))
        return n->parent->parent;
    else
        return NULL;
}
```

Uncle node (u) of a node (n) refers to the sibling of N’s parent (P), as in human family trees. The C code to find a node’s uncle can be given as follows:

```
struct node * uncle(struct node *n)
{
    struct node *g;
    g = grand_parent(n);
    //With no grandparent, there cannot be any uncle
    if (g == NULL)
        return NULL;
    if (n->parent == g->left)
        return g->right;
    else
        return g->left;
}
```

When we insert a new node in a red-black tree, note the following:

+   • All leaf nodes are always black. So property 3 always holds true.
+   • Property 4 (both children of every red node are black) is threatened only by adding a red node, repainting a black node red, or a rotation.
+   • Property 5 (all paths from any given node to its leaf nodes has equal number of black nodes) is threatened only by adding a black node, repainting a red node black, or a rotation.