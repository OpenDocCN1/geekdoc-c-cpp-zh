Each node in the binary search tree is itself the root of the nodes descending from it, making the node and its descendants a subtree. In Figure 17.12, for example, the nodes containing the words fate, carpet, and llama form the left subtree of the whole tree, and the word voyage is the right subtree of the style-plenum-voyage subtree.

Suppose you want to find an item—call it the target—in such a tree. If the item precedes the root item, you need to search only the left half of the tree, and if the target follows the root item, you need to search only the right subtree of the root node. Therefore, one comparison eliminates half the tree. That means comparing the target with the item in the left child. If the target precedes the left-child item, you need to search only the left half of its descendants, and so on. As with the binary search, each comparison cuts the number of potential matches in half.

Let’s apply this method to see whether the word puppy is in the tree shown in Figure 17.12. Comparing puppy to melon (the root node item), you see that puppy, if present, must be in the right half of the tree. Therefore, you go to the right child and compare puppy to style. In this case, puppy precedes the node item, so you must follow the link to the left node. There you find plenum, which precedes puppy. You now have to follow the right branch for that node, but it is empty, so three comparisons show you that puppy is not in the tree.

A binary search tree, then, combines a linked structure with binary search efficiency. The programming price that is putting a tree together is more involved than creating a linked list.

Let’s make a binary tree for the next, and final, ADT project.

# A Binary Tree ADT

As usual, we’ll start by defining a binary tree in general terms. This particular definition assumes the tree contains no duplicate items. Many of the operations are the same as list operations. The difference is in the hierarchical arrangement of data. Here is an informal summary of this ADT:

+   **Type Name:** Binary Search Tree
+   
+   **Type Properties:** A binary tree is either an empty set of nodes (an empty tree) or a set of nodes with one node designated the root. Each node has exactly two trees, called the left subtree and the right subtree, descending from it. Each subtree is itself a binary tree, which includes the possibility of being an empty tree. A binary search tree is an ordered binary tree in which each node contains an item, in which all items in the left subtree precede the root item, and in which the root item precedes all items in the right subtree.
+   
+   **Type Operations:**
+   - Initializing tree to empty.
+   - Determining whether tree is empty.
+   - Determining whether tree is full.