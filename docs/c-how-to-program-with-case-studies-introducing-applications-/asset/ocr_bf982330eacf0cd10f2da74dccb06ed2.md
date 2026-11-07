```
```c
121    else {
122        ListNodePtr previousPtr = *sPtr;
123        ListNodePtr currentPtr = (*sPtr)->nextPtr;
124
125        // loop to find the correct location in the list
126        while (currentPtr != NULL && currentPtr->data != value) {
127            previousPtr = currentPtr; // walk to ...
128            currentPtr = currentPtr->nextPtr; // ... next node
129        }
130
131        // delete node at currentPtr
132        if (currentPtr != NULL) {
133            ListNodePtr tempPtr = currentPtr;
134            previousPtr->nextPtr = currentPtr->nextPtr;
135            free(tempPtr);
136            return value;
137        }
138    }
139
140    return '\0';
141 }
142
```
```

The delete function performs the following steps:

+   1. If the character to delete matches the first node’s character (line 115), we must remove the first node. Assign *sPtr to tempPtr, which we’ll use to free the node’s memory. Assign (*sPtr)->nextPtr to *sPtr, so that startPtr in main now points to what was previously the list’s second node. Call free to deallocate the memory pointed to by tempPtr. Return the character that was deleted.
+   2. Otherwise, initialize previousPtr with *sPtr and initialize currentPtr with (*sPtr)->nextPtr (lines 122–123) to advance to the second node.
+   3. Locate the character to delete. While currentPtr is not NULL and the value to delete is not equal to currentPtr->data (line 126), assign currentPtr to previousPtr (line 127) and assign currentPtr->nextPtr to currentPtr (line 128) to advance to the list’s next node.
+   4. If currentPtr is not NULL (line 132), the character is in the list. Assign currentPtr to tempPtr (line 133), which we’ll use to deallocate the node. Assign currentPtr->nextPtr to previousPtr->nextPtr (line 134) to connect the node before and the node after the one being removed. Free the node pointed to by tempPtr (line 135), then return the deleted character (line 136).

If nothing has been returned yet, line 140 returns the null character ('\0') to signify that the character was not found in the list.

# ### Illustrating a Delete

The following diagram illustrates deleting the node containing 'C' from a linked list. Part (a) shows the linked list before the deletion. Part (b) shows the link reassignments. Pointer tempPtr is used to free the memory allocated to the node that stores