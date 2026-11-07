
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

The delete function performs the following steps:

- 1. If the character to delete matches the first node’s character (line 115), we must remove the first node. Assign `*sPtr` to tempPtr, which we’ll use to free the node’s memory. Assign `(*sPtr)->nextPtr` to `*sPtr`, so that startPtr in main now points to what was previously the list’s second node. Call free to deallocate the memory pointed to by tempPtr. Return the character that was deleted.
- 2. Otherwise, initialize previousPtr with `*sPtr` and initialize currentPtr with `(*sPtr)->nextPtr` (lines 122–123) to advance to the second node.
- 3. Locate the character to delete. While currentPtr is not NULL and the value to delete is not equal to currentPtr->data (line 126), assign currentPtr to previousPtr (line 127) and assign currentPtr->nextPtr to currentPtr (line 128) to advance to the list’s next node.
- 4. If currentPtr is not NULL (line 132), the character is in the list. Assign currentPtr to tempPtr (line 133), which we’ll use to deallocate the node. Assign currentPtr->nextPtr to previousPtr->nextPtr (line 134) to connect the node before and the node after the one being removed. Free the node pointed to by tempPtr (line 135), then return the deleted character (line 136).

If nothing has been returned yet, line 140 returns the null character ('\0') to signify that the character was not found in the list.

### Illustrating a Delete

The following diagram illustrates deleting the node containing 'C' from a linked list. Part (a) shows the linked list before the deletion. Part (b) shows the link reassignments. Pointer tempPtr is used to free the memory allocated to the node that stores 'C'. Note that in lines 118 and 135, we free `tempPtr`. Previously, we recommended setting a freed pointer to `NULL`. We do not do that here because `tempPtr` is a local automatic variable, and the function returns immediately after freeing the memory.

![](img/43d318ad505997c339a3ea78d716d162_662_0.png)

### 12.4.3 Functions isEmpty and printList

Function isEmpty (lines 144–146) is a predicate function—it does not alter the list in any way. Rather, isEmpty determines whether the list is empty—that is, the pointer to the first node is NULL. If the list is empty, isEmpty returns 1; otherwise, it returns 0.

```c
// return 1 if the list is empty, 0 otherwise
int isEmpty(ListNodePtr sPtr) {
    return sPtr == NULL;
}

// print the list
void printList(ListNodePtr currentPtr) {
    // if list is empty
    if (isEmpty(currentPtr)) {
        puts("List is empty\n");
    }
    else {
        puts("The list is:");

        // while not the end of the list
        while (currentPtr != NULL) {
            printf("%c --> ", currentPtr->data);
            currentPtr = currentPtr->nextPtr;
        }

        puts("\n");
    }
}
```

Function printList (lines 149–165) prints a list. The function's currentPtr parameter receives a pointer to the list's first node. The function first determines whether the list is empty (lines 151–153) and, if so, prints "List is empty." and terminates. Otherwise, lines 155–163 print the list's data. While currentPtr is not NULL, line 159 prints the value in currentPtr->data, and line 160 assigns currentPtr->nextPtr to currentPtr to advance to the next node. If the link in the last node of the list is not NULL, the printing algorithm will try to print past the end of the list, which is a logic error. This printing algorithm is identical for linked lists, stacks and queues.

### List-Based Recursion Exercises

Exercise 12.17 asks you to implement a recursive function that prints a list backward. Exercise 12.18 asks you to implement a recursive function that searches a linked list for a particular data item.

### Self Check

- **1. (Multiple Choice)** Which of the following statements a), b) or c) is false?
  - a) A linked list is a linear collection of self-referential structures, called nodes, connected by pointer links—hence, the term "linked" list.
  - b) A linked list is accessed via a pointer to the first node of the list.
  - c) Subsequent nodes in a linked list are accessed via the link pointer member stored in each node.
  - d) All of the above statements are true.
  - **Answer:** d.

- **2. (True/False)** A linked list is appropriate when the number of data items to store in the data structure is unpredictable.
  - **Answer:** True.

- **3. (True/False)** The elements in a linked list are stored contiguously in memory. This allows immediate access to any elements because its address can be calculated directly, based on its position relative to the beginning of the linked list. Arrays do not afford such immediate access to their elements.
  - **Answer:** False. Actually, the reverse is true. An array's elements are stored contiguously in memory and support immediate access by position. Linked lists do not afford such immediate access to their elements.

- **4. (Fill-In)** Passing into a function the address of the pointer to a linked list's first node creates a pointer to a pointer. This is often called double __________.
  - **Answer:** indirection.

## 12.5 Stacks

A stack can be implemented as a constrained version of a linked list. You add new nodes and remove existing ones only at the top. For this reason, a stack is referred to as a last-in, first-out (LIFO) data structure. You access a stack via a pointer to its top element. The link member in the stack’s last node is set to NULL to indicate the stack’s bottom. Not terminating the stack with NULL can lead to runtime errors.

The following diagram illustrates a stack with several nodes—stackPtr points to the stack’s top element. We represent stacks and linked lists in these figures identically. The difference between them is that insertions and deletions may occur anywhere in a linked list, but only at the top of a stack.

![](img/43d318ad505997c339a3ea78d716d162_664_0.png)

### Primary Stack Operations

A stack’s primary functions are push and pop. Function push creates a new node and places it on top of the stack. Function pop removes a node from the stack’s top, frees that node’s memory and returns the popped value.

### Implementing a Stack

Figure 12.2 implements a simple stack of integers. The program allows you to push a value onto the stack (function push), pop a value off the stack (function pop) and terminate the program. Lines 7–10 define struct stackNode, which we’ll use to represent the stack’s nodes. As in Fig. 12.1, we use typedefs (lines 12–13) to make the code more readable. Initially, stackPtr (line 23) is set to NULL to indicate an empty stack. Much of this application’s logic is similar to Fig. 12.1, so we focus on the differences here.

```c
1 // Fig12_02.c
2 // A simple stack program
3 #include <stdio.h>
4 #include <stdlib.h>
5
6 // self-referential structure
7 struct stackNode {
8    int data; // define data as an int
9    struct stackNode *nextPtr; // stackNode pointer
10 };
11
12 typedef struct stackNode StackNode; // synonym for struct stackNode
13 typedef StackNode *StackNodePtr; // synonym for StackNode*
14
15 // prototypes
16 void push(StackNodePtr *topPtr, int info);
17 int pop(StackNodePtr *topPtr);
18 int isEmpty(StackNodePtr topPtr);
19 void printStack(StackNodePtr currentPtr);
20 void instructions(void);
21
```

**Fig. 12.2** | A simple stack program. (Part 1 of 4.)
