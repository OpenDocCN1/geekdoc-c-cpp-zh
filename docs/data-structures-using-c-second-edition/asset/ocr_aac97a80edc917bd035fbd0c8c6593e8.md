![](bbox=[0.24, 0.1, 0.78, 0.4])

# Figure 6.35 Deleting the last node from a circular linked list

Figure 6.36 shows the algorithm to delete the last node from a circular linked list. In Step 2, we take a pointer variable PTR and initialize it with START. That is, PTR now points to the first node of the linked list. In the while loop, we take another pointer variable PREPTR such that PREPTR always points to one node before PTR. Once we reach the last node and the second last node, we set the next pointer of the second last node to START, so that it now becomes the (new) last node of the linked list. The memory of the previous last node is freed and returned to the free pool.

+   Step 1: IF START = NULL
+       Write Underflow
+       Go to Step 8
+   [END OF IF]
+   Step 2: SET PTR = START
+   Step 3: Repeat Steps 4 and 5 while PTR -> NEXT != START
+   Step 4: SET PREPTR = PTR
+   Step 5: SET PTR = PTR -> NEXT
+   [END OF LOOP]
+   Step 6: SET PREPTR -> NEXT = START
+   Step 7: FREE PTR
+   Step 8: EXIT

# Figure 6.36 Algorithm to delete the last node

# PROGRAMMING EXAMPLE

+   2. Write a program to create a circular linked list. Perform insertion and deletion at the beginning and end of the list.

```
#include <stdio.h>
#include <conio.h>
#include <malloc.h>
struct node
{
    int data;
    struct node *next;
};
struct node *start = NULL;
struct node *create_cll(struct node *);
struct node *display(struct node *);
struct node *insert_beg(struct node *);
struct node *insert_end(struct node *);
```