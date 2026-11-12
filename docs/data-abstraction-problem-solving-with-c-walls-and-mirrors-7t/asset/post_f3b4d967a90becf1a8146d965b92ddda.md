
## FIGURE 19-15 (a) A 2-3 tree; (b), (c), (d), (e) the steps for removing 70; (f) the resulting tree

![](img/288a0c22d14d2450c1e772f228f867b0_606_0.png)

In general, after you remove a value from a leaf, another value may remain in the leaf (because the leaf contained two values before the removal). If this is the case, you are done, because a leaf of a 2-3 tree can contain a single value. In this example, however, once you remove 70 from the leaf, the leaf is left without a value, as Figure 19-15e indicates.

### Merge nodes

You then delete the node, as Figure 19-15d illustrates. At this point you see that the parent of the deleted node contains two values (80 and 90) but has two children (60 and 100). This situation is not allowed in a 2-3 tree. You can remedy the problem by moving the smaller value (80) down from the parent into the left child, as Figure 19-15c illustrates. Deleting the leaf node and moving a value down from a sibling of the leaf is called **merging the leaf with its sibling**. The 2-3 tree that results from this removal operation is shown in Figure 19-15f.

### Redistribute values

Remove 100. The search strategy discovers that 100 is in the leaf <100> of the tree in Figure 19-15f. When you remove the value from this leaf, the node becomes empty, as Figure 19-16a indicates. In this case, however, no merging of nodes is required, because the sibling <60 80> can spare a value. That is, the sibling has two values, whereas a 2-3 tree requires only that it have at least one value. However, if you simply move the value 80 into the empty node—as Figure 19-16b illustrates—you find that the search-tree order is destroyed: The value in 90's right child should be greater than 90, but it is 80. Instead, you move the larger value (80) from <60 80> into the parent and move the value 90 down from the parent into the node that had been empty, as Figure 19-16c shows. This distribution preserves search-tree order, and you have thus completed the removal. The resulting 2-3 tree is shown in Figure 19-16d.

## FIGURE 19-16 (a), (b), (c) The steps for removing 100 from the tree in Figure 19-15f; (d) the resulting tree

![](img/288a0c22d14d2450c1e772f228f867b0_607_0.png)

![](img/288a0c22d14d2450c1e772f228f867b0_607_1.png)

### Remove 80.

The search strategy finds that 80 is in an internal node of the tree in Figure 19-16d. You must swap 80 with its inorder successor, 90, as Figure 19-17a illustrates. When you remove 80 from the leaf, the node becomes empty, as Figure 19-17b shows. Because the sibling of the empty node has only one value, you cannot redistribute as you did in the previous removal of 100. Instead you must merge the nodes, bringing the value 90 down from the parent and deleting the empty leaf, as Figure 19-17c indicates.

You are not yet finished, however, because the parent contains no data and has only one child. You must recursively apply the removal strategy to this internal node without a value. First, you should check to see whether the node's sibling can spare a value. Because the sibling <30> contains only the single value 30, you cannot redistribute—you must merge the nodes. The merging of two internal nodes is identical to the merging of leaves, except that the child <60 90> of the empty node must be adopted. Because the sibling of the empty node contains only one value—and hence can have only two children, as stated in the rule for 2-nodes—it can become the parent of <60 90> only if you bring the value 50 down from the sibling's parent. The tree now appears as shown in Figure 19-17d. Note that this operation preserves the search property of the tree.

Now the parent of the merged nodes is left without a data item and only a single child. Usually, you would apply the recursive removal strategy to this node, but this case is special because the node is the root. Because the root is empty and has only one child, you can simply delete it, allowing <30 50> to become the root of the tree, as Figure 19-17e illustrates. This deletion has thus caused the height of the tree to shrink by 1.

To summarize, we have removed 70, 100, and 80 from the 2-3 tree in Figure 19-15a and obtained the 2-3 trees in Figures 19-17c and 19-18a. In contrast, after removing 70, 100, and 80 from the balanced binary search tree in Figure 19-5a, you are left with the tree in Figure 19-18b. Notice that the removals affected only one part of the binary search tree, causing it to lose its balance. The left subtree has not been affected at all, and thus the overall height of the tree has not been diminished.

## FIGURE 19-17 The steps for removing 80 from the tree in Figure 19-16d

![](img/288a0c22d14d2450c1e772f228f867b0_608_0.png)

![](img/288a0c22d14d2450c1e772f228f867b0_608_1.png)

![](img/288a0c22d14d2450c1e772f228f867b0_608_2.png)

![](img/288a0c22d14d2450c1e772f228f867b0_608_3.png)

![](img/288a0c22d14d2450c1e772f228f867b0_608_4.png)

## FIGURE 19-18 Results of removing 70, 100, and 80 from (a) the 2-3 tree of Figure 19-15a and (b) the binary search tree of Figure 19-5a

![](img/288a0c22d14d2450c1e772f228f867b0_608_5.png)

![](img/288a0c22d14d2450c1e772f228f867b0_608_6.png)

### The removal algorithm.

In summary, to remove an item I from a 2-3 tree, you first locate the node n that contains it. If n is not a leaf, you find I's inorder successor and swap it with I. As a result of the swap, the removal always begins at a leaf. If the leaf contains an item in addition to I, you simply remove I and you are done. On the other hand, if the leaf contains only I, removing I would leave the leaf without a data item. In this case you must perform some additional work to complete the removal.

You first check the siblings of the now-empty leaf. If sibling has two items, you redistribute the items among the sibling, the empty leaf, and the leaf's parent, as Figure 19-19a illustrates. If no sibling of the leaf has two items, you merge the leaf with an adjacent sibling by moving an item down from the leaf's parent into the sibling—it had only one item before, so it has room for another—and deleting the empty leaf. This case is shown in Figure 19-19b.

### Redistribute values

By moving an item down from a node n, as just described, you might cause n to be left without a data item and with only one child. If so, you recursively apply the removal algorithm to n. Thus, if n has a sibling with two items—and three children—you redistribute the items among n, the sibling, and n's parent. You also give n one of its sibling's children, as Figure 19-19c indicates.

If n has no sibling with two items, you merge n with a sibling, as Figure 19-19d illustrates. That is, you move an item down from the parent and let the sibling adopt n's one child. (At this point you know that the sibling previously had only one item and two children.) You then delete the empty leaf. If the merge causes n's parent to be without an item, you recursively apply the removal process to it.

### Merge nodes

If the merging continues so that the root of the tree is without an item—and has only one child—you simply delete the root. When this step occurs, the height of the tree is reduced by 1, as Figure 19-19e illustrates.

A high-level statement of the algorithm for removing data from a 2-3 tree follows:

```
// Removes the given data item from a 2-3 tree. Returns true if successful
// or false if no such item exists.
removeItem(23Tree: TwoThreeTree, dataItem: ItemType): boolean
    Attempt to locate dataItem
    if (dataItem is found)
    {
        if (dataItem is not in a leaf)
            Swap dataItem with its inorder successor, which will be in a leaf leafNode
        // The removal always begins at a leaf
        Remove dataItem from leaf leafNode
        if (leafNode now has no items)
            fixTree(leafNode)
        return true
    }
    else
        return false
// Completes the removal when node n is empty by either deleting the root,
// redistributing values, or merging nodes. Note: If n is internal, it has one child.
fixTree(n: TwoThreeTree)
    if (n is the root)
        Delete the root
    else
    {
        Let p be the parent of n
        if (some sibling of n has two items)
            Distribute items appropriately among n, the sibling, and p
    }
```

2-3 tree removal algorithm
