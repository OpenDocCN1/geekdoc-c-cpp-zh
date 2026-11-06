+   - When removing a node with only one child from a binary search tree, the child replaces the node to be removed.
+   - When removing a node with two children from a binary search tree, replace it with the smallest node of the right subtree.
+   - If a binary search tree is balanced, then inserting an element takes O(log(n)) time.
+   - Tree traversal schemes include preorder traversal, inorder traversal, and postorder traversal.

# Describe the map data type and its implementation in the C++ library.

+   - A map keeps associations between key and value objects.
+   - A multimap can have multiple values associated with the same key.

# Describe the behavior of the priority queue data type.

+   - When removing an element from a priority queue, the element with the highest priority is retrieved.

# Describe the heap data structure and the efficiency of its operations.

+   - A heap is an almost complete tree in which the values of all nodes are at least as large as those of their descendants.
+   - Inserting or removing a heap element is an O(log(n)) operation.
+   - The regular layout of a heap makes it possible to store heap nodes efficiently in an array.

# REVIEW EXERCISES

+   - **R14.1** A school web site keeps a collection of web sites that are blocked at student computers. Should the program that checks for blocked sites use a vector, linked list, list, or set for storing the site addresses?
+   - **R14.2** A library wants to track which books are checked out to which patrons. Should they use a map or a multimap from books to patrons?
+   - **R14.3** A library wants to track which patrons have checked out which books. Should they use a map or a multimap from patrons to books?
+   - **R14.4** In an emergency, a case record is made for each incoming patient that describes the severity of the case. When doctors become available, they handle the most severe cases first. Should the case records be stored in a set, a map, or a priority queue?
+   - **R14.5** You keep a set of Point objects for a scientific experiment. (A Point has x and y coordinates.) Define a suitable operator< so that you can form a set<Point>.
+   - **R14.6** A set<T> can be implemented as a binary tree whose nodes store data of type T. How can you implement a multiset<T>?
+   - **R14.7** What is the difference between a binary tree and a binary search tree? Give examples of each.