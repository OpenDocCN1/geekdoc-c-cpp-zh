# Algorithm 9.16 getMin(): Find the node with minimum key value in a binary search tree

```
a := root
while a.left != NULL do
    a := a.left
end while
```

The algorithm begins at the top or root node and descends along the left-hand edge of the tree. In the case of Figure 9.9 the progression from the root node (4, 4) to the (0, 1) and (-15, 9) nodes before stopping at the node with (key, data) value (-16, 5). The same basic idea produces a function that returns the node with the largest key in the tree.

Searching in a binary search tree consists of moving into the left or the right subtree, depending on the outcome of the comparison between the key of the sought-for node and of the node at the current location. Algorithm 9.17 gives the details.

# Algorithm 9.17 lookup(key): Find a node with key value key in a binary search tree

```
a := root
while a.left != NULL and a.key != key do
    if key < a.key then
        a := a.left
    else
        a := a.right
    end
end while
```

Suppose, for example, a search is to be conducted to find the node with key value 3 in Figure 9.9. The starting point is the root node that has the key value 4. As 3 < 4, the algorithm moves to the left node with a key of 0. So, the search must move to the right child with key value 1. This node has no left child. But, even if it had, the fact that 3 is larger than the current node's key would have moved the search to its right child where the target key is actually located.

Insertion of an object into a binary search tree is much like the look-up operation. One proceeds as in Algorithm 9.18 below.

# Algorithm 9.18 insert(a): Insert a node into a binary search tree

```
b := root
while b.left != NULL do
    if a.key < b.key then
        b := b.left
    else
        b := b.right
    end
end while
if a.key < b.key then
    b.left := a
else
    b.right := a
end
return b
```