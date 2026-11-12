# 19.1 Balanced Search Trees

As you saw in the previous chapter, the efficiency of the binary search tree implementation of the ADT dictionary is related to the tree's height. The operations add, remove, and getItem follow a path from the root of the tree to the node that contains the desired item (or, in the case of the add operation, to the node that is to become the parent of the new item). At each node along the path, you compare a given value to the search key in the node and determine which subtree to search next. Because the maximum number of nodes on such a path is equal to the height of the tree, the maximum number of comparisons that the dictionary operations can require is also equal to this height.

As you know, the height of a binary search tree of n nodes ranges from a maximum of n to a minimum of ⌊log(n + 1)⌋ As a consequence, locating a particular item in a binary search tree requires between n and ⌊log(n + 1)⌋ comparisons. Thus, a search of a binary search tree can be as inefficient as a sequential search of a chain of linked nodes or as efficient as a binary search of a sorted array. Efficiency was the primary reason for developing the binary search tree implementation of the dictionary: We wanted to perform a search of a linked structure as efficiently as we could perform a binary search of an array. Thus, we certainly want the optimum behavior of the binary search tree.

What affects the height of a binary search tree? As you learned in Chapters 15 and 16, the height of the tree is quite sensitive to the order in which you insert or remove items. For example, consider a binary search tree that contains the items 10, 20, 30, 40, 50, 60, and 70. If you inserted the items into the tree in ascending order, you would obtain a binary search tree of maximum height, as shown in Figure 19-1a. If, on the other hand, you inserted the items in the order 40, 20, 60, 10, 30, 50, 70, you would obtain a balanced binary search tree of minimum height, as shown in Figure 19-1b.

As you can see, if you use the algorithms in Chapter 16 to maintain a binary search tree, insertions and removals can cause the tree to lose its balance and approach a linear shape. Such a tree is no better than a linear chain of linked nodes. For this reason, it is desirable in many applications to use one of

The height of a binary search tree is sensitive to the order of insertions and removals

Various search trees can retain their balance despite insertions and removals

# FIGURE 19-1 (a) A binary search tree of maximum height; (b) a binary search tree of minimum height

![](bbox=[0.255, 0.565, 0.555, 0.925])

![](bbox=[0.605, 0.565, 0.895, 0.755])