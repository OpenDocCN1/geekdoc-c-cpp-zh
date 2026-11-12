```
else if (r is a leaf)
    throw NotFoundException // Failure
// Else search the appropriate subtree
else if (r has two data items)
{
    if (target < smaller item in r)
        return findItem(r's left subtree, target)
    else if (target < larger item in r)
        return findItem(r's middle subtree, target)
    else
        return findItem(r's right subtree, target)
}
else // r has one data item
{
    if (target < r's data item)
        return findItem(r's left subtree, target)
    else
        return findItem(r's right subtree, target)
}
```

You can search the 2-3 tree and the shortest binary search tree with approximately the same efficiency, because

+   - A binary search tree with n nodes cannot be shorter than ⌈log2(n + 1)⌉
+   - A 2-3 tree with n nodes cannot be taller than ⌈log2(n + 1)⌉
+   - A node in a 2-3 tree has at most two items

Searching a 2-3 tree is not more efficient than searching a binary search tree, however. This observation may surprise you because, after all, the nodes of a 2-3 tree can have three children, and hence a 2-3 tree might indeed be shorter than the shortest possible binary search tree. Although true, this advantage in height is offset by the extra time required to compare a given value with two values instead of only one. In other words, although you might visit fewer nodes when searching a 2-3 tree, you might have to make more comparisons at each node. As a consequence, the number of comparisons that you need to search a 2-3 tree for a given item is approximately equal to the number of comparisons required to search a binary search tree that is as balanced as possible. This number is approximately log2 n.

If you can search a 2-3 tree and a balanced binary search tree with approximately the same efficiency, why then should you use a 2-3 tree? Because although maintaining the balance of a binary search tree is difficult in the face of insertion and removal operations, maintaining the shape of a 2-3 tree is relatively simple. For example, consider the two trees in Figure 19-5. The first tree is a binary

Searching a 2-3 tree is O(log n)

# FIGURE 19-5 (a) A balanced binary search tree; (b) a 2-3 tree with the same entries

![](bbox=[0.11, 0.73, 0.75, 0.93])