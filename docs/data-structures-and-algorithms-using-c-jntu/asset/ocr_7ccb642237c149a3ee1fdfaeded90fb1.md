# 5.3 SINGLY LINKED LIST

A singly linked list is a linear data structure in which each node contains only one link field. Figure 5.4 illustrates the singly linked list.

![](bbox=[0.13, 0.19, 0.86, 0.24])

Figure 5.4 Singly linked list

HEAD pointer contains the address of the first node. The representation of the singly linked list is similar to the representation explained in Section 5.2.

# 5.3.1 OPERATIONS

The operations performed on a singly linked list are as follows:

+   - Traversing
+   - Searching
+   - Insertion
+   - Deletion

To perform insertion and deletion, the functions GETNODE(N) and RETURN(N) are used. GETNODE(N) is used to allocate memory for node N and RETURN (N) is used to return the unused node to memory bank.

# 5.3.1.1 Traversing

Traversing the list implies visiting each and every node in the list from the first node to the last node only once.

```
Algorithm 5.1: SL-TRAVERSE
1. Set PTR with the current pointer node.
2. Repeat steps 3 and 4.
3. VISIT the current node.
4. Set PTR with pointer to next node.
5. End.
```

# 5.3.1.2 Searching

Searching operation is used to find the value of DATA field in the singly linked list, while inserting an item into the list at a specified location and deleting an item at the specified location from list. The search operation is performed to locate the node with the DATA item, is to be deleted and to insert a node after that node and to display that particular node.

![](bbox=[0.13, 0.81, 0.86, 0.87])

Figure 5.5 Searching for an element