```
0 dequeued
The queue is: 1 5

1 dequeued
The queue is: 5

5 dequeued
Empty queue
com.deitel.ch22.EmptyListException: queue is empty
    at com.deitel.ch22.List.removeFromFront(List.java:81)
    at com.deitel.ch22.Queue.dequeue(Queue.java:24)
    at QueueTest.main(QueueTest.java:29)
```

Fig. 22.14 | Queue processing program. (Part 2 of 2.)

# 22.7 Trees

Lists, stacks and queues are linear data structures (i.e., sequences). A tree is a nonlinear, two-dimensional data structure with special properties. Tree nodes contain two or more links. This section discusses binary trees (Fig. 22.15)—trees whose nodes each contain two links (one or both of which may be null). The root node is the first node in a tree. Each link in the root node refers to a child. The left child is the first node in the left subtree (also known as the root node of the left subtree), and the right child is the first node in the right subtree (also known as the root node of the right subtree). The children of a specific node are called siblings. A node with no children is called a leaf node. Computer scientists normally draw trees from the root node down—the opposite of the way most trees grow in nature.

![](bbox=[0.33, 0.6, 0.68, 0.8])

Fig. 22.15 | Binary tree graphical representation.

In our example, we create a special binary tree called a binary search tree. A binary search tree (with no duplicate node values) has the characteristic that the values in any left subtree are less than the value in that subtree’s parent node, and the values in any right subtree are greater than the value in that subtree’s parent node. Figure 22.16 illustrates a binary search tree with 12 integer values. The shape of the binary search tree that corre-