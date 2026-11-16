Data elements of a linear linked list are contained in the `info` field of the list and must be of the same data type (`int`, `char`, `struct`, etc). As each node contains within itself (within its `next` field) a pointer to the next node in the list, we are able to traverse the list and access the nodes of the list in order (that is, from first to last).

The linked list is a dynamic structure and can change size as the program executes. Nodes can be inserted and deleted at any position of a list (beginning, between nodes, at the end). Only the first node, accessed by the list pointer, is known. From there links between nodes can be used to move from one node to another node. Theoretically, there is no upper limit on the length of a list, but practically a computer's memory size is the limit.

Here's an example of a new node being inserted into the middle of the list without causing the other elements to change their locations in memory. Notice that this can be done with just the manipulation of two pointers and requires no data movements:

![](bbox=[0.15, 0.4, 0.73, 0.55])

Working with linear linked lists can be fun because they are easy to draw, yet give a useful way to organize data. In certain places lists can be tricky, but a good drawing can go a long ways toward clarifying such a situation. Actually, I cannot emphasize this enough. It's very important to draw pictures when you're trying to build and understand linked list code. Generally, all you need to do is to draw a box for each node and an arrow going from each node to the next to represent the `next` pointer.