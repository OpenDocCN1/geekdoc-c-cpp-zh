# 19.3.9 Circular Linked Lists and Double Linked Lists

The kind of linked list we’ve been discussing is a **singly linked list**—the list begins with a pointer to the first node, and each node contains a pointer to the next node “in sequence.” This list terminates with a node whose pointer member has the value `nullptr`. A singly linked list may be traversed in only one direction.

A **circular, singly linked list** ([Fig. 19.10](#)) begins with a pointer to the first node, and each node contains a pointer to the next node. The “last node” does not contain `nullptr`; rather, the pointer in the last node points back to the first node, thus closing the “circle.”

![](bbox=[0.118, 0.597, 0.767, 0.778])

**Fig. 19.10 Circular, singly linked list.**

A **doubly linked list** ([Fig. 19.11](#))—such as the Standard Library `list` class template—allows traversals *both forward and backward*. Such a