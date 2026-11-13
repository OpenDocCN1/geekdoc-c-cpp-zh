
Allocate memory for the new node and initialize its DATA part to 9 and Next part to NULL.

Take a pointer variable PTR which points to START.

Move PTR so that it points to the last node of the list.

Add the new node after the node pointed by PTR. This is done by storing the address of the new node in the NEXT part of PTR.

### Figure 6.14 Inserting an element at the end of a linked list

```
Step 1: IF AVAIL = NULL
        Write OVERFLOW
        Go to Step 10
        [END OF IF]
Step 2: SET NEW_NODE = AVAIL
Step 3: SET AVAIL = AVAIL -> NEXT
Step 4: SET NEW_NODE -> DATA = VAL
Step 5: SET NEW_NODE -> NEXT = NULL
Step 6: SET PTR = START
Step 7: Repeat Step 8 while PTR -> NEXT != NULL
Step 8: SET PTR = PTR -> NEXT
        [END OF LOOP]
Step 9: SET PTR -> NEXT = NEW_NODE
Step 10: EXIT
```

### Figure 6.15 Algorithm to insert a new node at the end

```
Step 1: IF AVAIL = NULL
        Write OVERFLOW
        Go to Step 12
        [END OF IF]
Step 2: SET NEW_NODE = AVAIL
Step 3: SET AVAIL = AVAIL -> NEXT
Step 4: SET NEW_NODE -> DATA = VAL
Step 5: SET PTR = START
Step 6: SET PRETR = PTR
Step 7: Repeat Steps 8 and 9 while PRETR -> DATA != NUM
Step 8: SET PRETR = PTR
Step 9: SET PTR = PTR -> NEXT
        [END OF LOOP]
Step 10: SET PRETR -> NEXT = NEW_NODE
Step 11: SET NEW_NODE -> NEXT = PTR
Step 12: EXIT
```

### Figure 6.16 Algorithm to insert a new node after a node that has value NUM

In Step 5, we take a pointer variable PTR and initialize it with START. That is, PTR now points to the first node of the linked list. Then we take another pointer variable PRETR which will be used to store the address of the node preceding PTR. Initially, PRETR is initialized to PTR. So now, PTR, PRETR, and START are all pointing to the first node of the linked list.

In the while loop, we traverse through the linked list to reach the node that has its value equal to NUM. We need to reach this node because the new node will be inserted after this node. Once we reach this node, in Steps 10 and 11, we change the NEXT pointers in such a way that new node is inserted after the desired node.

START Allocate memory for the new node and initialize its DATA part to 9.

Take two pointer variables PTR and PREPTR and initialize them with START so that START, PTR, and PREPTR point to the first node of the list.

Move PTR and PREPTR until the DATA part of PREPTR = value of the node which insertion has to be done. PREPTR will always point to the node just before PTR.

Add the new node in between the nodes pointed by PREPTR and PTR.

### Figure 6.17 Inserting an element after a given node in a linked list

## Inserting a Node Before a Given Node in a Linked List

Consider the linked list shown in Fig. 6.19. Suppose we want to add a new node with value 9 before the node containing 3. Before discussing the changes that will be done in the linked list, let us first look at the algorithm shown in Fig. 6.18.

### Figure 6.18 Algorithm to insert a new node before a node that has value NUM

```
Step 1: IF AVAIL = NULL
        Write OVERFLOW
        Go to Step 12
        [END OF IF]
Step 2: SET NEW_NODE = AVAIL
Step 3: SET AVAIL = AVAIL -> NEXT
Step 4: SET NEW_NODE -> DATA = VAL
Step 5: SET PTR = START
Step 6: SET PREPTR = PTR
Step 7: Repeat Steps 8 and 9 while PTR -> DATA != NUM
Step 8: SET PREPTR = PTR
Step 9: SET PTR = PTR -> NEXT
        [END OF LOOP]
Step 10: SET PREPTR -> NEXT = NEW_NODE
Step 11: SET NEW_NODE -> NEXT = PTR
Step 12: EXIT
```

In Step 5, we take a pointer variable PTR and initialize it with START. That is, PTR now points to the first node of the linked list. Then, we take another pointer variable PREPTR and initialize it with PTR. So, now, PTR, PREPTR, and START are all pointing to the first node of the linked list.

In the while loop, we traverse through the linked list to reach the node that has its value equal to NUM. We need to reach this node because the new node will be inserted before this node. Once we reach this node, in Steps 10 and 11, we change the NEXT pointers in such a way that the new node is inserted before the desired node.

![](img/be6359df08208122bec6fad1103de211_185_0.png)

Allocate memory for the new node and initialize its DATA part to 9.

![](img/be6359df08208122bec6fad1103de211_185_1.png)

Initialize PREPTR and PTR to the START node.

![](img/be6359df08208122bec6fad1103de211_185_2.png)

START
PTR
PREPTR
Move PTR and PREPTR until the DATA part of PTR = value of the node before which insertion has to be done. PREPTR will always point to the node just before PTR.

