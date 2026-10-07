# ABSTRACT DATA STRUCTURES

![](bbox=[0.147, 0.083, 0.83, 0.363])

Figure 9.9 A binary search tree

5 6 7 8 9 10 11 12 13 15 18 25

Note that the order of entry for the key values has produced the heap shown in Figure 9.1. An application of heapSort rearranges its elements in numerically ascending order.

# 9.4 ADT ordered set

Heaps are used to store ordered sets when only a few operations are necessary. In some situations it may be useful to have more information about the elements stored in the data structure. For example, the operations next or previous that return an element's successor or predecessor, respectively, are not easy to implement efficiently on a heap. The ADT ordered set provides a structure that is more amenable to these and several other operations. An ordered set requires the operations

+   - makeOrderedSet() creates a new ordered set,
- getMax() and getMin(), methods that return the ordered set elements with the largest and smallest keys,
- lookup(key) that performs a look-up of the specified key in the data structure and
- insert(key,object) that inserts an object with a specified key.

The basic structure that implements ADT ordered set is called a binary search tree. This can be visualized as a binary tree in which each node contains a member of the ordered set. The elements are arranged in the tree according to their keys so that they satisfy an order property: the key value of the node's left child is no larger than that of the node itself and the key value of a node's right child is no smaller than that of the node itself. In contrast to the previous ADTs we have considered, binary trees are nonlinear in nature; that is, the data is not stored in a sequence as it is for, e.g., dynamic arrays and lists.

Figure 9.9 shows an example of a binary search tree. The nodes are composed of (key, data) pairs with both the key and data objects integers.

To find the node with the minimum key in a binary search tree, descend from the root to its left child and continue descending until reaching a node without a left child. This node’s key value is the minimum of the set. The idea is summarized in Algorithm 9.16.