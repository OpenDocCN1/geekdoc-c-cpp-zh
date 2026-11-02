
### 12.4.3 Function `printList`

Function `printList` (lines 156–173) receives a pointer to the start of the list as an argument and refers to the pointer as `currentPtr`. The function first determines whether the list is *empty* (lines 159–161) and, if so, prints "List is empty." and terminates. Otherwise, it prints the data in the list (lines 162–172). While `currentPtr` is not NULL, the value of `currentPtr->data` is printed by the function, and `currentPtr->nextPtr` is assigned to `currentPtr` to advance to the next node. If the link in the last node of the list is not NULL, the printing algorithm will try to print past the end of the list, and an error will occur. The printing algorithm is identical for linked lists, stacks and queues.

Exercise 12.20 asks you to implement a recursive function that prints a list backward. Exercise 12.21 asks the reader to implement a recursive function that searches a linked list for a particular data item.

## 12.5 Stacks

A stack can be implemented as a constrained version of a linked list. New nodes can be added to a stack and removed from a stack *only at the top*. For this reason, a stack is referred to as a last-in, first-out (LIFO) data structure. A stack is referenced via a pointer to the top element of the stack. The link member in the last node of the stack is set to NULL to indicate the bottom of the stack.

Figure 12.7 illustrates a stack with several nodes—`stackPtr` points to the stack’s top element. We represent stacks and linked lists in these figures identically. The difference between stacks and linked lists is that insertions and deletions may occur *anywhere* in a linked list, but *only at the top* of a stack.

> **Common Programming Error 12.5**
>
> *Not setting the link in the bottom node of a stack to NULL can lead to runtime errors.*

![](img/d0d3b7423c2d9e5650be79209ea1885d_521_0.png)

**Fig. 12.7** | Stack graphical representation.

### *Primary Stack Operations*

The primary functions used to manipulate a stack are push and pop. Function push creates a new node and places it *on top* of the stack. Function pop *removes a node from the top* of the stack, *frees* the memory that was allocated to the popped node and *returns the popped value*.

### *Implementing a Stack*

Figure 12.8 (output shown in Fig. 12.9) implements a simple stack of integers. The program provides three options: 1) push a value onto the stack (function push), 2) pop a value off the stack (function pop) and 3) terminate the program.

```c
// Fig. 12.8: fig12_08.c
// A simple stack program
#include <stdio.h>
#include <stdlib.h>

// self-referential structure
struct stackNode {
    int data; // define data as an int
    struct stackNode *nextPtr; // stackNode pointer
};

typedef struct stackNode StackNode; // synonym for struct stackNode
typedef StackNode *StackNodePtr; // synonym for StackNode*

// prototypes
void push(StackNodePtr *topPtr, int info);
int pop(StackNodePtr *topPtr);
int isEmpty(StackNodePtr topPtr);
void printStack(StackNodePtr currentPtr);
void instructions(void);

// function main begins program execution
int main(void)
{
    StackNodePtr stackPtr = NULL; // points to stack top
    int value; // int input by user

    instructions(); // display the menu
    printf("%s", "\n");
    unsigned int choice; // user's menu choice
    scanf("%u", &choice);

    // while user does not enter 3
    while (choice != 3) {

        switch (choice) {

            // push value onto stack
            case 1:
                printf("%s", "Enter an integer: ");
                scanf("%d", &value);
                push(&stackPtr, value);
                printStack(stackPtr);
                break;
            // pop value off stack
            case 2:
                // if stack is not empty
                if (!isEmpty(stackPtr)) {
                    printf("The popped value is %d.\n", pop(&stackPtr));
                }

                printStack(stackPtr);
                break;
            default:
                puts("Invalid choice.\n");
                instructions();
                break;
        }

        printf("%s", "? ");
        scanf("%u", &choice);
    }

    puts("End of run.");
}

// display program instructions to user
void instructions(void)
{
    puts("Enter choice:\n"
        "1 to push a value on the stack\n"
        "2 to pop a value off the stack\n"
        "3 to end program");
}

// insert a node at the stack top
void push(StackNodePtr *topPtr, int info)
{
    StackNodePtr newPtr = malloc(sizeof(StackNode));

    // insert the node at stack top
    if (newPtr != NULL) {
        newPtr->data = info;
        newPtr->nextPtr = *topPtr;
        *topPtr = newPtr;
    }
    else { // no space available
        printf("%d not inserted. No memory available.\n", info);
    }
}

// remove a node from the stack top
int pop(StackNodePtr *topPtr)
{
    StackNodePtr tempPtr = *topPtr;
    int popValue = (*topPtr)->data;
    *topPtr = (*topPtr)->nextPtr;
    free(tempPtr);
    return popValue;
}

// print the stack
void printStack(StackNodePtr currentPtr)
{
    // if stack is empty
    if (currentPtr == NULL) {
        puts("The stack is empty.\n");
    }
    else {
        puts("The stack is:");

        // while not the end of the stack
        while (currentPtr != NULL) {
            printf("%d --> ", currentPtr->data);
            currentPtr = currentPtr->nextPtr;
        }

    }
    puts("NULL\n");
}

// return 1 if the stack is empty, 0 otherwise
int isEmpty(StackNodePtr topPtr)
{
    return topPtr == NULL;
}
```

