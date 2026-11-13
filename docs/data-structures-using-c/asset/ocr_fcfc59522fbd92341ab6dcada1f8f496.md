A search for a record with a particular key value K is done in the following way. First, the key cylinder index is read into memory. In general, it has a few hundred entries, so it fits in one track. The cylinder index is searched to determine the required cylinder number, and then, for this cylinder, its surface index is read into memory and searched for the track. Then, this track is read in and searched for the key. For example, if we search for a record with the key 'Rohit', then the cylinder index tells that the record is either on cylinder 2 or not in the file. If the surface index of cylinder 2 is searched, then it shows that the record is either on surface 1 or not in the file. So in the second track t2, 1 is read and searched for. The desired record is found on this track. So the total number of disk accesses to get a record is three—one for the cylinder index, one for the surface index, and one for the track of records. If the track sizes are very large, then a sector index is maintained. If several disks are used to store a file, then a disk index is also maintained.

This method of maintaining a file and index is referred to as indexed sequential access method (ISAM). It is the simplest file organization for single key files but not useful for multiple key files.

# Hashed Indexing

The operations related to hashed indices are the same as those for hash tables. This has been discussed in detail in Chapter 11.

# 13.3 TYPES OF SEARCH TREES

We have studied BSTs (binary search trees), AVL trees, optimal binary search trees, and heaps in Chapter 7. These were binary trees with outgoing degree two. For large data, these trees grow to a great height. To avoid these problems, we retain the properties of BSTs and increase the outgoing degree more than two. In a BST, the node maintains two links for its left and right child, whereas in a multiway search tree, each node can maintain more than two links for its more than two subtrees. Such search trees have vast applications such as dictionary, spell checks, and external file indices.

# 13.3.1 Multiway Search Tree

Binary search trees generalize directly to multiway search trees. A multiway search tree is a tree of order m, where each node has utmost m children. Here m is an integer. If k <= m is the number of children, then the node contains exactly k - 1 keys, which partition all the keys in the subtrees into k subsets. If some of these subsets are empty, then the corresponding children in the tree are empty. Figure 13.2 shows a 5-way search tree.

We always want to construct a multiway search tree that will minimize file accesses. So the height of the tree should be as small as possible, for example, B-tree and B+ tree.