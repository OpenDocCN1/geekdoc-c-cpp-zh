+   8 Write a function that takes a binary search tree as input and produces a linked list of the entries, with the entries sorted (smallest entries at the front of the list and largest entries at the back). Hint: use in-order traversal.

+   9 Binary search trees have their best performance when they are balanced, which means that at each node, n, the size of the left subtree of n is within one of the size of the right subtree of n. Write a function that takes a sorted linked list of entries and produces a balanced binary search tree. If useful, you may add extra parameters to the procedure, such as the total number of entries in the list. Hint: First build the left subtree of the root, then the right subtree of the root, then put pieces together with the join function from Self-Test Exercise 26 on page 531. Think recursively!

+   10 Redo Programming Project 17 in Chapter 3 using a binary search tree. Use the employee's ID number as the search key. A template function should print out various statistics on the tree by taking an appropriate function as a parameter.

+   11 Create a class to store the contact phone numbers/email of your friends and relatives. Use the new class in a program that maintains a list of contacts.

+   12 Design and implement a concordance program, that stores a library of book records. Create a book class with name, ISBN, author, and publication date. Use a binary search tree to store the records, where the author name is the search key. Revise the binary search tree to be able to store and retrieve duplicate search keys.

+   13 An internal iterator for a bag is a collection of member functions that allows a programmer to step through the elements of a bag one at a time. For example, we might have an internal iterator consisting of four member functions: start, advance, is_current, and get_current. The start method initializes the internal iterator;

the is_current function is a boolean function that tells whether the iterator has a specified current element that can be retrieved with the get_current function; and the advance function moves the iterator to its next element.

For this project, add an internal iterator to the bag from Section 10.5. The implementation technique is to use a private member variable called s. The member variable s is a stack of pointers to nodes.

Each of the elements in the stack points to a node whose element has not yet been processed by the internal iterator. The current element of the internal iterator is always in the node at the top of the stack. The pseudocode for the internal iterator functions is given here:

The start function: Clear the stack. Then do an in-order traversal of the tree's nodes, pushing a pointer to each node onto the stack.

The is_current function: Return true if the stack is non-empty.

The get_current function: Check the precondition (the stack must be non-empty). Then peek at the top node on the stack (without removing it). Return the data element from this node.

The advance function: Check the precondition (the stack must be non-empty). Then pop the top node off the stack.

Changing the bag by adding or removing elements should invalidate the internal iterator (by clearing the stack).

When the internal iterator is started, use an in-order traversal to push nodes pointers onto the stack. As you pop the stack, these pointers come off in reverse order so that the iterator will advance through the elements from largest to smallest. If you prefer a smallest-to-largest order, you could use a queue instead of a stack.

+   14 In Section 6.6, we showed how to add an STL-style iterator to the bag class that was implemented with a linked list. Do the same thing for the tree-based bag class of Section 10.5.

The iterator can be implemented with a single pointer to a node, though to implement the operator that moves to the next element, it will be useful to modify the tree node so that each node has a pointer to its parent. Alternatively, each iterator could have a stack of pointers as in the previous project.