![](bbox=[0.22, 0.08, 0.82, 0.17])

If the list contains more than one node, then Temp is assigned to HEAD and HEAD moves to the next node. Then Temp is deleted. The LINK field of the last node contains the address of the new first node.

![](bbox=[0.15, 0.25, 0.75, 0.33])

Figure 5.18 (a, b, c): Deletion from a Circular linked list

# Traverse a circular Linked list

This algorithm traverses a circular linked list and prints the data part of each node of the linked list. _f is a pointer which points to the starting node of the linked list . _Temp' is a temporary pointer to traverse the list.

# Algorithm to display a Circular Linked List

```
ALGORITHM: DISPLAY (HEAD)
1. [Make Temp to point to the first node]
   Set Temp = HEAD
   [Check for empty list]
2. IF HEAD = NULL then
   Print: "The linked list is empty" and Return
3. Print: Temp->DATA
   Set Temp = Temp->LINK
4. Repeat While Temp! = HEAD
   Print: Temp->DATA
   Set Temp = Temp->LINK
5. Return
```

# Complexity of a circular linked list

The cost to add or delete an element from a known location in the circular linked list is O(1).

# Application of Circular Linked List

+   - The real life application where the circular linked list is used is our Personal Computers, where multiple applications are running. All the running applications are kept in a circular linked list and the OS is given a fixed time slot to all for running. The Operating System keeps on iterating over the linked list until all the applications are completed.

+   - Another example, can be Multiplayer games. All the Players are kept in a Circular Linked List and the pointer keeps on moving forward as a player's chance ends.