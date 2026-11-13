The pop operation should not be performed when the stack is empty, and hence before every pop, we must ensure that the stack is not empty. After deleting the last element from the stack, the stack should be set to an empty state.

# GetTop

The getTop operation gives information about the topmost element and returns the element on the top of the stack. In this operation, only a copy of the element, which is at the top of the stack, is returned. Hence, the top is still set to the same element (Fig. 3.7).

![](bbox=[0.322, 0.316, 0.781, 0.422])

Fig. 3.7 The getTop operation

This is the key difference between the pop and getTop operations. The getTop operation does not modify the variable top. It signals the stack underflow error if the stack is empty.

As both insert and delete operations are allowed only at one end of the stack, it retrieves data in the reverse order in which the data is stored. In Fig. 3.8, let S = {A, B, C}.

![](bbox=[0.312, 0.621, 0.801, 0.762])

Fig. 3.8 Stack and push operations

Suppose that the order of the operations is push(A), push(B), and then push(C). When we remove these elements out of the stack, they will be removed in the order C, B, and then A. This is shown in Fig. 3.9.