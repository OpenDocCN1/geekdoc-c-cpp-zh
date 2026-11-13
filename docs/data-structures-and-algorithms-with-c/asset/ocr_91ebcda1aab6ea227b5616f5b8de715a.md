![](bbox=[0.3, 0.05, 0.7, 0.16])

A NEW node is created whose rlink holds the address of the P node and link holds the address of the PRE node.

![](bbox=[0.3, 0.22, 0.7, 0.33])

At last, rlink of PRE is linked with NEW node and link of P is linked with NEW node.

![](bbox=[0.2, 0.38, 0.8, 0.46])

# Figure 5.22 (a, b, c): Insertion in a doubly linked list

# Addition after any position of the Doubly Linked list

This algorithm creates a node and inserts it after the node at location P. HEAD is a pointer which points to the first node, i.e. it holds the content of HEADER of the linked list and ITEM is the value of the new node. NEW is a pointer which holds the address of the new node. POST holds the address of the next node where a new node to be inserted.

# Algorithm to insert a node after a given node pointer

```
Algorithm: DLL_ADD_AFTER (HEAD, ITEM, P)
1. Set POST = P-RLINK
2. [Create the new node]
   a) Allocate memory for NEW node
   b) IF NEW = NULL then Print: “Memory not Available” and Return
   c) Set NEW-DATA = ITEM
   d) Set NEW-RLINK = POST
   e) Set NEW-LLINK = P
3. Set P-RLINK = NEW
4. Set POST-LLINK = NEW
5. Return
```

At first POST is assigned with the RLINK of the node P after which a new node to be inserted.