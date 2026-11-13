The B tree of order 5 shown in Figure 13.6 is considered. To delete 89 from the tree as it is a leaf node element, Case 1 can be followed. Delete 89 and adjust its child pointer fields. To delete 40, a non-leaf node element, Case 2 can be followed. Replace 40 with 38 the largest element from its left subtree. Deleting 38 again follows Case 1. This is illustrated in Figure 13.8

![](bbox=[0.12, 0.18, 0.9, 0.44])

# (a) After deleting 89

![](bbox=[0.12, 0.48, 0.9, 0.75])

# (b) Delete 40

# **Figure 13.8** Deletion of 89 and 40 individually from B tree of order 5 shown in Figure 13.6

If the deletion of an element leaves less than the minimum number of elements in the corresponding nodes, then deletion becomes complicated. Cases 3 and 4 deal with such cases. Case 3: If deleting an element k from a node leaves it with less than its minimum number of elements, then elements can be borrowed from either of its sibling nodes. When the left subtree node is capable to spare the