![](bbox=[0.12, 0.07, 0.85, 0.22])

![](bbox=[0.08, 0.24, 0.92, 0.38])

# Figure 4.6 Insertion using a header node, with curr pointing one node head of the current element. (a) Linked list before insertion. The current node contains 12. (b) Linked list after inserting the node containing 10.

node. Unfortunately, there is no convenient access to the node preceding the one pointed to by curr.

There is an easy solution to this problem. If we set curr to point directly to the preceding element, there is no difficulty in adding a new element after curr. Figure 4.6 shows how the list looks when pointer variable curr is set to point to the node preceding the physical current node. See Exercise 4.5 for further discussion of why making curr point directly to the current element fails.

We encounter a number of potential special cases when the list is empty, or when the current position is at an end of the list. In particular, when the list is empty we have no element for head, tail, and curr to point to. Implementing special cases for insert and remove increases code complexity, making it harder to understand, and thus increases the chance of introducing a programming bug.

These special cases can be eliminated by implementing linked lists with an additional header node as the first node of the list. This header node is a link node like any other, but its value is ignored and it is not considered to be an actual element of the list. The header node saves coding effort because we no longer need to consider special cases for empty lists or when the current position is at one end of the list. The cost of this simplification is the space for the header node. However, there are space savings due to smaller code size, because statements to handle the special cases are omitted. In practice, this reduction in code size typically saves more space than that required for the header node, depending on the number of lists created. Figure 4.7 shows the state of an initialized or empty list when using a header node.

Figure 4.8 shows the definition for the linked list class, named LList. Class LList inherits from the abstract list class and thus must implement all of Class List’s member functions.