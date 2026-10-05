
# Chapter 10 ※ Trees 271

The performance of many tree algorithms is related to the tree's height. If a tree holding N nodes is relatively short and wide, its height is O(log N), and those algorithms are fairly quick. If the tree is tall and thin, it could have height O(N), and some of those perform well. For example, building a sorted binary tree takes O(N × log N) time in the best case and O(N²) in the worst case.

Because a tree's height is important to these algorithms, special trees have been devised to rebalance themselves so that they cannot grow too tall and thin. The next chapter describes several kinds of balanced trees, including the B-trees and B+trees used by many database systems to store and search indices efficiently.

## Exercises

Asterisks indicate particularly difficult problems.

- 1. Can a perfect binary tree hold an even number of nodes?
- 2. A perfect tree is full and complete, although not all full and complete trees are perfect. Draw a tree that is full and complete but not perfect.
- 3. Use induction to prove that the number of branches B in a binary tree containing N nodes is B = N - 1.
- 4. Prove that the number of branches B in a binary tree containing N nodes is B = N - 1 without using induction.
- 5. *Use induction to prove that the number of leaf nodes L in a perfect tree of height H is L = 2H.
- 6. **Induction to prove that the number of missing branches (places where a child could be added) M in a binary tree that contains N nodes is M = N + 1.
- 7. What is the preorder traversal for the tree shown in Figure 10-24?

![](img/fefa42765c0b410af6705110aea7c0cb_294_0.png)

Figure 10-24: Tree data structures usually are drawn with the root at the top.

- 8. What is the inorder traversal for the tree shown in Figure 10-24?
- 9. What is the postorder traversal for the tree shown in Figure 10-24?
- 10. What is the depth-first traversal for the tree shown in Figure 10-24?
- 11. Write a program that finds the preorder, inorder, postorder, and depth-first traversals for the tree shown in Figure 10-24.
- 12. What happens if you use a queue instead of a stack in the depth-first traversal algorithm described in the section “Depth-first Traversal?” How could you generate the same traversal recursively?
- 13. Write a program similar to the one shown in Figure 10-25 that uses a preorder traversal to display a textual representation of the tree shown in Figure 10-24.

![](img/fefa42765c0b410af6705110aea7c0cb_295_0.png)

**Figure 10-25:** A preorder traversal can generate a textual display of a tree similar to the one used by Windows Explorer to display a directory hierarchy.

- 14. **Write a program similar to the one shown in Figure 10-26 to display a more intuitive picture of a tree. (Hints: Give the node class a PositionSubtree method that positions the node’s subtree. It should take as parameters the minimum x and y-coordinates that the node’s subtree can occupy, and it should calculate the rectangle that the subtree will cover. It will need to recursively call the PositionSubtree method of its left and right child subtrees and use the subtrees’ sizes to see how big to make the original subtree. Also give the node class methods to recursively draw the tree’s links and nodes.)

![](img/fefa42765c0b410af6705110aea7c0cb_296_0.png)

**Figure 10-26:** To draw a tree, a program must first position it.

- 15. **The tree shown in Figure 10-26 is particularly useful for unordered trees, but for ordered binary trees it can be hard to tell whether a node is the left or right child of its parent. For example, in Figure 10-26 it's unclear whether node C is the left or right child of node D.**

Modify the program you wrote for Exercise 14 to produce a display similar to the one shown in Figure 10-27. Here, if a node has only one child, the program allows some space for the missing child, so you can tell whether the other child is a left or right child.

![](img/fefa42765c0b410af6705110aea7c0cb_296_1.png)

**Figure 10-27:** In an ordered binary tree, you can leave space to indicate missing children.

- 16. Write pseudocode to perform a reverse inorder traversal on a threaded sorted tree.
- 17. *Write a program that builds a threaded sorted tree and displays its inorder and reverse inorder traversals.

- 18. **Expand the program you built for Exercise 17 so that it displays the value shown in Figure 10-28. The circles in the drawing show a node's value and the values of the nodes to which its threads lead. For example, node 4 has its left thread set to null (displayed as -- in the program) and its right thread pointing to node 5.

