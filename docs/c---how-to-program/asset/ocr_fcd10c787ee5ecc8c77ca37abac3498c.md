+   - The memory allocated by `malloc` is not initialized.
+   - If no memory is available, `malloc` returns `NULL`.
+   - Function free (p. 511) deallocates memory so that it can be reallocated in the future.
+   - C also provides functions `calloc` and `realloc` for creating and modifying dynamic arrays.

# Section 12.4 Linked Lists

+   - A linked list is a linear collection of self-referential structures, called nodes (p. 512), connected by pointer links (p. 512).
+   - A linked list is accessed via a pointer to the first node. Subsequent nodes are accessed via the link pointer member stored in each node.
+   - By convention, the link pointer in the last node of a list is set to NULL to mark the end of the list.
+   - Data is stored in a linked list dynamically—each node is created as necessary.
+   - A node can contain data of any type including other struct objects.
+   - Linked lists are dynamic, so the length of a list can increase or decrease as necessary.
+   - Linked-list nodes are normally not stored contiguously in memory. Logically, however, the nodes of a linked list appear to be contiguous.

# Section 12.5 Stacks

+   - A stack (p. 521) can be implemented as a constrained version of a linked list. New nodes can be added to a stack and removed from a stack only at the top—referred to as a last-in, first-out (LIFO; p. 521) data structure.
+   - The primary functions used to manipulate a stack are push and pop. Function push creates a new node and places it on top of the stack. Function pop removes a node from the top of the stack, frees the memory that was allocated to the popped node and returns the popped value.
+   - Whenever a function call is made, the called function must know how to return to its caller, so the return address is pushed onto a stack. If a series of function calls occurs, the successive return values are pushed onto the stack in last-in, first-out order so that each function can return to its caller. Stacks support recursive function calls in the same manner as conventional nonrecursive calls.
+   - Stacks are used by compilers in the process of evaluating expressions and generating machine-language code.

# Section 12.6 Queues

+   - Queue nodes are removed only from the head of the queue and inserted only at the tail of the queue—referred to as a first-in, first-out (FIFO; p. 527) data structure.
+   - The insert and remove operations for a queue are known as enqueue and dequeue (p. 527).

# Section 12.7 Trees

+   - A tree (p. 533) is a nonlinear, two-dimensional data structure. Tree nodes contain two or more links.
+   - Binary trees (p. 533) are trees whose nodes all contain two links.
+   - The root node (p. 533) is the first node in a tree. Each link in the root node of a binary tree refers to a child (p. 533). The left child (p. 533) is the first node in the left subtree (p. 533), and the right child (p. 533) is the first node in the right subtree (p. 533). The children of a node are called siblings (p. 533).
+   - A node with no children is called a leaf node (p. 533).