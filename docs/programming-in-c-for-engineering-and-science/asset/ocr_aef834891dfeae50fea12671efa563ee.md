+   - A tree consists of a finite collection of nodes linked together in such a way that if the tree is not empty, then one of the nodes, called the root, has no incoming links, but every other node in the tree can be reached from the root by following a unique sequence of consecutive links.
+   - A binary tree is a tree in which each node has at most two children.
+   - In a binary search tree, for each node, all of the values in its left subtree are smaller than the value in this node, which is less than all values in its right subtree.
+   - Inorder traversal visits the nodes in a BST in ascending order.

# Style Tips

+   - If a problem solution requires that values stored more recently will be needed before the values stored less recently, then a stack is the appropriate structure for storing these values. Stacks are LIFO (Last-In-First-Out) lists, because the operation to remove a value will always retrieve the value that was inserted most recently.
+   - If a problem solution requires that values will be needed in the order in which they were stored, then a queue is the appropriate structure for storing these values. Queues are FIFO (First-In-First-Out) lists, because the operation to remove a value from the queue will always retrieve the value that was inserted least recently.
+   - If a problem solution requires access, insertion, and deletion only at the ends of a list, a deque is an appropriate structure for storing these values. Deques are double-ended queues.
+   - If a problem solution requires fast access to arbitrary elements but also requires that the collection be allowed to grow and shrink due to frequent insertions and deletions, then a binary search tree (BST) may be the appropriate structure to use. BSTs are linked structures and thus can grow and shrink without excessive memory waste. And they can be searched in a binary-search manner, which (except when the tree becomes lopsided) is more efficient (O(log₂n)) than a linear search (O(n)).

# Warnings

+   1. STL's queue<T> container may wrap a deque<T> or a list<T> but not a vector<T>. Removing an element at the front of a vector<T> is too inefficient.
+   2. STL's priority_queue<T> container may wrap a deque<T> or a vector<T> but not a list<T>. It needs direct access to its elements.

# TEST YOURSELF

Section 16.1

+   1. Convert 1234 to a base-2 number.
+   2. Convert 1234 to a base-8 number.
+   3. Convert 1234 to a base-16 number.