![](img/be6359df08208122bec6fad1103de211_185_3.png)

Insert the new node in between the nodes pointed by PREPTR and PTR.

![](img/be6359df08208122bec6fad1103de211_185_4.png)

![](img/be6359df08208122bec6fad1103de211_185_5.png)

### Figure 6.19 Inserting an element before a given node in a linked list

## 6.2.4 Deleting a Node from a Linked List

In this section, we will discuss how a node is deleted from an already existing linked list. We will consider three cases and then see how deletion is done in each case.

- Case 1: The first node is deleted.
- Case 2: The last node is deleted.
- Case 3: The node after a given node is deleted.

Before we describe the algorithms in all these three cases, let us first discuss an important term called UNDERFLOW. Underflow is a condition that occurs when we try to delete a node from a linked list that is empty. This happens when START = NULL or when there are no more nodes to delete. Note that when we delete a node from a linked list, we actually have to free the memory occupied by that node. The memory is returned to the free pool so that it can be used to store other programs and data. Whatever be the case of deletion, we always change the AVAIL pointer so that it points to the address that has been recently vacated.

### Deleting the First Node from a Linked List

Consider the linked list in Fig. 6.20. When we want to delete a node from the beginning of the list, then the following changes will be done in the linked list.

![](img/be6359df08208122bec6fad1103de211_186_0.png)

### Figure 6.20 Deleting the first node of a linked list

Figure 6.21 shows the algorithm to delete the first node from a linked list. In Step 1, we check if the linked list exists or not. If START = NULL, then it signifies that there are no nodes in the list and the control is transferred to the last statement of the algorithm. However, if there are nodes in the linked list, then we use a pointer variable PTR that is set to point to the first node of the list. For this, we initialize PTR with START that stores the address of the first node of the list. In Step 3, START is made to point to the next node in sequence and finally the memory occupied by the node pointed by PTR (initially the first node of the list) is freed and returned to the free pool.

### Figure 6.21 Algorithm to delete the first node

```
Step 1: IF START = NULL
         Write UNDERFLOW
         Go to Step 5
       [END OF IF]
Step 2: SET PTR = START
Step 3: SET START = START -> NEXT
Step 4: FREE PTR
Step 5: EXIT
```

### Deleting the Last Node from a Linked List

Consider the linked list shown in Fig. 6.22. Suppose we want to delete the last node from the linked list, then the following changes will be done in the linked list.

![](img/be6359df08208122bec6fad1103de211_186_1.png)

### Figure 6.22 Deleting the last node of a linked list

Figure 6.23 shows the algorithm to delete the last node from a linked list. In Step 2, we take a pointer variable PTR and initialize it to START. That is, PTR now points to the first node of the linked list. In the while loop, we take another pointer variable PREPTR such that it always points to one node before the PTR. Once we reach the last node and the second last node, we set the NEXT pointer of the second last node to NULL, so that it now becomes the (new) last node of the linked list. The memory of the previous last node is freed and returned back to the free pool.

```
Step 1: IF START = NULL
       Write UNDERFLOW
       Go to Step 8
       [END OF IF]
Step 2: SET PTR = START
Step 3: Repeat Steps 4 and 5 while PTR -> NEXT != NULL
Step 4: SET PREPTR = PTR
Step 5: SET PTR = PTR -> NEXT
       [END OF LOOP]
Step 6: SET PREPTR -> NEXT = NULL
Step 7: FREE PTR
Step 8: EXIT
```

### Figure 6.23 Algorithm to delete the last node

### Deleting the Node After a Given Node in a Linked List

Consider the linked list shown in Fig. 6.24. Suppose we want to delete the node that succeeds the node which contains data value 4. Then the following changes will be done in the linked list.

![](img/be6359df08208122bec6fad1103de211_187_0.png)

Take pointer variables PTR and PREPTR which initially point to START.

![](img/be6359df08208122bec6fad1103de211_187_1.png)

Move PREPTR and PTR such that PREPTR points to the node containing VAL and PTR points to the succeeding node.

![](img/be6359df08208122bec6fad1103de211_187_2.png)

![](img/be6359df08208122bec6fad1103de211_187_3.png)

![](img/be6359df08208122bec6fad1103de211_187_4.png)

Set the NEXT part of PREPTR to the Next part of PTR.

![](img/be6359df08208122bec6fad1103de211_187_5.png)

### Figure 6.24 Deleting the node after a given node in a linked list

Figure 6.25 shows the algorithm to delete the node after a given node from a linked list. In Step 2, we take a pointer variable PTR and initialize it with START. That is, PTR now points to the first node of the linked list. In the while loop, we take another pointer variable PREPTR such that it always points to one node before the PTR. Once we reach the node containing VAL and the node succeeding it, we set the next pointer of the node containing VAL to the address contained in next field of the node succeeding it. The memory of the node succeeding the given node is freed and returned back to the free pool.
