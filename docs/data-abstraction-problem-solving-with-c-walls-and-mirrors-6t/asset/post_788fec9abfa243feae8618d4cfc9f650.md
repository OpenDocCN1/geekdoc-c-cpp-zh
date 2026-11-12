
If the height of the binary search tree is log2(n + 1), the efficiency of its operations is O(log n). However, what will the height of a binary search tree actually be? The factor that determines the height of a binary search tree is the order in which you perform insertion and removal operations on the tree. Recall that, starting with an empty tree, if you insert names in the order Alan, Bob, Elisa, Jane, Nancy, Tom, Wendy, you would obtain a binary search tree of maximum height, as shown in Figure 15-14b. On the other hand, if you insert names in the order Jane, Bob, Tom, Alan, Elisa, Nancy, Wendy, you would obtain a binary search tree of minimum height, as shown in Figure 15-13.

> Insertion in sorted order produces a maximum-height binary search tree

Which of these situations should you expect to encounter in the course of a real application? It can be proven mathematically that if the insertion and removal operations occur in a random order, the height of the binary search tree will be quite close to log2 n. Thus, in this sense, the previous analysis is not unduly optimistic. However, in a real-world application, it is realistic to expect the insertion and removal operations to occur in random order? In many applications, the answer is yes. There are, however, applications in which this assumption would be dubious. For example, the person preparing the previous sequence of names for the insertion operations might well decide to “help you out” by arranging the names to be inserted into sorted order. This arrangement, as has been mentioned, would lead to a tree of maximum height. Thus, while in many applications you can expect the behavior of a binary search tree to be excellent, you should be wary of the possibility of poor performance due to some characteristic of a given application.

> Insertion in random order produces a near-minimum-height binary search tree

Is there anything you can do if you suspect that the operations might not occur in a random order? Similarly, is there anything you can do if you have an enormous number of items and need to ensure that the height of the tree is close to log2 n? Chapter 19 presents variations of the basic binary search tree that are guaranteed always to remain balanced and therefore be of minimum height.

Figure 15-17 summarizes the order of the retrieval, insertion, removal, and traversal operations for the ADT binary search tree.

## FIGURE 15-17 The Big O for the retrieval, insertion, removal, and traversal operations for the ADT binary search tree

| Operation | Average case | Worst case |
|---|---|---|
| Retrieval | O(log n) | O(n) |
| Insertion | O(log n) | O(n) |
| Removal | O(log n) | O(n) |
| Traversal | O(n) | O(n) |

## SUMMARY

- 1. Binary trees provide a hierarchical organization of data, which is important in many applications.
- 2. Traversing a tree is a useful operation. Intuitively, traversing a tree means to visit every node in the tree. Because the meaning of “visit” is application dependent, you can pass a client-defined visit function to the traversal operation.
- 3. The binary search tree allows you to use a binary search-like algorithm to search for an item with a specified value.
- 4. Binary search trees come in many shapes. The height of a binary search tree with n nodes can range from a minimum of log2(n + 1) to a maximum of n. The shape of a binary search tree determines the efficiency of its operations. The closer a binary search tree is to a balanced tree (and the farther it is from a linear structure), the closer the behavior of the search algorithm will be to a binary search (and the farther it will be from the behavior of a linear search).
- 5. An inorder traversal of a binary search tree visits the tree’s nodes in sorted search-key order.

## EXERCISES

- 1. Consider the tree in Figure 15-18. What node or nodes are
  - a. The tree's root?
  - b. Parents?
  - c. Children of the parents in part b?
  - d. Siblings?
  - e. Ancestors of 50?
  - f. Descendants of 20?
  - g. Leaves?
- 2. What is the height of the tree in Figure 15-18?
- 3. Write preconditions and postconditions for the ADT binary search tree operations.

## FIGURE 15-18 A tree for Exercises 1, 2, 6, 7, 11, and 23

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_476_0.png)

- 4. What are the preorder, inorder, and postorder traversals of the binary tree in Figure 15-19?
- 5. Consider a method isLeaf that returns true if a binary tree is a one-node tree—that is, if it consists of only a leaf—and returns false otherwise.
  - a. Specify the method isLeaf.
  - b. If isLeaf were not a method of a class of binary trees, would a client of the class be able to implement isLeaf? Explain.
- 6. Starting with an empty binary search tree, in what order should you insert items to get the binary search tree in Figure 15-18?
- 7. Using the binary search tree in Figure 15-18, trace the search algorithm when it searches for
  - a. 30
  - b. 15
  In each case, list the nodes in the order in which the search visits them.
- 8. Is the tree in Figure 15-19 a binary search tree? Explain.

## FIGURE 15-19 A tree for Exercises 4 and 8

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_477_0.png)

- 9. Beginning with an empty binary search tree, what binary search tree is formed when you insert the following values in the order given?
  - a. W, T, N, J, E, B, A
  - b. W, T, N, A, B, E, J
  - c. A, B, W, J, N, T, E
  - d. B, T, E, A, N, W, J

- 10. Consider the binary search tree in Figure 15-20. The numbers simply label the nodes so that you can reference them; they do not indicate the contents of the nodes.
  - a. Without performing an inorder traversal, which node must contain the value that comes immediately after the value in the root? Explain.
  - b. In what order will an inorder traversal visit the nodes of this tree? Indicate this order by listing the labels of the nodes in the order that they are visited.

- 11. Consider the binary search tree in Figure 15-18. What tree results after you insert the nodes 80, 65, 75, 45, 35, and 25, in that order?

## FIGURE 15-20 A binary search tree for Exercise 10

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_477_1.png)

- 12. If duplicates are allowed in a binary search tree, it is important to have a convention that determines the relationship between the duplicates. Items that duplicate the root of a tree should either all be in the left subtree or all be in the right subtree, and, of course, this property must hold for every subtree. Why is this convention critical to the effective use of the binary search tree?

- 13. Consider a nonempty binary tree with two types of nodes: min nodes and max nodes. Each node has an integer value initially associated with it. This tree is a minimax tree and has a value, which we define as follows:
  - If the root is a min node, the value of the tree is equal to the minimum of
    - The integer stored in the root
    - The value of the left subtree, but only if it is nonempty
    - The value of the right subtree, but only if it is nonempty
  - If the root is a max node, the value of the tree is equal to the maximum of the above three values.
  - a. Compute the value of the minimax tree in Figure 15-21. Each node is labeled with its initial value.
  - b. Design a general solution for representing and evaluating these trees.

- 14. A binary search tree with a given set of data items can have several different structures that conform to the definition of a binary search tree. If you are given a list of data items, does at least one binary search tree whose preorder traversal matches the order of the items on your list always exist? Is there ever more than one binary search tree that has the given preorder traversal?

- 15. How many differently shaped n-node binary trees are possible? How many differently shaped n-node binary search trees are possible? (Write recursive definitions.)

- 16. Write pseudocode for a binary search tree method that visits all nodes whose data lies within a given range of values (such as all values between 100 and 1,000).

- 17. By using mathematical induction, prove that a full binary tree of height h >= 0 has 2^h - 1 nodes.

- 18. By using mathematical induction, prove that the maximum number of nodes in a binary tree of height h is 2^h - 1.

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_478_0.png)
