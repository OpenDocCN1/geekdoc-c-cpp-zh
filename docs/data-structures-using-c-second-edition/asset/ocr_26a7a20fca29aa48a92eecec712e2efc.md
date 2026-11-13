# Deleting the Node Before a Given Node in a Doubly Linked List

Consider the doubly linked list shown in Fig. 6.53. Suppose we want to delete the node preceding the node with value 4. Before discussing the changes that will be done in the linked list, let us first look at the algorithm.

![](bbox=[0.175, 0.195, 0.875, 0.465])

Figure 6.53 Deleting a node before a given node in a doubly linked list

+   Step 1: IF START = NULL
+   Write UNDERFLOW
+   Go to Step 9
+   [END OF IF]
+   Step 2: SET PTR = START
+   Step 3: Repeat Step 4 while PTR -> DATA != NUM
+   Step 4: SET PTR = PTR -> NEXT
+   [END OF LOOP]
+   Step 5: SET TEMP = PTR -> PREV
+   Step 6: SET TEMP -> PREV -> NEXT = PTR
+   Step 7: SET PTR -> PREV = TEMP -> PREV
+   Step 8: FREE TEMP
+   Step 9: EXIT

Figure 6.54 Algorithm to delete a node before a given node

Figure 6.54 shows the algorithm to delete a node before a given node of a doubly linked list. In Step 2, we take a pointer variable PTR and initialize it with START. That is, PTR now points to the first node of the linked list. The while loop traverses through the linked list to reach the desired node. Once we reach the node containing val, the PREV field of PTR is set to contain the address of the node preceding the node which comes before PTR. The memory of the node preceding PTR is freed and returned to the free pool.

Hence, we see that we can insert or delete a node in a constant number of operations given only that node's address. Note that this is not possible in the case of a singly linked list which requires the previous node's address also to perform the same operation.

# PROGRAMMING EXAMPLE

+   3. Write a program to create a doubly linked list and perform insertions and deletions in all cases.

```
```c
#include <stdio.h>
#include <conio.h>
#include <malloc.h>
```
```