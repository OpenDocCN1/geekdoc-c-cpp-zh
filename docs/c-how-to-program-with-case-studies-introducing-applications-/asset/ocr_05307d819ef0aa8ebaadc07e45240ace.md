```
~~~
? 1
Enter an integer: 6
The stack is:
6 --> 5 --> NULL

? 1
Enter an integer: 4
The stack is:
4 --> 6 --> 5 --> NULL

? 2
The popped value is 4.
The stack is:
6 --> 5 --> NULL

? 2
The popped value is 6.
The stack is:
5 --> NULL

? 2
The popped value is 5.
The stack is empty.

? 2
The stack is empty.

? 4
Invalid choice.

Enter choice:
1 to push a value on the stack
2 to pop a value off the stack
3 to end program
? 3
End of run.
~~~
```

**Fig. 12.2** | A simple stack program. (Part 4 of 4.)

# ### 12.5.1 Function push

**Function push** (*lines 70–82*) places a new node onto the stack using the following steps:

+   1. Call `malloc` to create a new node, then assign the allocated memory’s address to `newPtr` (line 71).
+   2. Assign to `newPtr->data` the value to push onto the stack (line 75) and assign `*topPtr` (the pointer to the stack’s top) to `newPtr->nextPtr` (line 76). The link member of the new top node now points to the previous top node.
+   3. Assign `newPtr` to `*topPtr` (line 77)—this modifies `stackPtr` in `main` to point to the new stack top.

The following diagram illustrates a push operation. Part (a) shows the stack and the new node before the push operation inserts the new node at the stack’s top—`*topPtr` represents `stackPtr` in `main`. The dotted arrows in Part (b) illustrate *Steps 2 and 3* of the preceding discussion, which insert the node containing 12 at the top.