
## Section 20.3 Dynamic Memory Allocation and Data Structures

- The limit for dynamic memory allocation can be as large as the amount of available physical memory in the computer or the amount of available virtual memory in a virtual memory system.

## Section 20.4 Linked Lists

- A linked list is a linear collection of self-referential class objects, called nodes, connected by pointer links—hence, the term “linked” list.
- A linked list is accessed via a pointer to the first node of the list. Each subsequent node is accessed via the link-pointer member stored in the previous node.
- Linked lists, stacks and queues are linear data structures. Trees are nonlinear data structures.
- A linked list is appropriate when the number of data elements to be represented is unpredictable.
- Linked lists are dynamic, so the length of a list can increase or decrease as necessary.
- A singly linked list begins with a pointer to the first node, and each node contains a pointer to the next node “in sequence.”
- A circular, singly linked list begins with a pointer to the first node, and each node contains a pointer to the next node. The “last node” does not contain a null pointer; rather, the pointer in the last node points back to the first node, thus closing the “circle.”
- A doubly linked list allows traversals both forward and backward.
- A doubly linked list is often implemented with two “start pointers”—one that points to the first element to allow front-to-back traversal of the list and one that points to the last element to allow back-to-front traversal. Each node has a pointer to both the next and previous nodes.
- In a circular, doubly linked list, the forward pointer of the last node points to the first node, and the backward pointer of the first node points to the last node, thus closing the “circle.”

## Section 20.5 Stacks

- A stack data structure allows nodes to be added to and removed from the stack only at the top.
- A stack is referred to as a last-in, first-out (LIFO) data structure.
- The primary member functions used to manipulate a stack are push and pop. Function push inserts a new node at the top of the stack. Function pop removes a node from the top of the stack.
- A dependent name is an identifier that depends on the value of a template parameter. Resolution of dependent names occurs when the template is instantiated.
- Non-dependent names are resolved at the point where the template is defined.

## Section 20.6 Queues

- A queue is similar to a supermarket checkout line—the first person in line is serviced first, and other customers enter the line at the end and wait to be serviced.
- Queue nodes are removed only from a queue’s head and are inserted only at its tail.
- A queue is referred to as a first-in, first-out (FIFO) data structure. The insert and remove operations are known as enqueue and dequeue.

## Section 20.7 Trees

- Binary trees are trees whose nodes all contain two links (none, one or both of which may be null).
- The root node is the first node in a tree.
- Each link in the root node refers to a child. The left child is the root node of the left subtree, and the right child is the root node of the right subtree.
- The children of a single node are called siblings. A node with no children is called a leaf node.

- b) The ________ operator is used to dynamically allocate memory and construct an object; this operator returns a pointer to the object.
- c) A(n) ________ is a constrained version of a linked list in which nodes can be inserted and deleted only from the start of the list and node values are returned in last-in, first-out order.
- d) A function that does not alter a linked list, but looks at the list to determine whether it's empty, is an example of a(n) ________ function.
- e) A queue is referred to as a(n) ________ data structure, because the first nodes inserted are the first nodes removed.
- f) The pointer to the next node in a linked list is referred to as a(n) ________.
- g) The ________ operator is used to destroy an object and release dynamically allocated memory.
- h) A(n) ________ is a constrained version of a linked list in which nodes can be inserted only at the end of the list and deleted only from the start of the list.
- i) A(n) ________ is a nonlinear, two-dimensional data structure that contains nodes with two or more links.
- j) A stack is referred to as a(n) ________ data structure, because the last node inserted is the first node removed.
- k) The nodes of a(n) ________ tree contain two link members.
- l) The first node of a tree is the ________ node.
- m) Each link in a tree node points to a(n) ________ or ________ of that node.
- n) A tree node that has no children is called a(n) ________ node.
- o) The four traversal algorithms we mentioned in the text for binary search trees are ________, ________, ________ and ________.

20.2 What are the differences between a linked list and a stack?

20.3 What are the differences between a stack and a queue?

20.4 Perhaps a more appropriate title for this chapter would have been "Reusable Data Structures." Comment on how each of the following entities or concepts contributes to the reusability of data structures:

- a) classes
- b) class templates
- c) inheritance
- d) private inheritance
- e) composition

20.5 Manually provide the inorder, preorder and postorder traversals of the binary search tree of Fig. 20.24.

![](img/023f159fdd47d944d48e08843cea732d_880_0.png)

Fig. 20.24 | A 15-node binary search tree.

- d) function pop that pops a value off the stack
- e) function isEmpty that determines if the stack is empty
- f) function printStack that prints the stack

### **20.14** *(Postfix Evaluation Enhanced)*

Modify the postfix evaluator program of Exercise 20.13 so that it can process integer operands larger than 9.

### **20.15** *(Supermarket Simulation)*

Write a program that simulates a checkout line at a supermarket. The line is a queue object. Customers (i.e., customer objects) arrive in random integer intervals of 1–4 minutes. Also, each customer is served in random integer intervals of 1–4 minutes. Obviously, the rates need to be balanced. If the average arrival rate is larger than the average service rate, the queue will grow infinitely. Even with “balanced” rates, randomness can still cause long lines. Run the supermarket simulation for a 12-hour day (720 minutes) using the following algorithm:

- 1) Choose a random integer between 1 and 4 to determine the minute at which the first customer arrives.
- 2) At the first customer’s arrival time:
  - Determine customer’s service time (random integer from 1 to 4);
  - Begin servicing the customer;
  - Schedule arrival time of next customer (random integer 1 to 4 added to the current time).
- 3) For each minute of the day:
  - If the next customer arrives,
    - Say so,
    - Enqueue the customer,
    - Schedule the arrival time of the next customer;
  - If service was completed for the last customer,
    - Say so,
    - Dequeue next customer to be serviced,
    - Determine customer’s service completion time (random integer from 1 to 4 added to the current time).

Now run your simulation for 720 minutes, and answer each of the following:

- a) What’s the maximum number of customers in the queue at any time?
- b) What’s the longest wait any one customer experiences?
- c) What happens if the arrival interval is changed from 1–4 minutes to 1–3 minutes?

### **20.16** *(Allowing Duplicates in Binary Trees)*

Modify the program of Figs. 20.20–20.22 to allow the binary tree object to contain duplicate values.

### **20.17** *(Binary Tree of Strings)*

Write a program based on Figs. 20.20–20.22 that inputs a line of text, tokenizes the sentence into separate words (you may want to use the `istringstream` library class), inserts the words in a binary search tree and prints the inorder, preorder and postorder traversals of the tree. Use an OOP approach.

### **20.18** *(Duplicate Elimination)*

In this chapter, we saw that duplicate elimination is straightforward when creating a binary search tree. Describe how you’d perform duplicate elimination using only a one-dimensional array. Compare the performance of array-based duplicate elimination with the performance of binary-search-tree-based duplicate elimination.

### **20.19** *(Depth of a Binary Tree)*

Write a function that receives a binary tree and determines how many levels it has.

### **20.20** *(Recursively Print a List Backward)*

Write a member function `printListBackward` that recursively outputs the items in a linked list object in reverse order. Write a test program that creates a sorted list of integers and prints the list in reverse order.
