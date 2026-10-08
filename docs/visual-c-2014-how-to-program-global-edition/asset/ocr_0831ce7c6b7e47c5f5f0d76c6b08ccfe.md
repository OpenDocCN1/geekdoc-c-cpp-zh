# Linear and Circular Singly Linked and Doubly Linked Lists

The kind of linked list we have been discussing is a singly linked list—it begins with a reference to the first node, and each node contains a reference to the next node “sequence.” This list terminates with a node whose member has the value null. A singly linked list may be traversed in only one direction.

A circular, singly linked list begins with a reference to the first node, and each node contains a reference to the next node. The “last node” does not contain a null reference; rather, the the last node points back to the first node, thus closing the “circle.”

![](bbox=[0.198, 0.298, 0.802, 0.452])

**Fig. 19.10** | Circular, singly linked list.

A doubly linked list (Fig. 19.11) allows traversals both forward and backward. Such a list is often implemented with two “start references”—one that refers to the first element of the list to allow front-to-back traversal of the list and one that refers to the last element to allow back-to-front traversal. Each node has both a forward reference to the next node in the list and a backward reference to the previous node. If your list contains an alphabetized telephone directory, for example, a search for someone whose name begins with a letter near the front of the alphabet might begin from the front of the list. A search for someone whose name begins with a letter near the end of the alphabet might begin from the back.

![](bbox=[0.198, 0.679, 0.802, 0.831])

**Fig. 19.11** | Doubly linked list.

In a circular, doubly linked list (Fig. 19.12), the forward reference of the last node refers to the first node, and the backward reference of the first node refers to the last node, thus closing the “circle.”