Computer science offers the *abstract data types (ADTs)* like stacks, queues and trees. We call them “abstract” because they have an open implementation and are not native to a language. For instance, a data structure like a stack has an open implementation; both an array and linked list can represent a stack. Just as an `int` is operated upon by the `+`, abstract data types are also associated with a set of *methods* that can perform operations on the data they hold.

Abstract data types have to contend with overflow and underflow situations. An attempt to insert an element to a stack or queue that is full leads to an *overflow* situation. Similarly, an attempt to delete an element from a null or empty list results in an *underflow* situation. These checks are made right at the beginning of the operation. We’ll briefly examine the well-known ADTs and the essential methods used with them.

# 16.16.1 The Stack

You are already familiar with the *stack* as a container used by functions to store their parameters and local variables. This data type operates on the last-in-first-out (LIFO) principle, i.e., data that is last *pushed* onto the stack is the first to be *popped* out. Operations on a stack are carried out only at its beginning (head pointer for a linked list). The following methods (or functions) are commonly associated with a stack:

+   - *Push* — This operation inserts a data element at the top of the stack (if the stack is not full). We have already performed this operation in Program 16.8 by inserting a node at the beginning of the list.
+   - *Pop* — This operation removes the element that was last inserted into the stack (if the stack is not empty). This too has been demonstrated in Program 16.8 by deleting the first node.
+   - *Peek* — This operation evaluates the value at the top of the stack but it doesn’t delete the value.

Other operations include counting the number of elements and checking whether the stack is empty or full. A stack is often compared to a pile of plates that are added and removed only at the top. Office software (like Word and Excel) use a stack for performing undo/redo operations. The Web browser uses a stack for implementing the forward/back feature that allows a user to repeatedly step back and forth between previously visited Web pages.

# 16.16.2 The Queue

The *queue* represents exactly what we see in real life—queuing up for entry into, say, a sports field, bus or for casting votes. This abstract data type operates on the first-in-first-out (FIFO) principle; what goes in first also comes out first. Like a stack, a queue can be implemented by an array or a linked list.

An element is inserted into a queue from its rear or tail end, while deletion takes place from the front or head end. For a linked list, two pointers are used to locate the first and last item of the queue. A queue is associated with the following functions:

+   - *Enqueue* — This function adds an element to the tail end of the queue (if the queue is not full).
+   - *Dequeue* — This function deletes an element from the front end of the queue (if the queue is not empty).