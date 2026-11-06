# Section 19.3 Linked Lists

+   - A linked list is a linear collection of self-referential class objects, called nodes, connected by **pointer links** (p. 800)—hence, the term “linked” list.
+   - A linked list is accessed via a pointer to the first node of the list. Each subsequent node is accessed via the link-pointer member stored in the previous node and the last node contains a null pointer.
+   - Linked lists, stacks and queues are **linear data structures** (p. 800). Trees are **nonlinear data structures** (p. 800).
+   - A linked list is appropriate when the number of data elements to be represented is unpredictable.
+   - Linked lists are dynamic, so the length of a list can increase or decrease as necessary.
+   - A singly linked list begins with a pointer to the first node, and each node contains a pointer to the next node “in sequence.”
+   - A **circular, singly linked list** (p. 813) begins with a pointer to the first node, and each node contains a pointer to the next node. The “last node” does not contain a null pointer; rather, the pointer in the last node points back to the first node, thus closing the “circle.”
+   - A **doubly linked list** (p. 814) allows traversals both forward and backward.
+   - A doubly linked list is often implemented with two “start pointers”—one that points to the first element to allow front-to-back traversal of the list and one that points to the last element to allow back-to-