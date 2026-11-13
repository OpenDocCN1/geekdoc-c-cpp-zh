3.22 Write a program to evaluate a postfix expression.

3.23 a. Write a program to convert an infix expression that includes (, ), +, -, *, and / to postfix.
b. Add the exponentiation operator to your repertoire.
c. Write a program to convert a postfix expression to infix.

3.24 Write routines to implement two stacks using only one array. Your stack routines should not declare an overflow unless every slot in the array is used.

3.25 * a. Propose a data structure that supports the stack push and pop operations and a third operation findMin, which returns the smallest element in the data structure, all in O(1) worst-case time.
* b. Prove that if we add the fourth operation deleteMin which finds and removes the smallest element, then at least one of the operations must take Ω(log N) time. (This requires reading Chapter 7.)

* 3.26 Show how to implement three stacks in one array.

3.27 If the recursive routine in Section 2.4 used to compute Fibonacci numbers is run for N = 50, is stack space likely to run out? Why or why not?

3.28 A deque is a data structure consisting of a list of items on which the following operations are possible:
push(x): Insert item x on the front end of the deque.
pop(): Remove the front item from the deque and return it.
inject(x): Insert item x on the rear end of the deque.
eject(): Remove the rear item from the dequeue and return it.
Write routines to support the deque that take O(1) time per operation.

3.29 Write an algorithm for printing a singly linked list in reverse, using only constant extra space. This instruction implies that you cannot use recursion but you may assume that your algorithm is a list member function. Can such an algorithm be written if the routine is a constant member function?

3.30 a. Write an array implementation of self-adjusting lists. In a self-adjusting list, all insertions are performed at the front. A self-adjusting list adds a find operation, and when an element is accessed by a find, it is moved to the front of the list without changing the relative order of the other items.
b. Write a linked list implementation of self-adjusting lists.
* c. Suppose each element has a fixed probability, pi, of being accessed. Show that the elements with highest access probability are expected to be close to the front.

3.31 Efficiently implement a stack class using a singly linked list, with no header or tail nodes.

3.32 Efficiently implement a queue class using a singly linked list, with no header or tail nodes.

3.33 Efficiently implement a queue class using a circular array. You may use a vector (rather than a primitive array) as the underlying array structure.

3.34 A linked list contains a cycle if, starting from some node p, following a sufficient number of next links brings us back to node p. p does not have to be the first node