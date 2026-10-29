# Stacks

A stack is a last-in/first-out data structure; that is, data items are retrieved in the opposite order to which they were placed in the stack.

# Push and Pop

Adding a data item to a stack data structure is referred to as pushing the data item onto the stack. Removing a data item from a stack is referred to as popping the item off the stack.

# Self-Test Exercises

+   13. Give the definition of the member function push of the template class Stack described in Displays 17.17 and 17.19.
+   14. Give the definition of the copy constructor for the template class Stack described in Displays 17.17 and 17.19.
+   15. Give the definition of the overloaded assignment operator for the template class Stack described in Displays 17.17 and 17.19.

# EXAMPLE: A Queue Template Class

A stack is a last-in/first-out data structure. Another common data structure is a queue, which handles data in a first-in/first-out fashion. A queue can be implemented with a linked list in a manner similar to our implementation of the Stack template class. However, a queue needs a pointer at both the head of the list and at the end of the linked list, since action takes place in both locations. It is easier to remove a node from the head of a linked list than from the other end of the linked list. Therefore, our implementation will remove nodes from the head of the list (which we will now call the front of the list) and will add nodes to the other end of the list, which we will now call the back of the list (or the back of the queue).

The definition of the Queue template class is given in Display 17.20. A sample application that uses the class Queue is shown in Display 17.21. The definitions of the member functions are left as Self-Test Exercises (but remember that the answers are given at the end of the chapter should you have any problems filling in the details).