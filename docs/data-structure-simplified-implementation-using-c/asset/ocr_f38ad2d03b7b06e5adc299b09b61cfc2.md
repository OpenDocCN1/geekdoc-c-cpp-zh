16. If data is a circular array of CAPACITY elements, and rear is an index into that array, what is the formula for the index after rear?
A. (rear % 1) + CAPACITY
B. rear % (1 + CAPACITY)
C. (rear + 1) % CAPACITY
D. rear + (1 % CAPACITY)

17. I have implemented the queue with a circular array, keeping track of front, rear, and Many Items (the number of items in the array). Suppose front is zero, and rear is one less than the current capacity. What can you tell me about many Items?
A. manyItems must be zero.
B. manyItems must be equal to the current capacity.
C. count could be zero or the capacity, but no other values could occur.
D. None of the above.

18. I have implemented the queue with a linked list, keeping track of a front node and a rear node with two reference variables. Which of these reference variables will change during an insertion into a NONEMPTY queue?
A. Neither changes
B. Only front changes.
C. Only rear changes.
D. Both change.

19. Priority Queues suppose getFront is called on a priority queue that has exactly two entries with equal priority. How is the return value of getFront selected?
A. One is chosen at random.
B. The one which was inserted first.
C. The one which was inserted most recently.
D. This can never happen (violates the precondition)