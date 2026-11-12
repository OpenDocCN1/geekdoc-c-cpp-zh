7. Consider an array-based implementation of a binary search tree bst. Figure 16-1 presents such a representation for a particular binary search tree.

a. Depict the array in an array-based implementation for the binary search tree in Figure 15-14a of Chapter 15. Assume that tree items are strings.

b. Show the effect of each of the following sequential operations on the array in part a of this exercise.

```
bst.add("Doug");
bst.add("Nancy");
bst.add("Bob");
bst.add("Sarah");
```

c. Repeat parts a and b of this exercise for the tree in Figure 15-14b.

d. Write an inorder traversal algorithm for this array-based implementation.

8. Duplicates in an ADT could mean either identical items or, more subtly, objects that match because their class overloads the equality operator so that it compares only certain fields, while differences exist in other fields. If duplicates are allowed in a binary search tree, it is important to have a convention that determines the relationship between the duplicates. Items that duplicate the root of a tree should either all be in the left subtree or all be in the right subtree, and, of course, this property must hold for every subtree.

a. Why is this convention critical to the effective use of the binary search tree?

b. This chapter stated that you can remove an item from a binary search tree by replacing it with the item that either immediately follows or immediately precedes the item to be deleted. If duplicates are allowed, however, the choice between inorder successor and inorder predecessor is no longer arbitrary. How does the convention of putting duplicates in either the left or right subtree affect this choice?

9. Complete the trace of the nonrecursive inorder traversal algorithm that Figure 16-4 began. Show the contents of the implicit stack as the traversal progresses.

10. Implement in C++ the nonrecursive inorder traversal algorithm for a binary tree that was presented in this chapter.

11. Exercise 13 in Chapter 15 introduced the minimax tree. It has min nodes and max nodes. Part b of the exercise asked you to design a solution for representing and evaluating these trees. Implement your design in C++.

12. Design another algorithm to remove items from a binary search tree. This algorithm differs from the one described in this chapter when a node N has two children. First let N's right child take the place of the deleted node N in the same manner in which you delete a node with one child. Next reconnect N's left child (along with its subtree, if any) to the left side of the node containing the inorder successor of the value in N.

13. Write iterative methods to perform insertion and removal operations on a binary search tree.

14. A level-order traversal of a tree processes (visits) nodes one level at a time, from left to right, beginning with the root. Design an algorithm that performs a level-order traversal of a binary tree.

15. If you know in advance that you often access a given item in a binary search tree several times in succession before accessing a different item, you will end up searching for the same item repeatedly. One way to avoid this problem is to add an extra bookkeeping component to your implementation. That is, you can maintain a last-accessed pointer that will always reference the last item that any binary search tree operation accessed. Whenever you perform such an operation, you can check the search key of the item most recently accessed before performing the operation.

Revise the implementation of the ADT binary search tree to add this new feature by adding the data member lastAccessed to the class.