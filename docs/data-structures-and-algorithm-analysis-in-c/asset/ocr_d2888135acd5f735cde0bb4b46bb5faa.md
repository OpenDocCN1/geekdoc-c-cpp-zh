# 3.6 The Stack ADT

A stack is a list with the restriction that insertions and deletions can be performed in only one position, namely, the end of the list, called the top.

# 3.6.1 Stack Model

The fundamental operations on a stack are push, which is equivalent to an insert, and pop, which deletes the most recently inserted element. The most recently inserted element can be examined prior to performing a pop by use of the top routine. A pop or top on an empty stack is generally considered an error in the stack ADT. On the other hand, running out of space when performing a push is an implementation limit but not an ADT error.

Stacks are sometimes known as LIFO (last in, first out) lists. The model depicted in Figure 3.23 signifies only that pushes are input operations and pops and tops are output. The usual operations to make empty stacks and test for emptiness are part of the repertoire, but essentially all that you can do to a stack is push and pop.

Figure 3.24 shows an abstract stack after several operations. The general model is that there is some element that is at the top of the stack, and it is the only element that is visible.

![](bbox=[0.1, 0.46, 0.68, 0.58])

Figure 3.23 Stack model: Input to a stack is by push; output is by pop and top

![](bbox=[0.1, 0.66, 0.46, 0.88])

Figure 3.24 Stack model: Only the top element is accessible