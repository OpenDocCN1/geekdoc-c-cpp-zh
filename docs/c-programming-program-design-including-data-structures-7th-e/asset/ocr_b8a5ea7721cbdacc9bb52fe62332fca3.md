30. Given the nodes of a binary tree in the preorder sequence and the postorder sequence, show that it may not be possible to reconstruct a unique binary tree. (3)

The binary tree of Figure 19-15 is to be used for Exercises 31 and 32.

![](bbox=[0.199, 0.2, 0.897, 0.447])

**FIGURE 19-15**  Figure for Exercises 31 and 32

31. Recall the nonrecursive inorder traversal algorithm for a binary tree given in this chapter. Do an inorder traversal of the binary tree in Figure 19-15. Show the stack contents after each push and pop operation. (8)

32. Recall the nonrecursive preorder traversal algorithm for a binary tree given in this chapter. Do a preorder traversal of the binary tree in Figure 19-15. Show the stack contents after each push and pop operation. (8)

33. Draw the UML class diagram of the class `binaryTreeType`.

34. Draw the UML class diagram of the class `bSearchTreeType`. Also, show the inheritance hierarchy.

# PROGRAMMING EXERCISES

+   1. Write the definition of the function, `nodeCount`, that returns the number of nodes in the binary tree. Add this function to the class `binaryTreeType` and create a program to test this function.

+   2. Write the definition of the function, `nLeavesCount`, that takes as a parameter a pointer to the root node of a binary tree and returns the number of leaves in a binary tree. Add this function to the class `binaryTreeType` and create a program to test this function.

+   3. Write a function, `swapSubtrees`, that swaps all of the left and right subtrees of a binary tree. Add this function to the class `binaryTreeType` and create a program to test this function.