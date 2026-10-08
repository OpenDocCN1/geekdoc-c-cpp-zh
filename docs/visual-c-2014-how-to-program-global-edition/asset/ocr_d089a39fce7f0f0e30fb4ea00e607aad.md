# 19.7 Trees

many elements at the previous level. Figure 19.22 is a tightly packed binary tree. A tightly packed binary search tree with n elements has a minimum of log n levels. For such a tree, at most, n comparisons are required either to find a match or to determine that no match exists. Searching a (tightly packed) 1000-element binary search tree requires most 10 comparisons, because 2¹⁰ > 1000. Searching a (tightly packed) 1,000,000-element binary search tree requires at most 20 comparisons, because 2²⁰ > 1,000,000.

# Overview of the Level-Order-Binary-Tree Exercise

The chapter exercises present the algorithm for a level-order traversal of a binary tree, which visits the nodes of the tree row by row, starting at the root-node level. On each level of the tree, a level-order traversal visits the nodes from left to right.

# 19.7.2 Binary Search Tree of IComparable Objects

The binary-tree example in Section 19.7.1 works when all the data is of type int. Suppose you want to manipulate a binary tree of doubles. You could rewrite the TreeNode and Tree classes with different names and customize the classes to manipulate doubles. Similarly, for each data type you could create customized versions of classes TreeNode and Tree. This proliferates code, and can become difficult to manage and maintain.

Ideally, we’d like to define the binary tree’s functionality once and reuse it for many types. Languages like C# enable all objects to be manipulated in a uniform manner. Using such capabilities enables us to design a more flexible data structure. C# provides these capabilities using generics (Chapter 20).

In our next example, we take advantage of C#’s polymorphic capabilities by implementing TreeNode and Tree classes that manipulate objects of any type that implements interface IComparable (namespace System). It is imperative that we be able to compare objects stored in a binary search tree, so we can determine the path to the insertion point of a new class. Classes that implement IComparable method CompareTo the object that the method receives as an argument. The method returns an int value less than zero if the calling object is less than the argument object, a positive value if the calling object is greater than the argument object. Also, both the calling and argument objects must be of the same data type; otherwise the method throws an ArgumentException.

Figures 19.23–19.24 enhance the program of Section 19.7.1 to implement objects. On the new versions of classes TreeNode and Tree is that each tree object can contain objects of any type (e.g., all strings or doubles). If a program attempts to insert multiple types in the same tree of class TreeNode (lines 14, 20, 27, 29 and 41 of 19.23) and one line of code in class Tree (line 64) to enable insertion of IComparable objects, exceptions will occur. For lines 30 and 42, all changes replace replaced int with the < and > operators to compare the value being inserted with the value in a new node. These lines now compare IComparable objects via the interface CompareTo method then the method’s return value to determine whether it’s less than zero (the calling object is less than the argument object) or greater than zero (the calling object is greater than the argument object), respectively.

[Note: If this class was written using generics (Chapter 20), the type of data, int or