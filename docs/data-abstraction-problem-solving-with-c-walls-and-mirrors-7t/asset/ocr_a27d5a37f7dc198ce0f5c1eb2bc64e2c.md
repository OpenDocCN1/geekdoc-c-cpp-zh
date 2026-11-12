Split 4-nodes as they are encountered

reaching a leaf, the insertion algorithm for a 2-3-4 tree splits 4-nodes as soon as it encounters them on the way down the tree from the root to a leaf. As a result, when a 4-node is split and an item is moved up to the node's parent, the parent cannot possibly be a 4-node, and so it can accommodate another item.

As an example of the algorithm, consider the tree in Figure 19-22a. This one-node tree is the result of inserting 60, 30, and 10 into an initially empty 2-3-4 tree. We will now insert more data into this tree.

Insert 20. While determining the insertion point, you begin at the root and encounter the 4-node <10 30 60>, which you split by moving the middle value 30 up. Because the node is the root, you create a new root, move 30 into it, and attach two children, as Figure 19-22b illustrates. You continue the search for 20 by examining the left subtree of the root, because 20 is less than 30. The insertion results in the tree in Figure 19-22c.

# FIGURE 19-22 Inserting 20 into a one-node 2-3-4 tree (a) the original tree; (b) after splitting the node; (c) after inserting 20

![](bbox=[0.22, 0.36, 0.93, 0.47])

Insert 50 and 40. The insertions of 50 and 40 do not require split nodes and result in the tree in Figure 19-23.

# FIGURE 19-23 After inserting 50 and 40 into the tree in Figure 19-22c

![](bbox=[0.22, 0.56, 0.93, 0.65])

Insert 70. While searching Figure 19-23 for 70's insertion point, you encounter the 4-node <40 50 60>, because 70 is greater than 30. You split this 4-node by moving 50 up to the node's parent, <30>, to get the tree in Figure 19-24a. You then insert 70 into the leaf <60>, as Figure 19-24b illustrates.

# FIGURE 19-24 The steps for inserting 70 into the tree in Figure 19-23: (a) after splitting the 4-node; (b) after inserting 70

![](bbox=[0.22, 0.8, 0.93, 0.91])