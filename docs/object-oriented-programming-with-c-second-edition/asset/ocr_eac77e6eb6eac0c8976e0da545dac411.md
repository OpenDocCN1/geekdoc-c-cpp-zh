# 346 Object-Oriented Programming with C++

a tree? There are three ways of doing it—pre-order, in-order, and post-order. Keep in mind that we stop as we encounter an empty tree.

The sequence of steps for traversing a non-empty tree in pre-order is as follows:

+   1. Visit the root.
2. Visit the left sub-tree in pre-order.
3. Visit the right sub-tree in pre-order.

The sequence of steps for traversing a non-empty tree in in-order is as follows:

+   1. Visit the root.
2. Visit the right sub-tree in in-order.

The sequence of steps for traversing a non-empty tree in post-order is as follows:

+   1. Visit the left sub-tree in post-order.
2. Visit the right sub-tree in post-order.

Let us look at some examples now. Consider the tree shown in Figure 9.60, we have seen earlier also.

![](bbox=[0.231, 0.426, 0.856, 0.655])

Figure 9.60 A binary tree

Let us see the sequence in which the nodes when we follow each of the traversal methods. Let us start with pre-order traversal.

In pre-order traversal, we visit the root first. Hence, we get 'A'. Then we visit the left sub-tree of 'A' in pre-order (visiting the right sub-tree of 'A' is pending at this time). We visit the root first. Hence, we get 'B'. Then we visit the left sub-tree of 'B' in pre-order (visiting the right sub-tree of 'B' is pending at this time). We visit the root first. Hence, we get 'D'. Then, we visit the left sub-tree of 'D' in pre-order (visiting the right sub-tree of 'D' is pending at this time). There is no left sub-tree for 'D'. So, we visit the right sub-tree of 'D', which was pending. There is no left sub-tree for 'D', we go one step back. We visit the right sub-tree of 'B' in pre-order, which was pending. If we continue this we get 'E', 'G', 'C', 'F', 'H'.

To conclude, the result of a pre-order traversal of the above tree will be 'ABDEFGHI'. Similarly, the result of an in-order traversal will be 'GEBHIFCA'.

and the result of a post-order traversal will be 'DGEBHIFCA'