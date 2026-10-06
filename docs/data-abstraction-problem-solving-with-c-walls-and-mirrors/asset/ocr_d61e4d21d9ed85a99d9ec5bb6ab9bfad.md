# FIGURE 21-13 A B-tree of degree 5

![](bbox=[0.285, 0.137, 0.58, 0.313])

This type of search tree is known as a B-tree of degree m and has the following characteristics:

+   - All leaves are at the same level.
- Each node contains between $m-1$ and $[m/2]$ records, and each internal node has one more child than its parent. An exception to this rule is that the root of the tree can contain as few as one record and have as few as two children. This exception is necessitated by the insertion and removal algorithms described next.

A 2-3 tree is a B-tree of degree 3. Furthermore, the manner in which the B-tree insertion and removal algorithms maintain the structure of the tree is a direct generalization of the 2-3 tree's strategy of splitting and merging nodes. These algorithms are illustrated next by means of example. Suppose that the index file is organized into a B-tree of degree 5—that 5 is the maximum and 3 is the minimum number of children that an internal node—other than the root—in the tree can carry. (Typically, a B-tree will be of a higher degree, but the diagrams would get out of hand!)

**Insertion into a B-tree.** To insert data with search 55 into the tree shown in Figure 21-13, you take the following steps:

+   **Insert the record into the data file.** If you find block $b$ in the data file into you can insert the new record. As was with the external hashing implementation, block is either a block with a vacant slot or a new block.
**Insert a corresponding index record into the index file.** You now insert the index record $<55, p>$ into the index file, which is a B-tree of degree 5. The first step is to locate the leaf of the tree in this index record determining by which the search for 55 would terminate.

Suppose that this is the leaf $L$ shown in Figure 21-1a. Conceptually, you insert the new index record into $L$, causing it to contain five records (Figure 21-14b). Since a node can contain only four records, you must split $L$ into $L_1$ and $L_2$. With an analogous to the splitting of a node in a 2-3 tree, $L$ gets the two records with the smallest key values, $L_2$ gets the two records with the largest key values, and the record with the middle key value (56) is moved to the parent $P$ (See Figure 21-14c).