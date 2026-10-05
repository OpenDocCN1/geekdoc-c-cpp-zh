When you remove that node, you must also remove the value 6 that was used to decide when to move left from node B to the node containing 5. The third tree in Figure 11-9 shows the situation.

![](bbox=[0.185, 0.163, 0.814, 0.653])

**Figure 11-9:** When you delete a value from a node in a 2-3 tree, sometimes a node that is empty can borrow values from its sibling.

At this point, the value 6 doesn't have a node, and the values in the tree are no longer in sorted order. The value 6 is greater than any value in A's subtree, so move it to A's parent. The value that was in that position (3 in this example) is greater than the values in A's original subtree and less than the value borrowed from its sibling (5), so put 3 to the left of the borrowed value.
The bottom tree in Figure 11-9 shows the final result.

One more situation may occur when you delete a value. Suppose you remove a value from a node, so the node then has only one child, and the node's sibling contains only one value, so you can't borrow a node from it. In that case you can merge the node and its sibling. (Not surprisingly, this is called a node merge)