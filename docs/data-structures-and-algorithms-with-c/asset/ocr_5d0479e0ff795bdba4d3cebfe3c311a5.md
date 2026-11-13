![](bbox=[0.22, 0.08, 0.78, 0.28])

Figure G.4

+   (A) 4 (B) 6 (C) 8 (D) 10

Q29. A cycle on n vertices is isomorphic to its complement. The value of n is ___

+   (A) 2 (B) 4 (C) 6 (D) 5

Ans:(D)5

The complement graph is also isomorphic (same number of vertices connected in same way) to given graph.

![](bbox=[0.35, 0.47, 0.65, 0.6])

Figure G.5

Q30. Consider the pseudocode given below. The function DoSomething() takes as argument a pointer to the root of an arbitrary tree represented by the leftMostChild-rightSibling representation. Each node of the tree is of type treeNode.

```
typedef struct treeNode* treeptr;
struct treeNode
{
    treeptr leftMostChild,rightSibling;
};
int DoSomething (treeptr tree)
{
    int value=0;
    if (tree!= NULL)
    {
        if (tree->leftMostChild == NULL)
            value = 1;
```