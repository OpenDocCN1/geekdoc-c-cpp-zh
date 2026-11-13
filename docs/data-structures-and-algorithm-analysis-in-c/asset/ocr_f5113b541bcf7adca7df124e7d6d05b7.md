![](bbox=[0.21, 0.09, 0.46, 0.28])

Figure 4.12 Worst-case binary tree

# 4.2.1 Implementation

Because a binary tree node has at most two children, we can keep direct links to them. The declaration of tree nodes is similar in structure to that for doubly linked lists, in that a node is a structure consisting of the element information plus two pointers (left and right) to other nodes (see Fig. 4.13).

We could draw the binary trees using the rectangular boxes that are customary for linked lists, but trees are generally drawn as circles connected by lines, because they are actually graphs. We also do not explicitly draw nullPtr links when referring to trees, because every binary tree with N nodes would require N + 1 nullPtr links.

Binary trees have many important uses not associated with searching. One of the principal uses of binary trees is in the area of compiler design, which we will now explore.

# 4.2.2 An Example: Expression Trees

Figure 4.14 shows an example of an expression tree. The leaves of an expression tree are operands, such as constants or variable names, and the other nodes contain operators. This particular tree happens to be binary, because all the operators are binary, and although this is the simplest case, it is possible for nodes to have more than two children. It is also possible for a node to have only one child, as is the case with the unary minus operator. We can evaluate an expression tree, T, by applying the operator at the root to the values

```
struct BinaryNode
{
    Object      element;   // The data in the node
    BinaryNode *left;      // Left child
    BinaryNode *right;     // Right child
};
```

Figure 4.13 Binary tree node class (pseudocode)