threaded tree in the rest of our chapter.

# 8.2.1 Need of a threaded tree

It is apparent from our earlier discussion that the leaf doesn't have the child. Consequently, it's left and right pointer represents the NULL. Number of NULL pointers increases with the increase in level. Traversal, only in one direction is the other major limitation of a BST. To address all these issues, threaded tree is used. In the threaded tree, we connect the NULL pointers of the leaf as follows:

+   - Left pointer is connected to the in-order predecessor.
+   - Right pointer is connected to the in-order successor.
+   - If no predecessor or successor is present, in that case NULL pointer is connected to the root node.

Attachment of pointers to the predecessor and successor not only eliminates the NULL pointer, but also facilitates in backward traversal. In the rest of our discussion, we have considered the in-threaded tree. Once the readers can implement the in-threaded tree, implementing the left-in threaded tree or the right-in threaded tree can easily be mapped.

# 8.2.2 Creation of a threaded tree

In-threaded tree is popularly known as threaded tree. Structure of a threaded tree and the insertion of a node have been discussed in the following sub-section.

# 8.2.2.1 Representing the in-threaded tree

In-threaded tree is the advance version of a BST in which two additional components are also included. In addition to left and right pointer, provision for two threads i.e. left thread and right thread also managed. Complete structure of the in-threaded tree has been illustrated in the figure 8.1.

| lthread | Left node | Data | rightNode | rthread |

Figure 8-1: Structure of an in-threaded tree

In the above figure, symbols used have the following meaning:

lthread: denotes the left thread

leftnode: denotes the left node

info: data part of the tree

rightnode denotes the right node

rthread denotes the right thread