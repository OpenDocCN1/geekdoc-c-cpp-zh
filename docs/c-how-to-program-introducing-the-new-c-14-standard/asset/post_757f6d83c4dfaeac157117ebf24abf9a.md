
## 19.6.6 `Tree` Member Function `insertNodeHelper`

The `Tree` class’s utility function `insertNodeHelper` (lines 37–58) is called by `insertNode` (lines 13–15) to recursively insert a node into the tree. A node can *only be inserted as a leaf node in a binary search tree*. If the tree is *empty*, a new `TreeNode` is created, initialized and inserted in the tree (lines 40–42).

If the tree is *not empty*, the program compares the value to be inserted with the `data` value in the *root node*. If the insert value is smaller (line 45), the program recursively calls `insertNodeHelper` (line 46) to insert the value in the *left subtree*. If the insert value is larger (line 50), the program recursively calls `insertNodeHelper` (line 51) to insert the value in the *right subtree*. If the value to be inserted is identical to the data value in the *root node*, the program prints the message `" dup"` (line 54) and returns *without inserting* the duplicate value into the tree. Note that `insertNode` passes the address of `rootPtr` to `insertNodeHelper` (line 14) so it can modify the value stored in `rootPtr` (i.e., the address of the *root node*). To receive a pointer to `rootPtr` (which is also a pointer), `insertNodeHelper`’s first argument is declared as a *pointer to a pointer* to a `TreeNode`.

## 19.6.7 `Tree` Traversal Functions

Member functions `preOrderTraversal` (lines 18–20), `inOrderTraversal` (lines 23–25) and `postOrderTraversal` (lines 28–30) traverse the tree and print the node values. For the purpose of the following discussion, we use the binary search tree in **Fig. 19.23**.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2338_0.png)

Fig. 19.23 A binary search tree.

### *Inorder Traversal Algorithm*

Function `inOrderTraversal` invokes utility function `inOrderHelper` (lines 70–76) to perform the inorder traversal of the binary tree. The steps for an inorder traversal are:

- 1. Traverse the *left subtree* with an inorder traversal. (This is performed by the call to `inOrderHelper` at line 72.)
- 2. Process the value in the node—i.e., print the node value (line 73).
- 3. Traverse the *right subtree* with an inorder traversal. (This is performed by the call to `inOrderHelper` at line 74.)

The value in a node is not processed until the values in its left subtree are processed, because each call to `inOrderHelper` immediately calls `inOrderHelper` again with the pointer to the *left subtree*. The inorder traversal of the tree in **Fig. 19.23** is

```text
6 13 17 27 33 42 48
```

The inorder traversal of a binary search tree prints the node values in *ascending* order. The process of creating a binary search tree actually *sorts* the data—thus, this process is called the **binary tree sort**.

### *Preorder Traversal Algorithm*

Function `preOrderTraversal` invokes utility function `preOrderHelper` (lines 61–67) to perform the preorder traversal of the binary tree. The steps for a preorder traversal are:

- 1. Process the value in the node (line 63).
- 2. Traverse the *left subtree* with a *preorder* traversal. (This is performed by the call to `preOrderHelper` at line 64.)
- 3. Traverse the *right subtree* with a *preorder* traversal. (This is performed by the call to `preOrderHelper` at line 65.)

The value in each node is processed as the node is visited. After the value in a given node is processed, the values in the *left subtree* are processed. Then the values in the *right subtree* are processed. The preorder traversal of the tree in Fig. 19.23 is

```text
27 13 6 17 42 33 48
```

### Postorder Traversal Algorithm

Function `postOrderTraversal` invokes utility function `postOrderHelper` (lines 79–85) to perform the postorder traversal of the binary tree. The steps for a postorder traversal are:

- 1. Traverse the *left subtree* with a postorder traversal. (This is performed by the call to `postOrderHelper` at line 81.)
- 2. Traverse the *right subtree* with a postorder traversal. (This is performed by the call to `postOrderHelper` at line 82.)
- 3. Process the value in the node (line 83).

The value in each node is not printed until the values of its children are printed. The `postOrderTraversal` of the tree in Fig. 19.23 is

```text
6 17 13 33 48 42 27
```

## 19.6.8 Duplicate Elimination

The binary search tree facilitates **duplicate elimination**. As the tree is being created, an attempt to insert a duplicate value will be recognized, because a duplicate will follow the same “go left” or “go right” decisions on each comparison as the original value did when it was inserted in the tree. Thus, the duplicate will eventually be compared with a node containing the same value. The duplicate value may be *discarded* at this point.

Searching a binary tree for a value that matches a key is also fast. If the tree is balanced, then each branch contains about *half* the nodes in the tree. Each comparison of a node to the search key *eliminates half the nodes*. This is called an O(log n) algorithm (Big O notation is discussed in [Chapter 20](#)). So a binary search tree with n elements would require a maximum of log₂ n comparisons either to find a match or to determine that no match exists. For example, searching a (balanced) 1000-element binary search tree requires no more than 10 comparisons, because 2¹⁰ > 1000. Searching a (balanced) 1,000,000-element binary search tree requires no more than 20 comparisons, because 2²⁰ > 1,000,000.

## 19.6.9 Overview of the Binary Tree Exercises

In the exercises, algorithms are presented for several other binary tree operations such as deleting an item from a binary tree, printing a binary tree in a two-dimensional tree format and performing a **level-order traversal** of a binary tree. The level-order traversal of a binary tree visits the nodes of the tree row by row, starting at the root node level. On each level of the tree, the nodes are visited from left to right. Other binary tree exercises include allowing a binary search tree to contain duplicate values, inserting string values in a binary tree and determining how many levels are contained in a binary tree.

## 19.7 Wrap-Up

In this chapter, you learned that linked lists are collections of data items that are “linked up in a chain.” You also learned that a program can perform insertions and deletions anywhere in a linked list (though our implementation performed insertions and deletions only at the ends of the list). We demonstrated that the stack and queue data structures are constrained versions of lists. For stacks, you saw that insertions and deletions are made only at the top. For queues, you saw that insertions are made at the tail and deletions are made from the head. We also presented the binary tree data structure. You saw a binary search tree that facilitated high-speed searching and sorting of data and efficient duplicate elimination. You learned how to create these data structures for reusability (as templates) and maintainability. In the next chapter, we study various searching and sorting techniques and implement them as function templates.

## Summary

### Section 19.1 Introduction

- Dynamic data structures (p. 798) grow and shrink during execution.
- Linked lists (p. 798) are collections of data items “lined up in a row”—insertions and removals are made anywhere in a linked list.
- Stacks (p. 798) are important in compilers and operating systems: Insertions and removals are made only at one end of a stack—its top (p. 798).
- Queues (p. 798) represent waiting lines; insertions are made at the back (also referred to as the tail; p. 798) of a queue and removals are made from the front (also referred to as the head; p. 798).
- Binary trees (p. 798) facilitate high-speed searching and sorting of data, efficient duplicate elimination, representation of file-system directories and compilation of expressions into machine code.
