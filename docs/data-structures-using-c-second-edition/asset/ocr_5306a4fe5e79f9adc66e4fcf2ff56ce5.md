![](bbox=[0.1, 0.1, 0.5, 0.22])

Figure 10.28 Linked representation of a binary tree

In the linked representation, a number of nodes contain a NULL pointer, either in their left or right fields or in both. This space that is wasted in storing a NULL pointer can be efficiently used to store some other useful piece of information. For example, the NULL entries can be replaced to store a pointer to the in-order predecessor or the in-order successor of the node. These special pointers are called threads and binary trees containing threads are called threaded trees. In the linked representation of a binary tree, threads will be denoted using arrows. There are many ways of threading a binary tree and each type may vary according to the way the tree is traversed. In this book, we will discuss in-order traversal of the tree. Apart from this, a threaded binary tree may correspond to one-way threading or a two-way threading.

![](bbox=[0.1, 0.25, 0.5, 0.38])

Figure 10.29 (a) Binary tree without threading

![](bbox=[0.1, 0.41, 0.5, 0.55])

Figure 10.29 (b) Linked representation of the binary tree (without threading)

will point to the in-order successor of the node. Such a one-way threaded tree is called a right-threaded binary tree. In a two-way threaded tree, also called a double-threaded tree, threads will appear in both the left and the right field of the node. While the left field will point to the in-order predecessor of the node, the right field will point to its successor. A two-way threaded binary tree is also called a fully threaded binary tree. One-way threading and two-way threading of binary trees are explained below. Figure 10.29 shows a binary tree without threading and its corresponding linked representation. The in-order traversal of the tree is given as 8, 4, 9, 2, 5, 1, 10, 11, 3, 7, 12

# One-way Threading

![](bbox=[0.1, 0.75, 0.5, 0.88])

Figure 10.30 (a) Linked representation of the binary tree with one-way threading

In one-way threading, a thread will appear either in the right field or the left field of the node. A one-way threaded tree is also called a single-threaded tree. If the thread appears in the left field, then the left field will be made to point to the in-order predecessor of the node. Such a one-way threaded tree is called a left-threaded binary tree. On the contrary, if the thread appears in the right field, then it

Figure 10.30 shows a binary tree with one-way threading and its corresponding linked representation. Node 5 contains a NULL pointer in its RIGHT field, so it will be replaced to point to node 1, which is its in-order successor. Similarly, the RIGHT field of node 8 will point to node 4, the RIGHT field of node 9 will point to node 2, the RIGHT field of node 10 will point to node