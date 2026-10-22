
- (c) The records arrive with values having a uniform random distribution (so the BST is likely to be well balanced). 1000 insertions are interspersed with 1000 searches.

- (d) The records arrive with values having a uniform random distribution (so the BST is likely to be well balanced). 1000 insertions are performed, followed by 1,000,000 searches.

## 5.9 Projects

- 5.1 Re-implement the composite design for the binary tree node class of Figure 5.11 using a flyweight in place of NULL pointers to empty nodes.

- 5.2 One way to deal with the “problem” of NULL pointers in binary trees is to use that space for some other purpose. One example is the threaded binary tree. Extending the node implementation of Figure 5.7, the threaded binary tree stores with each node two additional bit fields that indicate if the child pointers `lc` and `rc` are regular pointers to child nodes or threads. If `lc` is not a pointer to a non-empty child (i.e., if it would be NULL in a regular binary tree), then it instead stores a pointer to the inorder predecessor of that node. The inorder predecessor is the node that would be printed immediately before the current node in an inorder traversal. If `rc` is not a pointer to a non-empty child, then it instead stores a pointer to the node’s inorder successor. The inorder successor is the node that would be printed immediately after the current node in an inorder traversal. The main advantage of threaded binary trees is that operations such as inorder traversal can be implemented without using recursion or a stack. Re-implement the BST as a threaded binary tree, and include a non-recursive version of the preorder traversal.

- 5.3 Implement a city database using a BST to store the database records. Each database record contains the name of the city (a string of arbitrary length) and the coordinates of the city expressed as integer x- and y-coordinates. The BST should be organized by city name. Your database should allow records to be inserted, deleted by name or coordinate, and searched by name or coordinate. Another operation that should be supported is to print all records within a given distance of a specified point. Collect running-time statistics for each operation. Which operations can be implemented reasonably efficiently (i.e., in Θ(log n) time in the average case) using a BST? Can the database system be made more efficient by using one or more additional BSTs to organize the records by location?

- 5.4 Create a binary tree ADT that includes generic traversal methods that take a visitor, as described in Section 5.2. Write functions count and BSTcheck of Section 5.2 as visitors to be used with the generic traversal method.

- 5.5 Implement a priority queue class based on the max-heap class implementation of Figure 5.19. The following methods should be supported for manipulating the priority queue:

  ```cpp
  void enqueue(int ObjectID, int priority);
  int dequeue();
  void changeweight(int ObjectID, int newPriority);
  ```

  Method `enqueue` inserts a new object into the priority queue with ID number ObjectID and priority priority. Method `dequeue` removes the object with highest priority from the priority queue and returns its object ID. Method `changeweight` changes the priority of the object with ID number ObjectID to be newPriority. The type for `E` should be a class that stores the object ID and the priority for that object. You will need a mechanism for finding the position of the desired object within the heap. Use an array, storing the object with ObjectID i in position i. (Be sure in your testing to keep the ObjectIDs within the array bounds.) You must also modify the heap implementation to store the object’s position in the auxiliary array so that updates to objects in the heap can be updated as well in the array.

- 5.6 The Huffman coding tree function `buildHuff` of Figure 5.29 manipulates a sorted list. This could result in a Θ(n²) algorithm, because placing an intermediate Huffman tree on the list could take Θ(n) time. Revise this algorithm to use a priority queue based on a min-heap instead of a list.

- 5.7 Complete the implementation of the Huffman coding tree, building on the code presented in Section 5.6. Include a function to compute and store in a table the codes for each letter, and functions to encode and decode messages. This project can be further extended to support file compression. To do so requires adding two steps: (1) Read through the input file to generate actual frequencies for all letters in the file; and (2) store a representation for the Huffman tree at the beginning of the encoded output file to be used by the decoding function. If you have trouble with devising such a representation, see Section 6.5.

## Non-Binary Trees

Many organizations are hierarchical in nature, such as the military and most businesses. Consider a company with a president and some number of vice presidents who report to the president. Each vice president has some number of direct subordinates, and so on. If we wanted to model this company with a data structure, it would be natural to think of the president in the root node of a tree, the vice presidents at level 1, and their subordinates at lower levels in the tree as we go down the organizational hierarchy.

Because the number of vice presidents is likely to be more than two, this company’s organization cannot easily be represented by a binary tree. We need instead to use a tree whose nodes have an arbitrary number of children. Unfortunately, when we permit trees to have nodes with an arbitrary number of children, they become much harder to implement than binary trees. We consider such trees in this chapter. To distinguish them from binary trees, we use the term general tree.

Section 6.1 presents general tree terminology. Section 6.2 presents a simple representation for solving the important problem of processing equivalence classes. Several pointer-based implementations for general trees are covered in Section 6.3. Aside from general trees and binary trees, there are also uses for trees whose internal nodes have a fixed number K of children where K is something other than two. Such trees are known as K-ary trees. Section 6.4 generalizes the properties of binary trees to K-ary trees. Sequential representations, useful for applications such as storing trees on disk, are covered in Section 6.5.

### 6.1 General Tree Definitions and Terminology

A tree T is a finite set of one or more nodes such that there is one designated node R, called the root of T. If the set (T − {R}) is not empty, these nodes are partitioned into n > 0 disjoint subsets T0, T1, ..., Tn−1, each of which is a tree, and whose roots R1, R2, ..., Rn, respectively, are children of R. The subsets Ti (0 ≤ i < n) are said to be subtrees of T. These subtrees are ordered in that Ti is said to come before Tj if i < j. By convention, the subtrees are arranged from left to right with subtree T0 called the leftmost child of R. A node’s out degree is the number of children for that node. A forest is a collection of one or more trees. Figure 6.1 presents further tree notation generalized from the notation for binary trees presented in Chapter 5.

![](img/7ea3c39173f146f675b63b146d1535f3_222_0.png)

Figure 6.1 Notation for general trees. Node P is the parent of nodes V, S1, and S2. Thus, V, S1, and S2 are children of P. Nodes R and P are ancestors of V. Nodes V, S1, and S2 are called siblings. The oval surrounds the subtree having V as its root.

Each node in a tree has precisely one parent, except for the root, which has no parent. From this observation, it immediately follows that a tree with n nodes must have n − 1 edges because each node, aside from the root, has one edge connecting that node to its parent.

#### 6.1.1 An ADT for General Tree Nodes

Before discussing general tree implementations, we should first make precise what operations such implementations must support. Any implementation must be able to initialize a tree. Given a tree, we need access to the root of that tree. There must be some way to access the children of a node. In the case of the ADT for binary tree nodes, this was done by providing member functions that give explicit access to the left and right child pointers. Unfortunately, because we do not know in advance how many children a given node will have in the general tree, we cannot give explicit functions to access each child. An alternative must be found that works for an unknown number of children.
