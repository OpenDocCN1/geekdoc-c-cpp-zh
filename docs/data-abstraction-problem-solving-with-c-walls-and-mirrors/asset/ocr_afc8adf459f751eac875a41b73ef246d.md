# 2-3 Trees 583

removals affected only one part of the binary tree, causing it to lose its balance. The left-subtree has not been affected at all, and the overall height of the tree has not been diminished.

The removal algorithm. In summary, to remove an item I from a 2-3 tree, you first locate the node n contains it. If n is not a leaf, you insert I into its successor and swap with I. As a result of the swap, the removal always begins at a leaf. If the leaf contains an item in addition to I, you simply remove I and do nothing. On the other hand, if the leaf contains only I, removing leave the leaf without a data item. In this case you must perform some additional work to complete the removal.

You check the siblings of the non-empty leaf. If it has siblings, you redistribute the items among the sibling, the leaf, and its parent, as shown in Figure 19-9a. If no sibling of the leaf has two items, you merge the leaf with sibling by moving an item from the leaf into the sibling—it had only one item, so it has room for another—and deleting the leaf. This case is shown in Figure 19-9b.

![](bbox=[0.778, 0.173, 0.938, 0.253])

By moving down from node n, as just described, you might cause n to be without a data item and with one child. If so, you recursively apply the algorithm to n. Thus, if n has a sibling with two and children—you redistribute the items among n, the sibling, and n’s parent. Also you give n one of its's children, as shown in Figure 19-9c.

If n has no sibling with two items, you merge n with sibling, as shown in Figure 19-9d. (At this point the knowing leaf had only one item and children). You then delete the empty leaf. If the merge causes n’s parent to be without it, you recursively apply the process to it.

If the merging continues until the root of the tree is without an item—and has only one child—you simply delete the root. When this occurs, the height of the tree is reduced by 1,

![](bbox=[0.778, 0.313, 0.938, 0.393])

A high-level description of the algorithm for removing data item from a 2-3 tree follows:

![](bbox=[0.778, 0.513, 0.938, 0.563])

```
// Removes the given item from a 2-3 tree. Returns true if successful
// or false if no such item exists.
removeItem(2Tree tree, dataItem: ItemType): boolean {
  Attempt to locate dataitem(dataItem)
  if (item is found) {
    if (data is not in a leaf) {
      Swap data with its successor, which will be in a leaf leafNode
      Remove dataItem from leaf leafNode
      if (leafNode has no items) {
        return true
      }
    } else {
      return false
    }
  }
  // Completes the removal when node n is empty by deleting the root,
  // redistributing values, or merging nodes. If n is internal, it has one child.
  fixTree(n: TwoNode)
  if (n is the root) {
    Delete the root
  } else {
    Let p be the parent of n
    if (some sibling of n has two items) {
      Distribute items appropriately among n, the sibling, and p
```