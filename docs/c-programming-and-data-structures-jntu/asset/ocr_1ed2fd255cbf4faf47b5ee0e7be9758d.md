![](bbox=[0.151, 0.119, 0.795, 0.436])

# **Inserting an Item**

One of the advantages of linked lists is the comparative ease with which new nodes can be inserted. It requires merely resetting of two pointers (rather than having to move around a list of data as would be the case with arrays).

Inserting a new item, say X, into the list has three situations:

+   1. Insertion at the front of the list.
+   2. Insertion in the middle of the list.
+   3. Insertion at the end of the list.

The process of insertion precedes a search for the place of insertion. The search involves in locating a node after which the new item is to be inserted. A general algorithm for insertion is as follows:

```
*Begin*
  *if* the list is empty or
    the new node comes before the head node *then*,
    insert the new node as the head node,
  *else*
    If the new node comes after the last node, *then*,
    insert the new node as the end node,
    *else*
    insert the new node in the body of the list.
*End*
```

Algorithm for placing the new item at the beginning of a linked list:

+   1. Obtain space for new node.