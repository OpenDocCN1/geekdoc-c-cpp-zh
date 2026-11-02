inserting and locating elements in a binary search tree takes time O(log N). For this reason it is usually very efficient to store data, which is annotated with a key, in a tree.

Whether this is the case, depends on the order the key values are inserted into the tree. For example, if the key values are inserted in already descending or ascending order, the resulting “tree” in fact will be a list, see Fig. 6.14, where the number of levels grows linearly with the number of nodes, instead of growing logarithmically. In this case, inserting and locating nodes would take linear time again. A list is a special case of an unbalanced tree, which, in general, contains nodes, whose two subtrees differ significantly in height, for example at least by two. There are several extensions of binary search trees, where the trees are always kept balanced, which guarantees that the main tree operations, also removal of nodes, can be performed in O(log N) time. The basic idea of these algorithms is that first elements are inserted as explained above (or removed, see below), and the additional reorganizations are performed if the resulting tree is unbalanced. We do not go into details here; please consider specialized literature [Cormen et al. (2001); Sedgewick (1990)].

Instead, we discuss how a binary search tree can be printed using a simple algorithm, such that all nodes are printed in increasing order. This can be achieved by a recursive approach: First the left subtree is printed, then the root, finally the right subtree. This job is done by the following function, which obtains a pointer to the tree as argument.

```
```c
void print_tree(node_t *tree)
{
    if(tree != NULL)
    {
        print_tree(tree->left);
        printf("%d ", tree->key);
        print_tree(tree->right);
    }
}
```
```

This way to print a tree is also called inorder printing. Note that other orders are possible, e.g. preorder, where first the root of the current subtree is printed, then the left and finally the right subtree. For the tree shown in Fig. 6.12, the inorder output looks as follows:

13 15 20 23 24 25 27