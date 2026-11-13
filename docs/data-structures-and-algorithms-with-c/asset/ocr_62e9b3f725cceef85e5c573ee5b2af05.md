In the one-way inorder threaded binary tree, an only right null pointer used as a thread that will point to the next node in the inorder traversal (i.e. inorder successor). However, the right null pointer of the last node remains unused. In the two-way inorder threaded binary tree, left null pointer acts as a thread that will point to the previous node in the inorder traversal (i.e. inorder predecessor) and right null pointer acts as a thread that will point to the next node in the inorder traversal (i.e. inorder successor). However, the left null pointer of the first node and the right null pointer of the last node remains unused.

![](bbox=[0.25, 0.21, 0.75, 0.42])

# Figure 8.10: Two-way inorder threaded binary tree

The structure definition for a node of two-way inorder threaded binary tree as follows:

```
```c
struct Node
{
    struct Node *left;
    char lthread;
    int info;
    struct Node *right;
    char rthread;
};
typedef struct Node ThreadedTreeNode;
```
```

# Properties of Binary Tree

**Lemma 1:** A binary tree with n nodes has exactly n – 1 edges (same as any normal tree).

**Proof:** The property can be proof by induction. **Induction Base:** Let n = 1. That is there is only one node in the tree. Therefore, a number of the edge is 0. Hence, the property is true for one node. **Induction Hypothesis:** Assume the property is true for n = k i.e., for k nodes there is k – 1 edges. **Induction Step:** The number of edges for k nodes is k - 1 edges by the induction hypothesis. Now addition of one node (i.e. n = k + 1) includes one extra edge. Therefore, total number of edges are = (k – 1) + 1 = k. Hence proved.

**Lemma 2:** The maximum number of nodes on level i of a binary tree is 2^(i-1), i >= 1

**Proof:** The property can be proof by induction on i. **Induction Base:** The root is the only node on level i=1.