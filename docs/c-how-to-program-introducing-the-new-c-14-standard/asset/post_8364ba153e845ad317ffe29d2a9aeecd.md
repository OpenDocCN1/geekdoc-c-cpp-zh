
- 11. 19.16 (*Allowing Duplicates in Binary Trees*) Modify the program of **Figs. 19.20–19.22** to allow the binary tree object to contain duplicates.

- 12. 19.17 (*Binary Tree of Strings*) Write a program based on **Figs. 19.20–19.22** that inputs a line of text, tokenizes the sentence into separate words (you may want to use the `istringstream` library class), inserts the words in a binary search tree and prints the inorder, preorder and postorder traversals of the tree. Use an OOP approach.

- 13. 19.18 (*Duplicate Elimination*) In this chapter, we saw that duplicate elimination is straightforward when creating a binary search tree. Describe how you’d perform duplicate elimination using only a one-dimensional array. Compare the performance of array-based duplicate elimination with the performance of binary-search-tree-based duplicate elimination.

- 14. 19.19 (*Depth of a Binary Tree*) Write a function `depth` that receives a binary tree and determines how many levels it has.

- 15. 19.20 (*Recursively Print a List Backward*) Write a member function `printListBackward` that recursively outputs the items in a linked list object in reverse order. Write a test program that creates a sorted list of integers and prints the list in reverse order.

- 16. 19.21 (*Recursively Search a List*) Write a member function `searchList` that recursively searches a linked list object for a specified value. The function should return a pointer to the value if it’s found; otherwise, `nullptr` should be returned. Use your function in a test program that creates a list of integers. The program should prompt the user for a value to locate in the list.

- 17. 19.22 (**Binary Tree Search**) Write member function `binaryTreeSearch`, which attempts to locate a specified value in a binary search tree object. The function should take as arguments a pointer to the binary tree’s root node and a search key to locate. If the node containing the search key is found, the function should return a pointer to that node; otherwise, the function should return a `nullptr` pointer.

- 18. 19.23 (**Level-Order Binary Tree Traversal**) The program of **Figs. 19.20–19.22** illustrated three recursive methods of traversing a binary tree—inorder, preorder and postorder traversals. This exercise presents the *level-order traversal* of a binary tree, in which the node values are printed level by level, starting at the root node level. The nodes on each level are printed from left to right. The level-order traversal is not a recursive algorithm. It uses a queue object to control the output of the nodes. The algorithm is as follows:

  - A. Insert the root node in the queue.
  - B. While there are nodes left in the queue,
    - Get the next node in the queue.
    - Print the node’s value.
    - If the pointer to the left child of the node is not `nullptr`
      - Insert the left child node in the queue.
    - If the pointer to the right child of the node is not `nullptr`
      - Insert the right child node in the queue.

  Write member function `levelOrder` to perform a level-order traversal of a binary tree object. Modify the program of **Figs. 19.20–19.22** to use this function. *[Note: You’ll also need to modify and incorporate the queue-processing functions of Fig. 19.16 in this program.]*

- 19. 19.24 (**Printing Trees**) Write a recursive member function `outputTree` to display a binary tree object on the screen. The function should output the tree row by row, with the top of the tree at the left of the screen and the bottom of the tree toward the right of the screen. Each row is output vertically. For example, the binary tree illustrated in **Fig. 19.24** is output as shown in **Fig. 19.25**. Note that the rightmost leaf node appears at the top of the output in the rightmost column and the root node appears at the left of the output. Each column of output starts five spaces to the right of the previous column. Function `outputTree` should receive an argument `totalSpaces` representing the number of spaces preceding the value to be output (this variable should start at zero, so the root node is output at the left of the screen). The function uses a modified inorder traversal to output the tree—it starts at the rightmost node in the tree and works back to the left. The algorithm is as follows:

  - While the pointer to the current node is not `nullptr`
    - Recursively call `outputTree` with the current node’s right subtree and `totalSpaces + 5`
    - Use a `for` structure to count from 1 to `totalSpaces` and output spaces
    - Output the value in the current node.
    - Set the pointer to the current node to point to the left subtree of the current node. Increment `totalSpaces` by 5.

  ![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2367_0.png)

  **Fig. 19.25 Sample output for [Exercise 19.24](#).**

- 20. 19.25 (**Insert/Delete Anywhere in a Linked List**) Our linked list class template allowed insertions and deletions at only the front and the back of the linked list. These capabilities were convenient for us when we used `private` inheritance and composition to produce a stack class template and a queue class template with a minimal amount of code by reusing the list class template. Actually, linked lists are more general than those we provided. Modify the linked list class template we developed in this chapter to handle insertions and deletions anywhere in the list.

- 21. 19.26 (**List and Queues without Tail Pointers**) Our implementation of a linked list ([Figs. 19.4–19.5](#)) used both a `firstPtr` and a `lastPtr`. The `lastPtr` was useful for the `insertAtBack` and `removeFromBack` member functions of the `List` class. The `insertAtBack` function corresponds to the `enqueue` member function of the `Queue` class. Rewrite the `List` class so that it does not use a `lastPtr`. Thus, any operations on the tail of a list must begin searching the list from the front. Does this affect our implementation of the `Queue` class (Fig. 19.16)?

- 22. 19.27 (*Performance of Binary Tree Sorting and Searching*) One problem with the binary tree sort is that the order in which the data is inserted affects the shape of the tree—for the same collection of data, different orderings can yield binary trees of dramatically different shapes. The performance of the binary tree sorting and searching algorithms is sensitive to the shape of the binary tree. What shape would a binary tree have if its data were inserted in increasing order? In decreasing order? What shape should the tree have to achieve maximal searching performance?

- 23. 19.28 (*Indexed Lists*) As presented in the text, linked lists must be searched sequentially. For large lists, this can result in poor performance. A common technique for improving list searching performance is to create and maintain an index to the list. An index is a set of pointers to various key places in the list. For example, an application that searches a large list of names could improve performance by creating an index with 26 entries—one for each letter of the alphabet. A search operation for a last name beginning with `"Y"` would first search the index to determine where the `"Y"` entries begin and “jump into” the list at that point and search linearly until the desired name was found. This would be much faster than searching the linked list from the beginning. Use the `List` class of Figs. 19.4–19.5 as the basis of an `IndexedList` class. Write a program that demonstrates the operation of indexed lists. Be sure to include member functions `insertInIndexedList`, `searchIndexedList` and `deleteFromIndexedList`.

## Special Section: Building Your Own Compiler

In **Exercises 8.15–8.17**, we introduced Simpletron Machine Language (SML), and you implemented a Simpletron computer simulator to execute SML programs. In Exercises 19.29–19.33, we build a compiler that converts programs written in a high-level programming language to SML. This section “ties” together the entire programming process. You’ll write programs in this new high-level language, compile them on the compiler you build and run them on the simulator you built in **Exercise 8.16**. You should make every effort to implement your compiler in an object-oriented manner. *[Note: Due to the size of the descriptions for Exercises 19.29–19.33, we’ve posted them in a PDF document located at [http://www.deitel.com/books/cpphtp10/](http://www.deitel.com/books/cpphtp10/).]*
