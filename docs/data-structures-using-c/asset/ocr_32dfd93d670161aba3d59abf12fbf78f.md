![](bbox=[0.226, 0.104, 0.882, 0.469])

# Fig. 6.48 Multilinked sparse matrix

# 6.11 LINKED STACK

In Chapter 3, we have implemented stacks using arrays. However, an array implementation has certain limitations. One of the limitations is that such a stack cannot grow or shrink dynamically. This drawback can be overcome by using linked implementation. We have studied linked list implementation of a linear list. Let us study the same linked list with restriction on addition and deletion of a node to use it as a stack. A stack implemented using a linked list is also called linked stack.

Each element of the stack will be represented as a node of the list. The addition and deletion of a node will be only at one end. The first node is considered to be at the top of the stack, and it will be pointed to by a pointer called top. The last node is the bottom of the stack, and its link field is set to Null. An empty stack will have top = Null. A linked stack with elements (X, Y, Z) in order (X on top) may be represented as in Fig. 6.49.

![](bbox=[0.352, 0.812, 0.782, 0.862])

# Fig. 6.49 Linked stack of elements (X, Y, Z)