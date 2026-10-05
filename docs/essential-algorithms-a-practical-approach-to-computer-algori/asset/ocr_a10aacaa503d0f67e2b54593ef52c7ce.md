# Stacks and Queues

Stacks and queues are relatively simple data structures that store objects in either first-in-first-out order or last-in-first-out order. They expand as needed to hold additional items, much as the linked lists described in Chapter 3. In fact, you can use linked lists to implement stacks and queues.

You can also use stacks and queues to model analogous real-world scenarios such as service lines at a bank or supermarket. But they are more often used to store objects for later processing by other algorithms such as shortest-path network algorithms.

This chapter explains stacks and queues. It explains what they are, stack and queue terminology, and methods you can use to implement them.

# Stacks

A stack is a data structure where items are added and removed in last-in-first-out order. Because of this last-in-first-out (LIFO), usually pronounced "life-oh" behavior, stacks are sometimes called LIFO lists or LIFOs.

A stack is similar to a pile of books on a desk. You can add a book to the top of the pile or remove the top book from the pile, but you cannot pull out one of the middle or bottom of the pile without making the whole thing topple.
A stack is also similar to a spring-loaded stack of plates at a cafeteria. If you add plates to the stack, the spring compresses so that the top plate is even with