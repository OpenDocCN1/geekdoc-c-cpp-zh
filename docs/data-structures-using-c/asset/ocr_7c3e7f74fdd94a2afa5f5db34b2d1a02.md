where the previous node lies in the memory. In SLL, we can traverse only in one direction. We have no way to go to the ith node from (i + 1)th node, unless the list is traversed again from the first node (Fig. 6.25).

![](bbox=[0.25, 0.18, 0.85, 0.24])

Fig. 6.25 Singly linked list

Often SLL is just referred to as a linked list.

# Doubly Linked List

In a doubly linked list (DLL), each node has two link fields to store information about the one to the next and also about the one ahead of the node. Hence, each node has knowledge of its successor and also its predecessor. In DLL, from every node, the list can be traversed in both the directions (Fig. 6.26).

![](bbox=[0.25, 0.44, 0.85, 0.5])

Fig. 6.26 Doubly linked list

Both SSL and DLL may or may not contain a header node. The one with a header node is explicitly mentioned in the title as a header-SLL and a header-DLL. These are also called as singly linked list with header node and doubly linked list with header node.

# 6.6.3 Linear and Circular Linked Lists

The other classification of linked lists based on their method of traversal is as follows:

+   1. Linear linked list
+   2. Circular linked list

# Linear Linked List

The linked lists that we have seen so far are known as linear linked lists. All elements of such a linked list can be accessed by traversing a list from the first node of the list.

# Circular Linked List

Although a linear linked list is a useful and popular data structure, it has some shortcomings. For example, consider an SLL. Given a pointer A to a node in a linear list, we cannot