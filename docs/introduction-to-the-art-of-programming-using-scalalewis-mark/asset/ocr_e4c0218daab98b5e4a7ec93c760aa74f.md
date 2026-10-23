# 25.8 End of Chapter Material

# 25.8.1 Summary of Concepts

+   - A slightly more complex ADT than the stack or queue is that List/Seq ADT. This ADT provides methods for random access of elements.
+   - The Arrays that we have been working with are stored as single blocks of memory that can hold the required number of references. This means when you know where the block is, you know where every element is. However, inserting and removing is slow.
+   - Linked lists are an alternative approach to storing values in a sequential manner. Instead of having a large block, there are nodes that link to one or two other nodes. The list keeps track of at least one node and then others can be reached from that. This makes random access slow, but inserting and removing can be done with O(1) memory moves.
+   - In a singly-linked list, each node keeps a reference to the one node in front of it and the list must keep track of the first node. It can also keep track of the last. These boundaries become special cases that make the code more complex.
+   - A doubly-linked list has nodes that keep references to both the next element and the previous element. They are best coded with a sentinel node that stores no data and is effectively the first and last node in the list. The sentinel keeps the code for a doubly-linked list short without special cases.
+   - While random access is slow for linked lists, iterators allow efficient linear access.
+   - A singly-linked list can also be written to be immutable. This is what the List type does. In this code, the node itself represents a list and there is a special object for an empty list.
+   - The fact that an ADT does not specify how things are done can be illustrated by reimplementing the stack and queue ADTs using linked lists as the mechanism for storing data.

# 25.8.2 Exercises

+   1. Write an array-based implementation of the list ADT. You can choose to implement just the four methods listed in the first section of this chapter or implement the Buffer trait.
+   2. Compare speed of your array-based list and a linked list using the following set of manipulations.
+   3. Compare speed of doubly-linked lists using the two different node types.