**Fig. 12.8** | A simple stack program.

```text
Enter choice:
1 to push a value on the stack
2 to pop a value off the stack
3 to end program
? 1
Enter an integer: 5
The stack is:
5 --> NULL

? 1
Enter an integer: 6
The stack is:
6 --> 5 --> NULL

? 1
Enter an integer: 4
The stack is:
4 --> 6 --> 5 --> NULL

? 2
The popped value is 4.
The stack is:
6 --> 5 --> NULL

? 2
The popped value is 6.
The stack is:
5 --> NULL

? 2
The popped value is 5.
The stack is empty.

? 2
The stack is empty.

? 4
Invalid choice.

Enter choice:
1 to push a value on the stack
2 to pop a value off the stack
3 to end program
? 3
End of run.
```

**Fig. 12.9** | Sample output from the program of Fig. 12.8.

### 12.5.1 Function push

Function push (lines 76–89) places a new node at the top of the stack. The function consists of three steps:

- 1. Create a *new node* by calling `malloc` and assign the location of the allocated memory to `newPtr` (line 78).
- 2. Assign to `newPtr->data` the value to be placed on the stack (line 82) and assign `*topPtr` (the *stack top pointer*) to `newPtr->nextPtr` (line 83)—the *link member* of `newPtr` now points to the *previous top node*.
- 3. Assign `newPtr` to `*topPtr` (line 84)—`*topPtr` now points to the *new stack top*.

Manipulations involving `*topPtr` change the value of `stackPtr` in `main`. Figure 12.10 illustrates function push. Part (a) of the figure shows the `stackPtr` and the new node before the push operation. The dotted arrows in part (b) illustrate *Steps 2 and 3* of the push operation that enable the node containing 12 to become the new stack top.

![](img/d0d3b7423c2d9e5650be79209ea1885d_525_0.png)

**Fig. 12.10** | push operation.

### 12.5.2 Function pop

Function pop (lines 92–99) removes the node at the top of the stack. Function main determines whether the stack is empty before calling pop. The pop operation consists of five steps:

- 1. Assign `*topPtr` to `tempPtr` (line 94); `tempPtr` will be used to *free* the unneeded memory.
- 2. Assign `(*topPtr)->data` to `popValue` (line 95) to *save* the value in the top node.
- 3. Assign `(*topPtr)->nextPtr` to `*topPtr` (line 96) so `*topPtr` contains the *address of the new top node*.
- 4. *Free* the memory pointed to by `tempPtr` (line 97).
- 5. *Return popValue* to the caller (line 98).

Figure 12.11 illustrates the function pop. Part (a) shows the stack after the previous push operation. Part (b) shows `tempPtr` pointing to the *first node* of the stack and `*topPtr` pointing to the *second node* of the stack. Function free is used to *free the memory* pointed to by `tempPtr`.

![](img/d0d3b7423c2d9e5650be79209ea1885d_526_0.png)

### 12.5.3 Applications of Stacks

Stacks have many interesting applications. For example, whenever a *function call* is made, the called function must know how to *return* to its caller, so the *return address* is pushed onto a stack (Section 5.7). In a series of function calls, the successive return addresses are pushed onto the stack in *last-in, first-out* order so that each function can return to its caller. Stacks support recursive function calls in the same manner as conventional nonrecursive calls.

Stacks contain the space created for *automatic variables* on each invocation of a function. When the function returns to its caller, the space for that function's automatic variables is popped off the stack, and these variables no longer are known to the program. Stacks also are sometimes used by compilers in the process of evaluating expressions and generating machine-language code. The exercises explore several applications of stacks.