![](img/fefa42765c0b410af6705110aea7c0cb_297_0.png)

**Figure 10-28:** This program builds and displays threaded sorted trees.

- 19. In general, is the knowledge tree used by the animal game full, perfect, none of those, or a combination of those?
- 20. The animal game can use the following node class to store information:

```
Class AnimalNode
  String: Question
  AnimalNode: YesChild, NoChild
End Class
```

If you use this class, can you tell whether a node represents a question or an animal?
- 21. Write a program that implements the animal game.
- 22. Draw expression trees for the following expressions:

- - (15 + 3) + (24 + 6)
- 8 × 12 - 14 × 32
- 1 + 2 + 1 + 4 + 1 + 20

- 23. Write a program that evaluates mathematical expressions. Because parsing expressions to build mathematical expression trees is deferred until Chapter 15, this program does not need to do that. Instead, make the program use code to build and evaluate the expressions in Exercise 22.
- 24. Draw expression trees for the following expressions:

- - $\sqrt{(36 \times 2)} \div (9 \times 32)$
- $5! + ((5 - 3)! \times 3!)$
- $Sine(45^\circ)^2$

- 25. Extend the program you wrote for Exercise 23 to evaluate the expressions in Exercise 24.
- 26. Write a program similar to the one shown in Figure 10-19. Let the user click to select a circle. If the user clicks all the circles, select no circle. When you draw the map, draw the selected circle (if there is one) in a different color.
- 27. Draw a trie to represent the following:

| KEY | VALUE |
| :--- | :--- |
| APPLE | 10 |
| APP | 20 |
| BEAR | 30 |
| ANT | 40 |
| BAT | 50 |
| APE | 60 |

- 28. **Write a program that adds and deletes from a trie.**

## Chapter 11 Balanced Trees

The performance of many tree algorithms is related to the tree's height. If a tree holding N nodes is relatively short and wide, its height is O(log N), and those algorithms are fairly quick. If the tree is tall and thin, it could have height O(N), and some of those perform well.

Because a tree's height is important to these algorithms, special trees have been devised to rebalance themselves so that they cannot grow too tall and thin. The next chapter describes several kinds of balanced trees, including the B-trees and B+trees used by many database systems to store and search indices efficiently.

## AVL Trees

An AVL tree is a sorted binary tree in which the heights of two subtrees at any given node differ by most 1. When a node is added or removed, the tree is rebalanced if necessary to ensure that the subtrees have heights differing by most 1.

> AVL trees are named after their inventors, G. M. Adelson-Velskii, and E. M. Landis. They were described in a 1962 paper and are the oldest type of balanced tree.

Because an AVL tree is a sorted binary tree, searching one is fairly easy. The previous chapter explained how to do so.

## Adding Values

Usually the implementation of the AVL tree node includes a balance factor that indicates whether node's subtrees are left-heavy, or right-heavy. You can define the balance factor as <height of left subtree> – <height of right subtree>. Therefore, a balance factor of -1 means the node is right-heavy, a balance factor of 0 means the two subtrees have the same height, and a balance factor of +1 means the node is left-heavy.

The basic strategy for adding a new node to an AVL tree is to recursively climb down the tree until you find the location where the new node belongs. As the recursion unwinds, the program updates the balance factors at each node as it returns to the root. If a program finds a node with a balance factor less than -1 or greater than +1, it uses one or more “rotations” to rebalance the subtrees at that node.

Which rotations the algorithm uses depends on which grandchild subtree contains the new node. If the node is in the left child's subtree, the left child's right subtree, the right child's right subtree,

The tree shown in Figure 11-1 illustrates the situation in which the new node is in the left child's subtree A. This is called a left-left case.

You can rebalance the tree by rotating it to the right, replacing node B with node A and moving subtree A2 so that it becomes the left subtree for node B. Figure 11-2 shows the result. This rebalancing is called a right rotation.
