Allocate memory for the new node and initialize its DATA part to 9 and Next part to NULL.

Take a pointer variable PTR which points to START.

Move PTR so that it points to the last node of the list.

Add the new node after the node pointed by PTR. This is done by storing the address of the new node in the NEXT part of PTR.

# Figure 6.14 Inserting an element at the end of a linked list

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

# Figure 6.15 Algorithm to insert a new node at the end

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

# Figure 6.16 Algorithm to insert a new node after a node that has value NUM

In Step 5, we take a pointer variable PTR and initialize it with START. That is, PTR now points to the first node of the linked list. Then we take another pointer variable PRETR which will be used to store the address of the node preceding PTR. Initially, PRETR is initialized to PTR. So now, PTR, PRETR, and START are all pointing to the first node of the linked list.

In the while loop, we traverse through the linked list to reach the node that has its value equal to NUM. We need to reach this node because the new node will be inserted after this node. Once we reach this node, in Steps 10 and 11, we change the NEXT pointers in such a way that new node is inserted after the desired node.