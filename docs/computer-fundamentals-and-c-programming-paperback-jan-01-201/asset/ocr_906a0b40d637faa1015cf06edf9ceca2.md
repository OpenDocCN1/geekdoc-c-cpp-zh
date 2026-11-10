16.6 realloc uses the pointer returned by ______ or ______ as an argument.

16.7 For automatic initialization of the bytes of a memory block to zeroes, the block must be created by ______ .

16.8 While an array comprises elements, a linked list comprises ______ .

16.9 The .next member of the last node of a linked list has the value ______ .

16.10 Stacks and queues are implementations of the ______ data type.

# **A3. MULTIPLE-CHOICE QUESTIONS**

16.1 Dynamic memory is allocated on the (A) stack, (B) heap, (C) region storing program code, (D) A and B.

16.2 If malloc is called repeatedly and its returned value is assigned to the same pointer variable, (A) a single memory block is allocated, (B) multiple blocks are allocated, (C) heap may become full, (D) B and C.

16.3 If a memory block is not freed, (A) a memory leak occurs, (B) a dangling pointer is created, (C) it is automatically cleared on program termination, (D) B and C.

16.4 realloc returns a pointer (A) to the existing allocated block, (B) that is different from the existing block, (C) that may or may not be different from the existing block, (D) that may be NULL, (E) C and D.

16.5 Access to a linked list (A) is random, (B) is sequential, (C) begins from the head pointer, (D) B and C, (E) A and C.

16.6 The .next member of a linked list is assigned a value (A) after the next node is created, (B) before the next node is created, (C) NULL if no further node is created, (D) A and C, (E) B and C.

# **A4. MIX AND MATCH**

16.1 Match the data structure with its attribute:
(A) Stack, (B) queue, (C) tree
(1) FIFO, (2) hierarchy, (3) LIFO

16.2 Match the linked list with its attribute:
(A) Circular list, (B) list with tail pointer, (C) doubly-linked list.
(1) Pointer to previous node, (2) last node not set to NULL, (3) access from end of list.

# **CONCEPT-BASED QUESTIONS**

16.1 Explain the possible consequences of dynamically creating memory inside a user-defined function.