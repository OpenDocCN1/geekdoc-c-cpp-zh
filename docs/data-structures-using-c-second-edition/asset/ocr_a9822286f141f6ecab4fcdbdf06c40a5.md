All the key values cannot be easily represented as strings. For example, the same floating point number can be represented as a string in multiple ways (1 is equivalent to 1.0, 1.00, +1.0, etc.).

# Applications

Tries are commonly used to store a dictionary (for example, on a mobile telephone). These applications take advantage of a trie’s ability to quickly search, insert, and delete the entries. Tries are also used to implement approximate matching algorithms, including those used in spell-checking software.

# POINTS TO REMEMBER

+   • An M-way search tree has M – 1 values per node and m sub-trees. In such a tree, m is called the degree of the tree. M-way search tree consists of pointers to M sub-trees and contains M – 1 keys, where m > 2.
+   • A B tree of order m can have a maximum of m–1 keys and m pointers to its sub-trees. A B tree may contain a larger number of key values and pointers to its sub-trees.
+   • A B+ tree is a variant of B tree which stores sorted data in a way that allows for efficient insertion, retrieval, and removal of records, each of which is identified by a key. B+ tree record data at the

+   • leaf level of the tree; only keys are stored in interior nodes.
+   • A trie is an ordered tree data structure which stores keys that are usually strings. It is basically a k-ary position tree.
+   • In contrast to binary search trees, nodes in a trie do not store the keys associated with them. Rather, a node’s position in the tree represents the key associated with that node.
+   • In a 2-3 tree, each interior node has either two or three children. This means that a 2-3 tree is not a binary tree.

# EXERCISES

# Review Questions

+   1. Why is a large value of n needed in a B tree?
+   2. Compare B trees with B+ trees.
+   3. In what conditions will you prefer a B+ tree over a B tree?
+   4. Write a short note on trie data structure.
+   5. Compare binary search trees with trie. Also, list the merits and demerits of using the trie data structure.
+   6. Compare hash tables with trie.

+   7. Give a brief summary of M-way search trees.
+   8. Consider the B tree given below
+      (a) Insert 1, 5, 7, 11, 13, 15, 17, and 19 in the tree.
+      (b) Delete 30, 59, and 67 from the tree.
+   9. Write an essay on B+ trees.
+   10. Create a B+ tree of order 5 for the following data arriving in sequence:
+       90, 20, 7, 9, 18, 21, 3, 4, 16, 11, 21, 72

![](bbox=[0.18, 0.74, 0.82, 0.84])

+   11. List down the applications of B trees.
+   12. B trees of order 2 are all full binary trees. Justify this statement.

+   13. Consider the 3-way search tree given below. Insert 23, 45, 67, 87, 54, 32, and 11 in the tree. Then, delete 9, 36, and 54 from it.