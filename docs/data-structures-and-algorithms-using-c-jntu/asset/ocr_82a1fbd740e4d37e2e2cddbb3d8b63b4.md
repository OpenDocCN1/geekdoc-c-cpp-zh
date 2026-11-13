+   1. The edges that connect an internal node and an external node must be black.
+   2. In every root node to an external node path no two consecutive red edges or pointers (or red nodes) should appear.
+   3. The number of black edges or pointers (or black nodes) in all root node to the external node path must be same.

On the path from a node to an external node, the number of black edges gives the rank of a node. Therefore, the rank of all external nodes is 0.

All through the chapter, red nodes are represented by normal circles, red edges are represented by thin lines, black nodes are represented by shaded circles and black edges are represented by thick lines.

![](bbox=[0.16, 0.28, 0.84, 0.52])

Figure 14.2 A red-black tree

The red-black tree shown in Figure 14.2 has the root node and all the external nodes are with black colour. In any root node to the external node path no two consecutive red nodes exist. It has three black nodes and two black pointers in every root node to external node path.

# 14.2 REPRESENTATION OF A RED-BLACK TREE

The node representation of a red-black tree is the same as that of a binary search tree because it is an extended binary search tree. As colour plays a vital role it is necessary to record the colour of either the node or two pointers that emerge from the node. Based on the method that is followed either one field or two fields for colour are added to the node structure.

The insert or delete operations may lead to the imbalance of the red-black tree. In rebalancing the tree, nodes may move up and down. In order to facilitate this movement, a field that holds a pointer to its parent node should be incorporated in the node structure of a red-black tree.

# 14.3 OPERATIONS

Among the numerous operations, the most frequently used search, insert and delete operations are explained.