![](bbox=[0.16, 0.06, 0.84, 0.33])

Note that queues and linked lists are represented identically. The difference between a queue and an ordinary linked list is that insertions and deletions may occur anywhere in a linked lists, but in a queue, insertions can be made only in the rear end and deletions can be made only in the front end.

# 3.7.3 PEEK Operation

PEEK operation is used to display the element from the FRONT of the queue, pointed by the FRONT pointer without actually removing it. PEEK operation of a queue is also implemented using linked lists. When implementing the PEEK operation, underflow condition of a queue to be checked. The user should not try to PEEK an element from an empty queue. This type of an attempt is illegal and should be avoided.

```
Algorithm to Retrieve the Contents from the Top of the Stack

PEEK(FRONT : QUEUE, VALUE : DATA)
Step 1 : If (ISEMPTY(FRONT))
    Print “Queue is Empty.”
    Return
[End of If Structure]
Step 2 : VALUE = FRONT -> DATA
End PEEK()
```

# 3.7.4 Traversing a Queue

To read the information or to display the information in a queue, you have to traverse (move) a linked list, node by node from the FRONT node, until the REAR node is reached. Traversing a list involves the following steps.

+   - Assign the address of FRONT pointer to a variable.
+   - Display the information in the data field.
+   - Traverse the list from one node to another by advancing the pointer upto REAR.