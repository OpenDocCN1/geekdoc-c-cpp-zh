![](bbox=[0.219, 0.108, 0.783, 0.545])

# 13.3.3 B+ Tree

B+ trees are internal data structures. That is, the nodes contain whatever information is associated with the key as well as the key values. A variant of B-trees is often used as an index tree. A B-tree combines the features of ISAM and B-trees as follows:

+   1. In an index tree, the pointers in the internal nodes point to other index nodes.
+   2. The pointers in the leaf nodes are not nil, but rather point to where the information associated with each key is stored on disk.
+   3. Each key must appear in a leaf node.
+   4. B-trees whose keys are only in the internal nodes of the tree and whose pointers in the leaf nodes print to where the related information is stored externally are called B+ trees.
+   5. Leaves are connected to form a linked list of keys in sequential order.
+   6. It has two parts—the index part consists of interior nodes and the sequence set consists of leaf nodes.
+   7. B+ trees are used to store index sequential file organization; the key values in the sequence set are the key values of record collections.