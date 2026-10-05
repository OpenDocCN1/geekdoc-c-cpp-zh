# Chapter 11 = Balanced Trees

Just as searching in a B-tree is similar to searching in a 2-3 tree, adding and removing values in a B-tree is similar to adding and removing values in a 2-3 tree.

# Adding Values

To insert a value in a B-tree, locate the leaf node that should contain it. If that node contains fewer 2 × K values, simply add the new value.

If the node contains 2 × K values, there's no room for a new value. If any of the node's siblings contain 2 × K values, you can rearrange the values in the siblings so that the new value will fit.

For example, consider the tree shown at the top of Figure 11-12. Suppose you want to add the value 17. The leaf node that should hold the new value is full. In the tree at the bottom of the figure, the values in the node and its right sibling have been rearranged to make room for the new value. (Notice that the dividing value has been changed in the parent node.)

![](bbox=[0.13, 0.413, 0.474, 0.683])

Figure 11-12: Sometimes when you add a value to a full B-tree node, you can redistribute values among the node's siblings to make room.

If all the sibling nodes are full (or if you don't want to rearrange values among siblings, a potentially difficult task), you can split the node into two nodes that each contain 2 × K values. Add the new value to the node's existing values, move the middle value up to be the dividing value in the parent node, and put the remaining values in the two new nodes.

For example, consider the tree shown at the top of Figure 11-13. Suppose you want to add the value 34. The leaf node and its siblings are all full, so you cannot