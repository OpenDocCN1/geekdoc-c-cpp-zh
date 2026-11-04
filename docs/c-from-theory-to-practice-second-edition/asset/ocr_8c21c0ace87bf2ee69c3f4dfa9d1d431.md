Consult that code and try U.14.18. Our approach to solve it was first to visit all left nodes. We also changed the queue to LIFO. For example, consider the nodes of the first program. Initially, the nodes 9, 6, and 4 are stored. We pop the last one and display its key, that is, 4. We pop the last but one, that is, 6, and ... to be continued.

# Exercises

# C.14.16 Add a recursive function that displays the smallest key value in the tree.

```
void find_min(node *p)
{
    if(p == NULL)
        return;
    if(p->left == NULL)
    {
        printf("Min:%d\n", p->key);
        return;
    }
    find_min(p->left);
}
```

Comments: In a binary search tree, the smallest value is stored in the leftmost node. Then, the recursion ends. To find the largest value, just change the pointer to p->right, to find the rightmost node. Call the function with argument the root pointer, to test its operation. For an alternative nonrecursive solution, try U.14.16.

# C.14.17 Write a recursive function that counts the nodes of the tree.

```
void tree_nodes(node *p)
{
    if(p == NULL)
        return;
    cnt++;
    tree_nodes(p->left);
    tree_nodes(p->right);
}
```

Comments: cnt could be a global variable initialized with 0 and incremented by one each time a node is visited.

# C.14.18 Modify the structure that represents the node, in order to store different strings in the tree. For example:

```
typedef struct node
{
    char *key;
    struct node *left;
    struct node *right;
} node;
```